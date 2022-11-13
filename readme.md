# How to share UAS data using public clouds

Written by Jinha Jung (jinha@purdue.edu), Jose Scott Landivar (jose.landivarscott@ag.tamu.edu), and Zhou Zhang (zzhang347@wisc.edu).
Please contact authors for any questions on this tutorial.

**Acknowledgement**: We really appreciate support from **![oracle](figures/oracle.gif) for Research** for providing Oracle Cloud Infrastructure (OCI) credits. Please contact Bryan Barker (bryan.barker@oracle.com) for any further questions on OCI.

## How to set up a web server using OCI

1. Creating an account on OCI - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/00-oci_configuration/readme.md)
2. Creating a new instance with Linux OS - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/00-oci_configuration/create_new_instance.md)
3. Installing and configuring a web server - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/01-configuring_web_server/readme.md)
4. Additional storage space
   - Connect object storage for large data storage - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/00-oci_configuration/object_storage.md)
   - Connect block storage - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/00-oci_configuration/block_volumes.md)

## How to share raster data as a web service

1. Uploading raster data via SFTP - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/02-share_raster_data/upload_raster_data_via_sftp.md)
2. Configuring FOSS environments - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/02-share_raster_data/readme.md)
3. Generating tile map layers - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/02-share_raster_data/readme.md)
4. Configuring tile map service - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/02-share_raster_data/readme.md)

## How to share 3D point cloud data as a web service - [here](https://github.com/gdslab/uas_data_sharing_via_clouds/blob/main/03-share_3d_point_cloud_data/readme.md)

1. Uploading point cloud data via SFTP
2. Configuring FOSS environments
3. Converting point cloud data into Potree format
4. Configuring 3D point cloud visualization service
