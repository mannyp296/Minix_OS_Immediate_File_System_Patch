README: CS170 Project 3
Alex King and Manuel Perez

OVERVIEW:
This patch implements an immediate file system and an LSR system call. The
immediate file system uses the data block as a means to store small files instead
using the blocks as pointers to larger blocks of data. The LSR system call can
determine if a particular file is immediate or not and it also indicates how
many blocks of data were read from that file.


IMMEDIATE FILES:
-We tested our immediate files for: creating a new immediate file, creating a new regular file ( > 32 Bytes ), adding to an immediate file to create a regular file, rewriting an immediate file with a smaller amount of data, deleting an immediate file


LSR SYSTEM CALL:
-If the system call is used on a nonexistent file, it prints out a series of errors relating to page faults and such. This is not an error. We are using it as our error message.
-We tested the part about printing the process IDs by creating a program which opens a file and sleeps for 30 seconds. In the meantime, we ran the lsr function on that file to see if it would capture the pid of the sleeping process.
-We tested the block printing section by putting files of various sizes in and running it on them, checking if it would output the correct number of blocks.
-It has special print statements for immediate files and files with no data in them.

THE FILES

Immediate File Section:

SERVERS/VFS
-open.c  set files to I_IMMEDIATE by default, allow immediate files to be truncated
-link.c  allow immediate files to be truncated

SERVERS/MFS
-read.c  almost everything: implementing imm, upgrading to reg, add wipe_inode
-write.c add immediate check in write_map
-link.c  nothing

INCLUDE/MINIX
-const.h add I_IMMEDIATE value


System Call Section:

SERVERS/VFS
-table.c add system call to call_vector
-proto.h add system call declaration
-misc.c  add system call definition

SERVERS/MFS
-table.c add system call to call_vector
-proto.h add system call declaration
-misc.c  add system call definition

LIB/LIBC/SYS-MINIX
-lsr.c   add lsr syscall
-Makefile.inc  add lsr.c

INCLUDE/MINIX
-callnr.h add LSR syscall

INCLUDE
-unistd.h