# Hands on Guide on Linux Server

#### Copy Anythig
```bash
cp /home/doe/folder_name/august/invoice.blade.php .
```


#### Laravel on CentOs
```bash

chmod u+x setup.sh

chown -R apache.apache /var/www/laravel
chmod -R 755 /var/www/laravel
chmod -R 755 /var/www/laravel/storage
//SELinux enabled systems also run the below command to allow writing on the storage directory.
chcon -R -t httpd_sys_rw_content_t /var/www/laravel/storage // Must use this.
chcon -R -t httpd_sys_rw_content_t /var/www/html/ng-journal/bootstrap // Must use this.

```

#### Find anything
```

```

#### Glances
```
gances
```

#### Basic Command:

```
ls -la // For check file permission.
ls // List of file.
pwd // Print the current working directory.
mkdir directory_name // mkdir: Create a new directory.
rm file_name // Remove file.
rm -r directory_name // Remove file and directories.
mv old_file new_file // Rename files and directories.
mv file_name /path/to/new_directory // Move files and directories.
cat file_name // Display the contents of a file.
grep pattern file_name // Search for patterns in files.
chmod permissions file_name // Change the permissions of a file or directory.
chown user:group file_name // Change the ownership of a file or directory.
su // Root permission.
nano file_name // Edit a file.
```

#### Networking:
```
traceroute google.com  // Trace the route to google.com
wget https://example.com/file.zip // Download a file from a web server
sudo systemctl restart httpd // Restart apache.
sudo systemctl restart mysqld // Restart MySql.
```
