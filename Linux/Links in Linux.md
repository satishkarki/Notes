# Soft Link and Hard Link in Linux

In Ubuntu (and other Linux-based operating systems), a "hard link" is a type of file link that points directly to the physical location of a file on a file system. This means that if multiple hard links point to the same file, changes made to one hard link will be reflected in all other hard links.

A "soft link," also known as a "symbolic link," is a type of file link that points to the file path of another file. This means that if multiple soft links point to the same file, changes made to the file will be reflected in all soft links, but changes to the properties of one soft link will not affect the other soft links.

In summary, a hard link is a direct link to the inode of a file, while a soft link is a link to the file path, and it is more like a Windows shortcut.



For example, let's say you have a file called "document.txt" in your home directory.

If you create a hard link to "document.txt" and name it "document-hardlink.txt," any changes you make to "document-hardlink.txt" will also be made to the original "document.txt" file. This is because both "document.txt" and "document-hardlink.txt" are now pointing to the same physical location on the file system.

If you create a soft link to "document.txt" and name it "document-softlink.txt," any changes you make to the original "document.txt" file will be reflected in "document-softlink.txt," but changes made to the properties of "document-softlink.txt" (such as permissions) will not affect the original "document.txt" file. This is because "document-softlink.txt" is pointing to the file path of "document.txt" rather than the physical location.

You can create a hard link by using the command: `ln <source-file> <link-name>`

You can create a soft link by using the command: `ln -s <source-file> <link-name>`

For example: 

`ln document.txt document-hardlink.txt` 

`ln -s document.txt document-softlink.txt`