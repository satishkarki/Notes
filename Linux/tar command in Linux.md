

tar stands for tape archive. It is used to create an archive or extract the archive. A compressed or uncompressed archive can be created with it. A file with tar extension is commonly called "tarball".

***

## Syntax

```bash
tar [options] [archive-file] [file or directory to be archived]
```

| options                                                      |
| ------------------------------------------------------------ |
| **-c :** Creates Archive                                     |
| **-x :** Extract the archive                                 |
| **-f :** creates archive with given filename                 |
| **-t :** displays or lists files in archived file            |
| **-u :** archives and adds to an existing archive file       |
| **-v :** Displays Verbose Information                        |
| **-A :** Concatenates the archive files                      |
| **-z :** zip, tells tar command that creates tar file using gzip |
| **-j :** filter archive tar file using tbzip                 |
| **-W :** Verify a archive file                               |
| **-r :** update or add file or directory in already existed .tar file |

***

### The magic behind configure, make, make install

```bash
./configure    #Configure the software
make           #Build the software
make install   #Install the software
```

[Learn the magic](https://thoughtbot.com/blog/the-magic-behind-configure-make-make-install)

***

## Example

```bash
# Download the desired .tar.gz or (.tar.bz2) file
# Open Terminal

# Extract the .tar.gz or (.tar.bz2) file with the following commands
tar xvzf PACKAGENAME.tar.gz
tar xvjf PACKAGENAME.tar.bz2

# Navigate to the extracted folder using cd command
cd PACKAGENAME

# Now run the following command to install the tarball
./configure
make
sudo make install
```





