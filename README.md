# CSC-360-Assignment-3-A-Simple-File-System-SFS-solution

Download Here: [CSC 360 Assignment 3: A Simple File System (SFS) solution](https://jarviscodinghub.com/assignment/assignment-3-a-simple-file-system-sfs-solution/)

For Custom/Original Work email jarviscodinghub@gmail.com/whatsapp +1(541)423-7793

In this assignment, you will implement utilities that perform operations on a simple file system, FAT12, used by
3 MS-DOS.
4 1.1 Sample File Systems
5 You will be given a file system image: disk.IMA for self-testing, but your submission may be tested against other
6 disk images following the same specification.
7 You should get comfortable examining the raw, binary data in the file system images using the program xxd.
8 2 Requirements
9 2.1 Part I
10 In part I, you will write a program that displays information about the file system. In order to complete part I,
11 you will need to understand the file system structure of MS-DOS, including FAT Partition Boot Sector, FAT File
12 Allocation Table, FAT Root Folder, FAT Folder Structure, and so on.
13 For example, your program for part I will be invoked as follows:
./diskinfo disk.IMA
14 Your output should include the following information:
OS Name:
Label of the disk:
Total size of the disk:
Free size of the disk:
==============
The number of files in the disk (including all files in the root directory and files in all subdirectories):
=============
Number of FAT copies:
Sectors per FAT:
15 Note 1: when you list the total number of files in the disk, a subdirectory name is not considered
16 as a normal file name and thus should not be counted.
17 Note 2: For a directory entry, if the field of “First Logical Cluster” is 0 or 1, then this directory
18 entry should not be counted.
19 Note 3: Total size of the disk = total sector count * bytes per sector
20 Note 4: Free size of the disk = total number of sectors that are unused (i.e., 0x000 in an FAT
21 entry means unused) * bytes per sector. Remember that the first two entries in FAT are reserved.
1
22 2.2 Part II
23 In part II, you will write a program, with the routines already implemented for part I, that displays the contents of
24 the root directory and all sub-directories (possibly multi-layers) in the file system.
25 Your program for part II will be invoked as follows:
./disklist disk.IMA
26 Starting from the root directory, the directory listing should be formatted as follows:
27 • Directory Name, followed by a line break, followed by “==================”, followed by a line
28 break.
29 • List of files or subdirectories:
30 – The first column will contain:
31 ∗ F for regular files, or
32 ∗ D for directories;
33 followed by a single space
34 – then 10 characters to show the file size in bytes, followed by a single space
35 – then 20 characters for the file name, followed by a single space
36 – then the file creation date and creation time.
37 – then a line break.
38 Note: For a directory entry, if the field of “First Logical Cluster” is 0 or 1, then this directory
39 entry should be skipped and not listed.
40 2.3 Part III
41 In part III, you will write a program that copies a file from the file system to the current directory in Linux. If the
42 specified file cannot be found in the file system, you should output the message File not found. and exit.
43 Note: In order to find a file in the file system, the root directory and all subdirectories (possibly
44 multi-layers) should be searched.
45 Your program for part III will be invoked as follows:
./diskget disk.IMA ANS1.PDF
46 If your code runs correctly, ANS1.PDF should be copied to your current Linux directory, and you should be able
47 to read the content of ANS1.PDF.
48 2.4 Part IV
49 You will write a program that copies a file from the current Linux directory into specified directory (i.e., the root
50 directory or a subdirectory) of the file system. If the specified file is not found, you should output the message File
51 not found. and exit. If the specified directory is not found in the file system, you should output the message The
52 directory not found. and exit. If the file system does not have enough free space to store the file, you should
53 output the message No enough free space in the disk image. and exit.
54 Your program will be invoked as follows:
./diskput disk.IMA \subdir1\subdir2\foo.txt
55 where subdir1 is a sub-directory of the root directory and subdir2 is a sub-directory of subdir1, and foo.txt is
56 the file name. If no specified directory is given, then the file is copied to the root directory of the file system, e.g.,
./diskput disk.IMA foo.txt
57 will copy foo.txt to the root directory of the file system.
58 Note that a correct execution should update FAT and related allocation information in disk.IMA accordingly.
59 To validate, you can use diskget implemented in Part III to check if you can correctly read foo.txt from the file
60 system.
2
61 3 File System Specification
62 The specification of FAT12 and related information could be found in Connex -¿ Resources.
63 4 Byte Ordering
64 Different hardware architectures store multi-byte data (like integers) in different orders. Consider the large integer:
65 0xDEADBEEF
66 On the Intel architecture (Little Endian), it would be stored in memory as:
67 EF BE AD DE
68 On the PowerPC (Big Endian), it would be stored in memory as:
69 DE AD BE EF
70 Since the FAT was developed for IBM PC machines, the data storage is in Little Endian format, i.e. the least
71 significant byte is placed in the lowest address. This will mean that you have to convert all your integer values to
72 Little Endian format before writing them to disk.
73 5 Submission Requirements
74 What to hand in: You need to hand in a .tar.gz file containing all your source code, readme.txt, and a Makefile
75 that produces the executables (i.e., diskinfo, disklist, diskget, and diskput).
76 The file is submitted through connex.csc.uvic.ca site.
77 6 Marking Scheme
78 We will mark your code submission based on correct functionality and code quality.
79 6.1 Functionality
80 1. Your programs must correctly output the required information in Part I, II, and III. One sample disk image is
81 provided to you for self-learning and self-testing. Nevertheless, your code may be tested with other disk images
82 of the same file system. We will not test your code with a damaged disk image. We will not disclose all test
83 files before the final submission. This is very common in software engineering.
84 2. You are required to catch return errors of important function calls, especially when a return error may result
85 in the logic error or malfunctioning of your program.
86 6.2 Code Quality
87 We cannot specify completely the coding style that we would like to see but it includes the following:
88 1. Proper decomposition of a program into subroutines (and multiple source code files when necessary)—A 1000
89 line C program as a single routine would fail this criterion.
90 2. Comment—judiciously, but not profusely. Comments also serve to help a marker, in addition to yourself. To
91 further elaborate:
92 (a) Your favorite quote from Star Wars or Douglas Adams’ Hitch-hiker’s Guide to the Galaxy does not count
93 as comments. In fact, they simply count as anti-comments, and will result in a loss of marks.
94 (b) Comment your code in English. It is the official language of this university.
95 3. Proper variable names—leia is not a good variable name, it never was and never will be.
96 4. Small number of global variables, if any. Most programs need a very small number of global variables, if any.
97 (If you have a global variable named temp, think again.)
98 5. The return values from all system calls and function calls listed in the assignment specification
99 should be checked and all values should be dealt with appropriately.
3
100 6.3 Detailed Test Plan
101 The detailed test plan for the code submission is as follows.
Components Weight
Make file 5
diskinfo 15
disklist 20
diskget 25
diskput 30
Readme 5
Total Weight 100
102
103 7 Warning
104 1. You are required to use C. Any other language is not acceptable.
105 2. Your code should output the required information specified in Parts I, II, III, and IV. Failing to do so will
106 result in the deduction of scores.
107 3. You should use the server linux.csc.uvic.ca to test your work.
108 8 Plagiarism
109 This assignment is to be done individually. You are encouraged to discuss the design of the solution and the FAT 12
110 specification with your classmates, but each student must implement their own assignment.

