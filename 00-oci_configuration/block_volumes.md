# Adding block volume

## Creating a Volume

Open the navigation menu and click Storage. Under Block Storage, click Block Volumes.

1. Click Create Block Volume.
2. In the Create Block Volume dialog, enter the following:
  * Create in Compartment: This field defaults to your current compartment. Select the compartment you want to create the volume in, if not already selected.
  * Name: Enter a user-friendly name. Avoid entering confidential information.
availability domain: Select the same availability domain  that you selected for your instance. If you followed the tutorial instructions when launching your instance, this is the first AD in the list. The volume and the instance must be in the same availability domain.
  * Size: Enter 50 to create a 50 GB block volume.
  * Backup Policy: Do not select a backup policy.
  * Tags: Leave the tagging fields blank.
3. Click Create Block Volume.


A 50 GB block volume is displayed in the provisioning state. When the volume is no longer in the provisioning state, you can attach it to your instance.

## Attaching the Volume to an Instance

Next you attach the volume via an iSCSI  network connection to your instance:

1. Find your instance: Open the navigation menu and click Compute. Under Compute, click Instances.
2. Click your instance name to view its details.
3. In the Resources section, click Attached block volumes.
4. Click Attach block volume.
5. Enter the following:
  * Volume: select the Select volume option.
  * If you need to change the comparment, click Change Compartment, and then select the compartment where you created the block volume.
  * Volume in <compartment>: Select the block volume from the list.
  * Attachment type: Select ISCSI.
  * Require CHAP Credentials: Leave cleared.
  * Device Path: If the instance supports consistent device paths, you will see a list of device paths. Select one from the list.
  * Access: Select Read/Write.
6. Click Attach.

The attachment process takes about a minute. You'll know the volume is ready when the Attachment State for the volume is ATTACHED.

## Connecting to the Volume

After your volume is attached, you can configure the iSCSI connection. You connect to the volume using the iscsiadm command-line tool. The commands you need to configure, authenticate, and log on are provided by the Console so you can easily copy and paste them into your instance session window. After the connection is configured, you can mount the volume on your instance and use it just as you would a physical hard drive.

To connect to your volume:

1. Log on to your instance as described in Connecting to Your Instance.
2. Open the navigation menu and click Compute. Under Compute, click Instances.
3. Click your instance name to view its details.
4. In the Resources section, click Attached block volumes.
5. Click the Actions menu next to the volume you just attached and then click iSCSI commands & information.

The iSCSI commands & information dialog is displayed. Notice that the dialog displays specific identifying information about your volume (such as IP address and port) as well as the iSCSI commands you'll need to use. The commands are ready to use with the appropriate information already included in each command.
The Connect commands configure the iSCSI connection and log on to iSCSI. Copy and paste each command from the Connect list into the instance session window.

6. Be sure to paste and run each command individually. There are three attach commands. Each command begins with `sudo iscsiadm`.
7. After entering the final command to log on to iSCSI, you are ready to format (if needed) and mount the volume. To get a list of mountable iSCSI devices on the instance, run the following command:

```
sudo fdisk -l
```

If your disk attached successfully, you'll see it in the returned list as follows:

```
Disk /dev/sdb: 50.0 GB, 50010783744 bytes, 97677312 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 1048576 bytes
```
