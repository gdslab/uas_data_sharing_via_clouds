# Upload raster data via SFTP

As a first step to share the raster data, we need to upload the raster file to the server we configured earlier. We will use SFPT client to do this.

## Configuring SFTP client

You can use [FileZilla](https://filezilla-project.org) to connect to the server via SFPT protocol.

* username: ubuntu
* password: leave blank
* hostname: [public ip address] of the server
* ssh key setting

With the information above, now you can click "connect" button.

Once you're connected to the server, you can move into the directory where you would like to upload files, then simply drag and drop to upload files.

Things to consider when uploading files...

* You may want to upload files under the **DOCUMENT_ROOT** folder so that you can share the link to download the original raster data as well.
* You may want to upload big files to either *object storage* or *block storage* so that storage space on the server gets too low. 
