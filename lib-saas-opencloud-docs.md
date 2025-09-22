---
title: lib-saas-opencloud-docs
tags: [docs, opencloud]
created: 2025-09-22T12:32:53.355Z
modified: 2025-09-22T12:33:00.828Z
---

# lib-saas-opencloud-docs

# guide

# overview
- OpenCloud is designed to give you a privacy-focused alternative to mainstream platforms like Microsoft OneDrive or Google Drive, freeing you from reliance on big tech services and their data-collection practices.
- OpenCloud is a fully self-hosted (on-premise) solution, meaning you have complete control over where your data is stored.

- OpenCloud allows you customizations:
  - Wordings: You can replace specific terms, such as changing the word “Spaces” to “Datarooms” to better fit your terminology.
  - Extensions: The web UI also supports custom web extensions. 

- Does it support integration with third-party storage solutions like S3 Storage?
  - Posix Storage
  - S3ng
  - Ceph

- 
- 
- 
- 

# [FAQ | OpenCloud Docs](https://docs.opencloud.eu/docs/admin/resources/faq)
- Is OpenCloud 100% open source?
  - Yes. The source code of OpenCloud is licenced under the Apache 2 licence.

- OpenCloud is simpler and more reliable than existing PHP-based solutions. 
  - OpenCloud stands out by offering a radically simplified architecture compared to other open-source file-sharing solutions.
  - It writes data directly to disk instead of relying on a dedicated database, making it much easier to maintain and far more reliable. 

- What types of files can I store and share with OpenCloud?
  - No restrictions. You can store and share any filetype. 
  - If necessary, you can restrict the upload of certain filetypes like .exe or documents with macros like xlsm.

- Is there an upload file size limit in OpenCloud?
  - No

- Does OpenCloud support real-time collaboration and editing?
  - Yes. We use the WOPI standard for realtime collabration in the web office application Collabora.

- Can I create and manage user accounts and permissions?
  - Yes, you can either use the built-in user management system or integrate OpenCloud with your existing identity management.

- 
- 
- 
- 
- 
- 

# docs
- 🧩 PosixFS is a storage driver that saves OpenClouds files and folders in a folder structure how the user sees that in the web interface or other clients. 
  - That is a difference to the previously used driver DecomposedFS, which stores files in a technical folder structure that has limited meaning for admins.
- PosixFS Driver supports two different modes:
  - The non collaborative mode where the filesystem tree in use is exclusively granted to OpenCloud
  - The collaborative mode where modifications of the underlying file tree are permitted by other processes than OpenCloud

- To ensure reliable operation in non-collaborative mode, the underlying file system used by the PosixFS driver must not be modified while OpenCloud is running. 
  - The assigned file system tree must be exclusively reserved for access by OpenCloud. 
  - All files and directories must be owned by the same user and group under which the OpenCloud process is running. 
  - File and directory permissions must allow OpenCloud to read, write, and traverse the entire tree.
  - These conditions are automatically fulfilled as long as the root directory of the assigned tree is writable.

- When OpenCloud starts up, it scans the assigned file system tree for newly added or modified files and directories. 
  - During this process, metadata is updated and internal caches are built accordingly. This is referred to as the assimilation(吸收；消化) of new resources.
  - It is important to note that assimilation does not trigger post-upload checks, such as virus scanning. Since the files are already in their final location within the file system, such checks would be ineffective at this stage and are therefore skipped.
  - However, indexing for the search service does take place for assimilated resources.

- When OpenCloud with PosixFS starts up, it is running over the entire file system to warm up the caches. This might take some time.

- With PosixFS backup and restore is easy. The entire OpenCloud filesystem tree can be snapshotted regularly and restored as needed. It depends on the filesystem type how that has to be done in detail.

- PosixFS in this so called non collaborative mode is the default for new installations of OpenCloud. 
  - There is currently no way to migrate OpenCloud installations with DecomposedFS backend to PosixFS.
  - If that is needed, data needs to be copied into a new installation of OpenCloud.

- PosixFS Non Collaborative Mode
  - When OpenCloud is shut down, limited manipulation of the underlying file system tree is possible for certain administration tasks such as adding/removing/renaming files/folders
  - Whenever files are manipulated externally to OpenCloud, it is important to remember to shut down OpenCloud before starting

- PosixFS Collaborative Mode
  - collaborative mode allows the file system to be modified while OpenCloud is running
  - Changes made in this mode are reflected in real time in OpenCloud clients.
  - Compared to non-collaborative mode, collaborative mode requires significantly more system resources to monitor the file system. 
  - External access to files is permitted under specific conditions. File changes are detected and assimilated in real time.

- 🧩 Decomposeds3 is a storage driver for OpenCloud that uses MinIO — an S3-compatible object storage — to store files efficiently. 

- Configuration files are written as yaml files by default under `$HOME/.config/OpenCloud`.

- OpenCloud stores files by default in the file system under the path `/var/lib/opencloud/`. 
  - Any other path that is local to the server instance running the OpenCloud backend can be configured as alternative path using the environment variable `OC_BASE_DATA_PATH`.
  - Files and folders are stored in a folder structure underneath that base path in folder `data/storage/users/`.
- Files are by default stored in the original format and not encrypted.
- File metadata is stored in the file system with every file. 
  - It is either in the extended file attributes (user namespace) or in a separate metadata file. That file is in the `MessagePack` format and can be read with the CLI tools for that file type.

- Other, non-file-related metadata such as links is also stored under the general data base path, in JSON format.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# more
