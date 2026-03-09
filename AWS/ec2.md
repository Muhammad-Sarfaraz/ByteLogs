# EC2

EC2 Storage Increase

To expand the root partition after increasing the EC2 volume size:

```sh
# Check current disk usage
df -h

# Extend the partition to use the new space
sudo growpart /dev/xvda 1

# Resize the filesystem
sudo resize2fs /dev/xvda1

# Verify the updated disk usage
df -h
```
