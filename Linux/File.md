#### Metadata

- **Inode Number**: Every file in a Linux filesystem is represented by an inode, which is a unique identifier. The inode contains information about the file's location, size, permissions, timestamps, and other attributes.

- **File Permissions**: The file permissions define who can read, write, or execute the file. The permissions are represented by three sets of three characters (e.g., -rw-r--r--) for user, group, and others.

- **Owner and Group**: The file metadata includes information about the owner and group associated with the file. The owner is the user who created the file, and the group is a collection of users with shared access permissions.

- **Timestamps**: Linux stores three timestamps for each file: Access Time (atime): The last time the file was accessed (read). Modification Time (mtime): The last time the content of the file was modified. Change Time (ctime): The last time the inode metadata of the file was modified (e.g., permissions change).

- **File Size**: The size of the file in bytes.

- **File Type**: The type of the file, which could be regular file, directory, symbolic link, character device, block device, socket, or FIFO (named pipe).

- **Symbolic Links**: If the file is a symbolic link, the metadata holds the information about the target file or directory.

- **Extended Attributes**: Some filesystems support extended attributes, which are additional metadata associated with a file. These attributes can hold various information beyond the traditional metadata, such as file checksums or custom data.

- **File System Information**: The file metadata includes information about the file system, such as the type of filesystem, the device on which the file is stored, and the file system block size.

- **Inode Metadata**: The inode itself holds additional metadata, like the number of hard links to the file, file owner's user ID and group ID, disk block addresses for data storage, and more.

- The folder's metadata lists the names and locations of the files and sub-folders within the directory. 

#### Links

    Hard Links:
        A hard link is another name (link) for an existing file or directory.
        It points directly to the inode of the original file on the filesystem.
        Hard links share the same inode number as the original file, so they essentially refer to the same data blocks on the disk.
        Changes made to the original file are also reflected in all its hard links because they are just different names for the same underlying data.
        Hard links cannot span different filesystems or partitions since inodes are specific to a particular filesystem.
        Deleting a hard link does not affect the original file unless it is the last remaining hard link. In that case, the file's data is freed once all hard links are removed.

    Symbolic Links (Symlinks):
        A symbolic link (symlink) is a separate file that contains a path or reference to the target file or directory.
        Symlinks act as pointers to the target and do not share the same inode or underlying data blocks.
        If you access a symlink, it will redirect you to the actual file or directory it points to.
        Changes made to the original file are immediately reflected in the symlink, but modifying the symlink itself does not affect the original file.
        Symbolic links can span different filesystems or partitions since they contain a path that can be on a different device.
        If the target file or directory is deleted or moved, the symlink becomes "broken" or "dangling" and will not work until the target is restored or relinked.