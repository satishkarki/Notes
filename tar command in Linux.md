## tar command in Linux

- tar stands for tape archive. 

- It is used to create an archive or extract the archive

- We can create a compressed or uncompressed archive with it

- Syntax

  ```linux
  tar [options] [archive-file] [file or directory to be archived]
  ```

  **-c :** Creates Archive 
  **-x :** Extract the archive 
  **-f :** creates archive with given filename 
  **-t :** displays or lists files in archived file 
  **-u :** archives and adds to an existing archive file 
  **-v :** Displays Verbose Information 
  **-A :** Concatenates the archive files 
  **-z :** zip, tells tar command that creates tar file using gzip 
  **-j :** filter archive tar file using tbzip 
  **-W :** Verify a archive file 
  **-r :** update or add file or directory in already existed .tar file 

Example:

File Name: "blender-2.93.4-linux-x64.tar.xz"

Note: .xz is a compression format different when compared to common file format like RAR, Zip and 7z. It is a lossless data compression file format. BZIP2 and GZIP are some of the other application to compress/decompress.





