### Notes
In an inode is the owner, create time, permissions, and length. Extension is just for users.
All `ls` does is read the datablocks of an inode, so placement policies don't affect a single inode `ls`. 

### Redundancy
If A and B are two pieces of data and knowing A eliminates some values of B, there is redundancy between A and B. 
RAID with mirrored disks has complete redundancy, and parity blocks have partial redundancy. 
This also includes the superblock with the total blocks and inodes with the pointer to data blocks. 

Redundancy can cause a problem if one of the two pieces of data is written to, and the system crashes before writing to the other one. We want consistency in our file system. 

## File System ChecKer (FSCK)
After a crash, we can scan the whole disk for contradictions and fix them. We can also keep the system offline until FSCK completes. 
