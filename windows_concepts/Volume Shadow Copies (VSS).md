Volume Shadow Copy Service (VSS) is a feature in Microsoft Windows that allows the OS or applications to periodically take "point-in-time snapshots" of an entire disk without locking the filesystem.

Shadow copies are only capture the changed bits of each file and so do not require a lot of storage space. They are also fast and easy to recover directly from Windows.

## Configuring Volume Shadow Copies (VSS) on Windows Server

### Prerequisite steps
[create an additional disk](http://helpcenter.itopia.com/manage/add-new-disk-to-a-server) to hold the Shadow Copies

### Enabling Volume Shadow Copies on Disk
![[shadow_copies1_windows_stuffs.png]]

1. Click on the Volume you want to enable Shadow Copies for, then click **Settings**.

- Under _Storage Area_, change the location to the additional disk you created in the Prerequisite Steps section of this document. You can also change the size limit of the volume copies. If this storage limit is reached, it will automatically delete the oldest copy.
- The **Schedule** button allows you to set a preferred schedule to capture the Shadow Copies
![[shadow_copies2_windows_stuffs.png]]

2. In the _Shadow Copies_ window, ensure the volume is still selected and click **Enable**. Windows will create the first Shadow Copy with the settings you implemented and will use the schedule to create subsequent Copies.

## Reverting Changes

1. When a file or folder has been modified (or deleted) and you would like to revert the changes, right-click on the file/folder and select **Restore previous versions**.
![[shadow_copies3_windows_stuffs.png]]

2. From the list of versions, select the desired version, click **Restore**, and then click **Restore** again in the dialogue prompt.
![[shadow_copies4_windows_stuffs.png]]

3. Click **OK** in the final two boxes and the process is complete.
![[shadow_copies5_windows_stuffs.png]]