### Notes
In an inode is the owner, create time, permissions, and length. Extension is just for users.
All `ls` does is read the datablocks of an inode, so placement policies don't affect a single inode `ls`. 

### Redundancy
If A and B are two pieces of data and knowing A elminates some values of B, th