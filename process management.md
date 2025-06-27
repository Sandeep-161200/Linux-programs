#PROCESS MANAGEMENT
## Write a C program to demonstrate the use of fork() system call.
```c
#include<stdio.h>
#include<sys/types.h>
#include<unistd.h>
void main()
{
        int pid;
        pid=fork();
        if(pid==0)
        {
                        printf("this is child process\n");
        }
        else
        {
                        printf("this is parent process\n");
        }
}
```
## Write a C program to illustrate the use of the execvp() function.
```c
#include<stdio.h>
void main()
{
        char *args[]={"ls","-l",NULL};
        execvp("ls",args);
}
```
## Write a program in C to create a child process using fork() and print its PID. 
```c
#include<stdio.h>
#include<unistd.h>
void main()
{
        int pid;
        pid=fork();
        if(pid ==0)
        {
                printf("child process\n");
                printf("PID=%d\n",getpid());
                printf("PPID=%d\n",getppid());
        }
        else
        {
                printf("parent process\n");
                printf("PID=%d\n",getpid());
                printf("PPID=%d\n",getppid());
        }
}
```
## Write a C program to create multiple child processes using fork() and display their 
PIDs. 
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
void main()
{
        int pid;
        int i;
        for(i=0;i<5;i++)
        {
                pid=fork();
                if(pid==0)
                {
                        printf("%d.child process\t%d\n",i,getpid());
                        exit(0);
                }
        }
        sleep(1);
        printf("%d.parent process\t%d\n",i,getpid());

}
```
## Write a program in C to create a zombie process 
```c
#include<stdio.h>
#include<stdlib.h>
#include<sys/types.h>
#include<unistd.h>
void main()
{
        int pid;
        pid=fork();
        if(pid==0)
        {
                printf("this is child process\n");
                printf("exiting...\n");
                exit(0);
        }
        else
        {
                sleep(1);
                printf("this is parent process\n");
                printf("child process will become zombie process for 30 seconds\n");
                sleep(20);
                printf("exiting parent process\n");
        }
}
```
## Write a C program to demonstrate the use of the waitpid() function for process 
synchronization. 
```c
#include<stdio.h>
#include<sys/wait.h>
#include<stdlib.h>
#include<unistd.h>
void main()
{
        int pid,status;
        pid=fork();
        if(pid==0)
        {
                printf("this is child process\n");
                printf("exiting...\n");
                exit(5);
        }
        else
        {
                sleep(1);
                printf("waiting for child process to terminate\n");
                waitpid(pid,&status,0);
                if(WIFEXITED(status))
                {
                        printf("child exited with status %d\n",WIFEXITED(status));
                }
                else
                {
                        printf("child exited not normally\n");
                }
        }
}
```
## Write a program in C to create a daemon process.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<fcntl.h>
#include<sys/types.h>
#include<sys/stat.h>
void main()
{
        int pid=fork();
        if(pid=0)
        {
                exit(0);
        }
        else
        {
                exit(1);
        }
        if (setsid() < 0)
        exit(EXIT_FAILURE);
        umask(0);
        close(STDIN_FILENO);
        close(STDOUT_FILENO);
        close(STDERR_FILENO);
        while (1)
        {
                int fd = open("/tmp/daemon_log.txt", O_WRONLY | O_CREAT | O_APPEND, 0644);
                if (fd >= 0)
                {
                        dprintf(fd, "Daemon is running...\n");
                        close(fd);
                }
        sleep(5);
        }
}
```
## Write a C program to demonstrate the use of the system() function for executing shell 
commands.
```c
#include<stdio.h>
#include<stdlib.h>
void main()
{
        system("ls -l");
}
```
## Write a C program to create a process using fork() and pass arguments to the child 
process.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<sys/wait.h>
void child_process(int a,int b)
{
        int c=a+b;
        printf("%d\n",c);
}
void main()
{
        int pid;
        pid=fork();
        if(pid==0)
        {
                child_process(4,5);
        }
        else
        {
                wait(NULL);
                printf("this is parent process\n");
        }
}
```
## Write a program in C to demonstrate process synchronization using semaphores.
```c
#include <stdlib.h>


union semun
{
    int val;
};

int main()
{
    key_t key = ftok("semfile", 1);
    int semid = semget(key, 1, 0666 | IPC_CREAT);

    union semun u;
    u.val = 1;
    semctl(semid, 0, SETVAL, u);

    pid_t pid = fork();

    if (pid == 0)
    {
        struct sembuf p = {0, -1, 0};
        semop(semid, &p, 1);

        printf("Child is in critical section\n");
        sleep(2);
        printf("Child is leaving critical section\n");

        struct sembuf v = {0, 1, 0};
        semop(semid, &v, 1);

        exit(0);
    }
    else
    {

        struct sembuf p = {0, -1, 0};
        semop(semid, &p, 1);
        printf("Parent is in critical section\n");
        sleep(2);
        printf("Parent is leaving critical section\n");
        struct sembuf v = {0, 1, 0};
        semop(semid, &v, 1);
        wait(NULL);
        semctl(semid, 0, IPC_RMID);
    }

    return 0;
}
```
## Write a C program to demonstrate the use of the execvpe() function.
```c
#define _GNU_SOURCE
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
void main()
{
        char *args[]={"ls","-l","/tmp",NULL};
        char *envp[]={"myvar=san","PATH=/bin:/usr/bin",NULL};
        printf("calling excevpe to run ls -l/tmp\n");
        execvpe("ls",args,envp);
}
```
## Write a C program to create a process group and change its process group ID (PGID).
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
void main()
{
        int pid,pgid;
        pid=fork();
        if(pid==0)
        {
                printf("child: pid=%d\t ppid=%d\t gpid=%d\n",getpid(),getppid(),getpgid(0));
                setpgid(0,0);
                printf("child:changed pgid to its pid:%d\n",getpgid(0));
                sleep(2);
                printf("child:final pgid = %d\n",getpgid(0));
                exit(0);
        }
        else
        {
                sleep(1);
                printf("parent pid=%d\t,pgid=%d\n",getpid(),getpgid(0));
                wait(NULL);
        }
}
```
## Write a program in C to demonstrate inter-process communication (IPC) using shared 
memory.
```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/wait.h>
#include <sys/types.h>
#include <unistd.h>
#include <string.h>
#define SHM_SIZE 1024
void main()
{
        key_t key=ftok("shmfile",65);
        int shmid=shmget(key,SHM_SIZE,0666|IPC_CREAT);
        int pid=fork();
        if(pid==0)
        {
                char *shared_memory=shmat(shmid,NULL,0);
                printf("child:read from shared memory:%s\n",shared_memory);
                shmdt(shared_memory);
                exit(0);
        }
        else
        {
                char *shared_memory=shmat(shmid,NULL,0);
                char msg[]="hello from parent process via shared memory";
                strncpy(shared_memory,msg,SHM_SIZE);
                shmdt(shared_memory);
                wait(NULL);
                shmctl(shmid,IPC_RMID,NULL);
        }
}
```
## Write a C program to create a child process using vfork()
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/wait.h>
void main()
{
        int pid=vfork();
        if(pid==0)
        {
                execlp("ls","ls","-l",NULL);
                _exit(1);
        }
        else
        {
                printf("vfork returned ,child PID=%d\n",pid);
                wait(NULL);
        }
}
```
## Write a C program to create a pipeline between two processes using the pipe() system 
call.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/wait.h>
#include<sys/types.h>
#include<sys/ipc.h>
void main()
{
        int fds[2],pid,status;
        pipe(fds);
        pid=fork();
        if(pid==0)
        {
                char buf[20]={0};
                close(fds[1]);
                printf("waiting for msg from parent\n");
                read(fds[0],buf,20);
                printf("received message:%s\n",buf);
        }
        else
        {
                sleep(1);
                char buf[20];
                close(fds[0]);
                printf("enter message for child:\n");
                scanf("%s",buf);
                write(fds[1],buf,strlen(buf));
        }
        wait(&status);
}
```
## Write a program in C to demonstrate the use of the nice() system call for adjusting 
process priority
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/time.h>
#include<sys/resource.h>
void main()
{
        int priority;
        priority=getpriority(PRIO_PROCESS,0);
        printf("initial priority :%d\n",priority);
        int new_nice=nice(5);
        priority=getpriority(PRIO_PROCESS,0);
        printf("new priority after new_nice : %d\n",priority);
}
```
## Write a C program to demonstrate the use of the clone() system call to create a thread.
```c
#define _GNU_SOURCE
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sched.h>
#include<signal.h>
#include<sys/wait.h>

#define STACK_SIZE 1024*64

int thread(void *args)
{
        int i;
        for(i=0;i<5;i++)
        {
                printf("%d\n",i+1);
                sleep(1);
        }
        return 0;
}
int main()
{
        char *ptr=malloc(STACK_SIZE);
        int pid=clone(thread, ptr+STACK_SIZE, CLONE_VM | CLONE_FS | CLONE_FILES | CLONE_SIGHAND | CLONE_THREAD,NULL);
        for(int i=0;i<5;i++)
        {
                printf("from main thread : %d\n",i+1);
                sleep(1);
        }
        free(ptr);
        return 0;
}
```
## Write a C program to create a child process using fork() and communicate between 
parent and child using pipes.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/wait.h>
#include<sys/types.h>
#include<sys/ipc.h>
void main()
{
        int fd1[2],fd2[2],pid,status;
        pipe(fd1);
        pipe(fd2);
        pid=fork();
        if(pid==0)
        {
                char buf[20]={0};
                close(fd1[1]);
                printf("waiting for msg from parent\n");
                read(fd1[0],buf,20);
                printf("received message:%s\n",buf);
                close(fd2[0]);
                printf("reply to parent:\n");
                scanf("%s",buf);
                write(fd2[1],buf,strlen(buf));
                printf("message sent successfully\n");
        }
        else
        {
                sleep(1);
                char buf[20];
                close(fd1[0]);
                printf("enter message for child:\n");
                scanf("%s",buf);
                write(fd1[1],buf,strlen(buf));
                close(fd2[1]);
                printf("waiting for reply\n");
                read(fd2[0],buf,20);
                printf("message received from child: %s\n",buf);
        }
        wait(&status);
}
```
## Write a C program to demonstrate process synchronization using the fork() and wait() 
system calls.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/wait.h>
void main()
{
        int pid,status;
        pid=fork();
        if(pid==0)
        {
                printf("child process is exectuing\n");
                sleep(3);
                printf("child process finished its execution\n");

        }
        else
        {
                printf("parent process waiting the child process to complete\n");
                wait(&status);
                printf("child process finished .back to parent process\n");
        }
}
```
## Write a C program to create a process using fork() and change its scheduling policy 
using sched_setscheduler().
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sched.h>
#include<sys/wait.h>
void main()
{
        int pid;
        struct sched_param param;
        pid=fork();
        if(pid==0)
        {
                param.sched_priority=10;
                sched_setscheduler(0,SCHED_FIFO,&param);
                printf("child process is running with SCHD_FIFO\n");
                for(int i=0;i<5;i++)
                {
                        printf("%d\n",i+1);
                        sleep(1);
                }
        }
        else
        {
                wait(NULL);
                printf("child process finished\n");
        }
}
```
## Write a C program to create a child process using fork() and demonstrate inter-process 
communication (IPC) using shared memory.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/types.h>
#include<sys/ipc.h>
#include<sys/shm.h>
#include<sys/wait.h>
void main()
{
        key_t key=ftok("shmfile",65);
        int shmid=shmget(key,512,0666|IPC_CREAT);
        int pid=fork();
        if(pid==0)
        {
                char *data=shmat(shmid,NULL,0);
                strcpy(data,"hello from shared memory(child process)\n");
                printf("child:message written to shared memory\n");
                shmdt(data);
        }
        else
        {
                wait(NULL);
                char *data=shmat(shmid,NULL,0);
                printf("parent:message received from shared memory:\n%s\n",data);
                shmdt(data);
        }
}
```
## Write a C program to demonstrate the use of the prctl() system call to change process 
attributes.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/prctl.h>
#include<signal.h>
void main()
{
        prctl(PR_SET_NAME,"myprocess");
        char name[10];
        prctl(PR_GET_NAME,name);
        printf("process name set to:%s\n",name);
        prctl(PR_SET_PDEATHSIG, SIGTERM);
        printf("if parent dies SIGTERM will be sent\n");
        printf("process is running \n");
}
```
## Write a C program to create a child process using fork() and demonstrate process 
synchronization using semaphores
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/sem.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<sys/ipc.h>
void main()
{
        key_t key=ftok("semfile",65);
        int semid=semget(key,1,0666|IPC_CREAT);
        semctl(semid,0,SETVAL,1);
        int pid=fork();
        if(pid==0)
        {
                struct sembuf sb1={0,-1,0};
                semop(semid,&sb1,1);
                printf("child in critical section\n");
                sleep(2);
                printf("child is leaving critical section\n");
                struct sembuf sb2={0,1,0};
                semop(semid,&sb2,1);
        }
        else
        {
                struct sembuf sb1={0,-1,0};
                semop(semid,&sb1,1);
                printf("parent is in critical section\n");
                sleep(2);
                printf("parent is leaving critical section\n");
                struct sembuf sb2={0,1,0};
                semop(semid,&sb2,1);
                wait(NULL);
        }
}
```
## Write a C program to create a child process using fork() and demonstrate process 
communication using message queues.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/msg.h>
#include<sys/types.h>
#include<string.h>
#include<sys/wait.h>
struct msg_buffer
{
        long msg_type;
        char msg_txt[100];
};
void main()
{
        key_t key=ftok("msgfile",65);
        int msgid;
        msgid=msgget(key,0666|IPC_CREAT);
        int pid=fork();
        if(pid==0)
        {
                struct msg_buffer message;
                msgrcv(msgid,&message,sizeof(message.msg_txt),1,0);
                printf("child received message:%s\n",message.msg_txt);
        }
        else
        {
                struct msg_buffer message;
                message.msg_type=1;
                strcpy(message.msg_txt,"hello from parent process");
                msgsnd(msgid,&message,sizeof(message.msg_txt),0);
                wait(NULL);
        }
}
```
## Write a C program to create a child process using fork() and demonstrate process 
communication using named pipes (FIFOs).
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <string.h>
#include <sys/wait.h>

#define FIFO_NAME "fifo"
void main()
{
        int ret;
        ret=mkfifo(FIFO_NAME,0666);
        if(ret<0)
        {
                printf("failed to create fifo\n");
        }
        int pid;
        pid=fork();
        if(pid==0)
        {
                char buffer[100];
                int fd=open(FIFO_NAME,O_RDONLY);
                int ret=read(fd,buffer,sizeof(buffer));
                buffer[ret]='\0';
                printf("child received:%s\n",buffer);
                close(fd);
        }
        else
        {
                int fd=open(FIFO_NAME,O_WRONLY);
                char *msg="hello from parent";
                write(fd,msg,strlen(msg));
                close(fd);
                wait(NULL);
                unlink(FIFO_NAME);
        }
}
```
## Write a C program to create a child process using fork() and demonstrate 
process communication using shared memory and semaphores
```c 
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/sem.h>
#include <sys/wait.h>

#define SHM_KEY 1234
#define SEM_KEY 5678
#define SHM_SIZE 1024

union semun {
        int val;
        };

int main()
{
        int shmid, semid;
        char *shared_data;
        shmid = shmget(SHM_KEY, SHM_SIZE, IPC_CREAT | 0666);
        shared_data = (char *)shmat(shmid, NULL, 0);
        semid = semget(SEM_KEY, 1, IPC_CREAT | 0666);
        union semun arg;
        arg.val = 0;
        semctl(semid, 0, SETVAL, arg);
        pid_t pid = fork();
        if (pid == 0)
        {
                struct sembuf sb = {0, -1, 0};
                semop(semid, &sb, 1);
                printf("Child: Read from shared memory: %s\n", shared_data);
                shmdt(shared_data);
                exit(0);
        }
        else
        {
                strcpy(shared_data, "Hello from parent");
                struct sembuf sb = {0, 1, 0};
                semop(semid, &sb, 1);
                wait(NULL);
        }
}
```
