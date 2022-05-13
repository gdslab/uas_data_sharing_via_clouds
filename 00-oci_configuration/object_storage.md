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
