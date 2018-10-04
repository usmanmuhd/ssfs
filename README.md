# SSFS

## Command to run the ssfs program

1. Create a directory by some name so that fuse thing can be mounted.
	`$ mkdir Fuse_Files`
2. Compile the ssfs program
	`$ gcc -D_FILE_OFFSET_BITS=64  ssfs.c` 
	If this compile with no error then:

	`$ ./ssfs /path_to_/FuseFiles`
	Cat and ls are the only two commands which works with the ssfs
	go to Fuse_Files
	`$ cd Fuse_Files`
	`$ ls` (Will list all the files in the Fuse_Files)
	`$ cat filename`(Will output the content of the particular)

	cat and ls are the only two operations supported .
	To check if other operation can be performed or no,
	Try:
	`$ echo "Hello" > File.txt` This might give an error as ssfs doesnt have any code related to writing to a particular file
If error :
	(Error: No such file.h) then
		`$ sudo apt-get update && sudo apt-get install libfuse-dev`
		Repeat the step number 2

	(Error : Undefined reference to fuse_main_real):
		`$ sudo apt install pkg-config`
		`$ sudo apt-get install pkgconf`

	After the installation is done
	Compile the file

	```
	$ gcc -Wall  -o ssfs ssfs.c `pkg-config fuse --cflags --libs`
	$ ./ssfs /path_to_/FuseFiles
	$ cd Fuse_Files
	$ ls (Will list all the files in the Fuse_Files)
	$ cat filename(Will output the content of the particular)```

To check the system calls happening when the ssfs is being run,
On one of the terminal run
`$ ./ssfs -f /path_to_Fuse_File`

Open the other terminal
`$ cd Fuse_Files`
`$ ls` (On the other terminal you will be able to see the system call happening)

3. After all the operations are done unmount the directories created
`$ sudo umount /path_to/Fuse_Files`	

