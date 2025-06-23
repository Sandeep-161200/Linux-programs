## Write a C program to create a new text file and write "Hello, World!" to it?
```c
#include<stdio.h>
#include<string.h>
#include<fcntl.h>
void main()
{
        int fd,ret;
        char buf[]="hello world!";
        fd=open("file.txt",O_CREAT|O_WRONLY,0660);
        if(fd<0)
        {
                printf("failed to open a file\n");
                return;
        }
        ret=write(fd,buf,strlen(buf));
        if(ret<0)
        {
                printf("failed to write\n");
                return;
        }
        close(fd);
}
```
## Develop a C program to open an existing text file and display its contents?
```c
#include<stdio.h>
#include<fcntl.h>
#include<string.h>
#include<unistd.h>
void main()
{
        int fd;
        char buf[512];
        fd=open("file1.c",O_RDONLY);
        if(fd<0)
        {
                printf("failed to open the file\n");
                return;
        }

        int ret;
        ret=read(fd,buf,sizeof(buf));
        if(ret<0)
        {
                printf("failed to read\n");
                return;
        }
        buf[ret]='\0';
        printf("%s\n",buf);
        close(fd);
}

3. Implement a C program to create a new directory named "Test" in the current 
directory?

#include<stdio.h>
#include<sys/stat.h>
#include<sys/types.h>
void main()
{
        const char *dirname="test";
        if(mkdir(dirname,0755)==0)
        {
                printf("directory %s is created successfully",dirname);

        }
        else
        {
                printf("error in creating the directory\n");
        }
}

4. Write a C program to check if a file named "sample.txt" exists in the current directory?

#include<stdio.h>
#include<unistd.h>
void main()
{
        char *name="sample.txt";
        if(access(name,F_OK)==0)
        {
                printf("file is existed in current directory\n");
        }
        else
        {
                printf("file is not existed\n");
        }
}

5. Develop a C program to rename a file from "oldname.txt" to "newname.txt"?

#include<stdio.h>
void main()
{
        char *oldname="file.txt";
        char *newname="myfile.txt";
        if(rename(oldname,newname)==0)
        {
                printf("file name changed from %s to %s\n",oldname,newname);
        }
        else
        {
                printf("failed to change the name of file\n");
        }
}

6. Implement a C program to delete a file named "delete_me.txt"? 

#include<stdio.h>
void main()
{
        char *name="delete.txt";
        if(remove(name)==0)
        {
                printf("%s file is deleted successfully\n",name);
        }
        else
        {
                printf("failed to delete the file\n");
        }

}

7. Write a C program to copy the contents of one file to another? 

#include<stdio.h>
#include<fcntl.h>
#include<unistd.h>
#include<stdlib.h>
void main()
{
        int fd1,fd2;
        char buf[1024];
        int bytesread,byteswritten;
        const char *src="myfile.txt";
        const char *dest="ourfile.txt";
        fd1=open(src,O_RDONLY);
        if(fd1<0)
        {
                printf("failed to open source file\n");
                return;
        }
        fd2=open(dest,O_WRONLY|O_CREAT|O_TRUNC,0660);
        if(fd2<0)
        {
                printf("failed to open destination file\n");
                return;
        }
        while((bytesread=read(fd1,buf,sizeof(buf)))>0)
        {
                byteswritten=write(fd2,buf,bytesread);
                close(fd1);
                close(fd2);   
        }

        close(fd1);
        close(fd2);
        printf("file copied\n");
}

8. Develop a C program to move a file from one directory to another?

#include<stdio.h>
void main()
{
        const char *src="send/text.c";
        const char *dest="receive/text.c";
        if(rename(dest,src)==0)
        {
                printf("file moved successfully\n");
        }
        else
        {
                printf("failed to move\n");
        }
}

9. Implement a C program to list all files in the current directory?

#include<stdio.h>
#include<unistd.h>
void main()
{
        execl ("/bin/ls","ls",NULL);
}

10. Write a C program to get the size of a file named "file.txt"? 

#include<stdio.h>
#include<sys/stat.h>
void main()
{
        struct stat filestat;
        const char *file="myfile.txt";
        stat(file,&filestat);
        printf("the size of %s is %d bytes",file,filestat.st_size);
}

11. Develop a C program to check if a directory named "Test" exists in the current 
directory? 

#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
void main()
{
        struct stat statbuf;
        const char *file="test";
        if(stat(file,&statbuf)==0)
        {
                if(S_ISDIR(statbuf.st_mode))
                {
                        printf("%s directory exists\n",file);
                }
                else
                {
                        printf("%s exists but not as a directory\n",file);
                }
        }
        else
        {
                printf("%s directory not exists\n",file);
        }
}

12. Implement a C program to create a new directory named "Backup" in the parent 
directory? 

#include<stdio.h>
#include<sys/stat.h>
#include<sys/types.h>
void main()
{
        const char *dirpath="../backup";
        if(mkdir(dirpath,0755)==0)
        {
                printf("%s directory is created\n",dirpath);
        }
        else
        {
                printf("failed to create a directory\n");
        }

}

13. Write a C program to recursively list all files and directories in a given directory?

#include<stdio.h>
#include<unistd.h>
void main(int argc,char *argv[])
{
        const char *path;
        if(argc<2)
        {
                path=".";
        }
        else
        {
                path=argv[1];
        }
        execlp("ls","ls","-R",path,NULL);
}

14. Develop a C program to delete all files in a directory named "Temp"? 

#include<stdio.h>
#include<unistd.h>
void main()
{
        execlp("rm","rm","-rf","receive",NULL);
}

15. Implement a C program to count the number of lines in a file named "data.txt"?

#include<stdio.h>
#include<fcntl.h>
#include<unistd.h>
void main()
{
        int fd,linecount=0;
        ssize_t bytesread;
        char buf[1024];
        fd=open("copy.c",O_RDONLY);
        if(fd<0)
        {
                printf("failed to open the file\n");
                return;
        }
        while((bytesread=read(fd,buf,sizeof(buf)))>0)
        {
                for(ssize_t i=0;i<bytesread;i++)
                {
                        if(buf[i]=='\n')
                        {
                                linecount++;
                        }
                }
        }
        close(fd);
        printf("the number of lines are %d\n",linecount);
}

16. Write a C program to append "Goodbye!" to the end of an existing file named 
"message.txt"? 

#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
void main()
{
        int fd;
        char buf[]="good bye";
        fd=open("file.txt",O_APPEND|O_WRONLY);
        if(fd<0)
        {
                printf("failed to open the file\n");
                return;
        }
        ssize_t ret=write(fd,buf,strlen(buf));
        if(ret<0)
        {
                printf("failed to write\n");
                return;
        }
        close(fd);
        printf("message appended successfully\n");
}

17. Implement a C program to change the permissions of a file named "file.txt" to read
only? 

#include<stdio.h>
#include<sys/stat.h>
void main()
{
        const char *name="file.txt";
       if(chmod(name,0444)==0)
       {
               printf("permissions changed to read only to %s\n",name);
       }
       else
       {
               printf("failed to change the permissions\n");
       }
}

18. Write a C program to change the ownership of a file named "file.txt" to the user 
"user1"? 

#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<pwd.h>
#include<sys/types.h>
void main()
{
        const char *filename="file.txt";
        const char *username="user1";
        struct passwd *pw=getpwnam(username);
        if(pw==NULL)
        {
                printf("%s user not found\n",username);
                return;
        }
        uid_t uid=pw->pw_uid;
        gid_t gid=pw->pw_gid;
        chown(filename,uid,-1);
        printf("owner changed from %s to %s\n",filename,username);
}

19. Develop a C program to get the last modified timestamp of a file named "file.txt"? 

#include<stdio.h>
#include<time.h>
#include<sys/stat.h>
void main()
{
        const char *filename="file.txt";
        struct stat filestat;
        stat(filename,&filestat);
        printf("last modified of %s:%s\n",filename,ctime(&filestat.st_mtime));
}

20. Implement a C program to create a temporary file and write some data to it? 

#include<stdio.h>
#include<fcntl.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
void main()
{
        char template[]="/tmp/tempfileXXXXXX";
        int fd=mkstemp(template);
        if(fd<0)
        {
                printf("failed to create temporary file\n");
                return;
        }
        printf("temporary file is created:%s\n",template);
        const char *data="this is sample data written to temporary file";
        if(write(fd,data,strlen(data))<0)
        {
                printf("write failed\n");
                close(fd);
                return;
        }
        printf("data written to temporary file successfully\n");
        close(fd);
}

