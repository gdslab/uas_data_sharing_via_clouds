This document include instruction on how to set up an object storage and connect the storage with compute instance. 

# Create an object storage

Using https://docs.oracle.com/en-us/iaas/Content/Object/Tasks/managingbuckets.htm 

To create a bucket
1. Open the navigation menu and click Storage. Under Object Storage, click Buckets.
2. Select a compartment from the Compartment list on the left side of the page. A list of existing buckets is displayed.
3. Click Create Bucket.
4. In the Create Bucket dialog box, specify the attributes of the bucket:
  * Bucket Name: The system generates a default bucket name that reflects the current year, month, day, and time, for example bucket-20190306-1359. If you change this default to any other bucket name, use letters, numbers, dashes, underscores, and periods. Avoid entering confidential information.
  * Default Storage Tier: Select the default tier in which you want to store your data. When you upload objects, the objects are automatically assigned to and uploaded to this tier by default. Available default storage tiers include:
    * Standard is the primary, default storage tier used for Object Storage service data. Use the Standard tier for storing data that requires fast and immediate access. Standard buckets do, however, provide an option to assign and upload objects to different storage tiers (Infrequent Access and Archive), while remaining in the Standard bucket.
    * Archive is the default storage tier used for Archive Storage service data. Use the Archive tier for storing data that does not require immediate access, but requires long retention periods. Access to data in the Archive tier is not immediate. Archived data must be restored before the data is accessible.
  * Select Enable Auto-Tiering if you want Object Storage to monitor and automatically move infrequently accessed objects from the Standard tier to the less expensive Infrequent Access storage tier. For more information, see Enabling Auto-Tiering.
  * Select Enable Object Versioning if you want Object Storage to create an object version each time the content changes or the object is deleted. For more information, see Using Object Versioning.
  * Select Emit Object Events if you want to enable the bucket to emit events for object state changes. For more information about events, see Overview of Events.
  * Select Uncommited Multipart Uploads Clean-up to create a lifecycle rule that automatically deletes all uncommitted multipart uploads after 7 days.
  * Encryption: Buckets are encrypted with keys managed by Oracle by default, but you can optionally encrypt the data in this bucket using your own Vault encryption key. To use Vault for your encryption needs, select Encrypt Using Customer-Managed Keys. Then, select the Vault Compartment and Vault that contain the master encryption key you want to use. Also select the Master Encryption Key Compartment and Master Encryption Key. For more information about encryption, see Overview of Vault. For details on how to create a vault, see Managing Vaults.
  * Tags: If you have permissions to create a resource, then you also have permissions to apply free-form tags to that resource. To apply a defined tag, you must have permissions to use the tag namespace. For more information about tagging, see Resource Tags. If you are not sure whether to apply tags, skip this option (you can apply tags later) or ask your administrator.
5. Click Create.

The bucket is created immediately and you can start uploading objects. Objects added to archive buckets are immediately archived and must be restored before they are available for download.

# Mounting an Object storage bucket as file system on OCI

Following https://blogs.oracle.com/cloud-infrastructure/post/mounting-an-object-storage-bucket-as-file-system-on-oracle-linux

Recently, I found that I need to move a lot of automatically generated report files to Object Storage for easy delivery. I could do this in one of several ways: by writing a Python script using Oracle Cloud Infrastructure SDKs, using pre-authenticated requests, writing curl, and bash scripts. But I thought it would be nice to access Object Storage content directly using a file system without having to change any of my existing automation scripts.

Thanks to the s3fs-fuse project and Oracle Cloud Infrastructure's S3 compatible API, this is possible and pretty easy to do.

For this tutorial, you need an Oracle Cloud Infrastructure account, and Oracle Linux 7 compute instance, SSH, and about 10 minutes. Let's start!

## Prerequisites:

Make sure that bucket you're trying to mount is in the compartment listed for S3 compatibility, by default it's a root compartment of the tenancy.

If you need to change that, settings are located under Administration->Tenancy Details->Edit Object Storage Settings

### Step 1: Install s3fs-fuse

You can install s3fs-fuse either from source or by using a prebuilt package from the Oracle Linux EPEL repository. In this post, I'm using the binary RPM.

```
$ sudo yum install s3fs-fuse
```

### Step 2: Configure Credentials

In the Oracle Cloud Infrastructure Console, click the Profile icon in the top-right corner, and select User Settings.

Click Customer Secret Keys, and then click Generate Secret Key.

Give the key a meaningful name (for example, s3fs-access), and then click Generate Secret Key. 

Copy and save the secret key because it won't be shown again.

The S3 credentials are created by using an access key and the secret key. The access key is displayed in the Customer Secret Keys area of the Console.

Enter your credentials in a ${HOME}/.passwd-s3fs file and set owner-only permissions:

```
$ echo ACCESS_KEY_ID:SECRET_ACCESS_KEY > ${HOME}/.passwd-s3fs
$ chmod 600 ${HOME}/.passwd-s3fs
```

### Step 3: Mount the File System

Run the mount by using the following command:

```
s3fs [bucket] [destination directory] -o endpoint=[region] -o passwd_file=${HOME}/.passwd-s3fs -o url=https://[namespace].compat.objectstorage.[region].oraclecloud.com/ -onomultipart -o use_path_request_style
```

As shown, S3-compatible endpoints are built in the following format:

```
mynamespace.compat.objectstorage.aa-region-1.oraclecloud.com
```

If you are using the opc user, you will see the following error:

```
fuse: failed to exec fusermount: Permission denied
```

Run the following command, and then try again:

```
sudo chmod +x /usr/bin/fusermount
```

Now you can use the Object Storage bucket as a mostly POSIX-compliant file system.

