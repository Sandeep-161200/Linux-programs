#MEMORY MANAGEMENT
## Write a C program to demonstrate dynamic memory allocation using malloc(). 
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct class
{
        int rollno;
        char name[10];
        float marks;
};
void main()
{
        struct class *ptr;
        ptr=malloc(sizeof(struct class));
        ptr->rollno=1;
        strcpy(ptr->name,"sandeep");
        ptr->marks=96.8;
        printf("%d\n",ptr->rollno);
        printf("%s\n",ptr->name);
        printf("%f\n",ptr->marks);
        printf("%d\n",sizeof(struct class));
}
```
## Implement a C program to allocate memory for an array dynamically using calloc().
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct class
{
        int rollno;
        char name[10];
        float marks;
};
void main()
{
        struct class *ptr;
        int i;
        ptr=calloc(2,sizeof(struct class));
        for(i=0;i<2;i++)
        {
                scanf("%d",&ptr[i].rollno);
                scanf("%s",ptr[i].name);
                scanf("%f",&ptr[i].marks);
        }
        for(i=0;i<2;i++)
        {
                printf("%d\t%s\t%f\n",ptr[i].rollno,ptr[i].name,ptr[i].marks);
        }
}
```
## Write a C program to resize dynamically allocated memory using realloc().
```c
#include<stdio.h>
#include<stdlib.h>
void main()
{
        int *arr;
        int m,n,i;
        printf("enter the number of elements:\n");
        scanf("%d",&n);
        arr=malloc(n*sizeof(int));
        for(i=0;i<n;i++)
        {
                scanf("%d",&arr[i]);
        }
        for(i=0;i<n;i++)
        {
                printf("%d\t",arr[i]);
        }
        printf("\n");
        printf("enter new size of array:\n");
        scanf("%d",&m);
        arr=realloc(arr,m*sizeof(int));
        for(i=0;i<m;i++)
        {
                scanf("%d",&arr[i]);
        }
        for(i=0;i<m;i++)
        {
                printf("%d\t",arr[i]);
        }
        printf("\n");
}
```
##  Develop a program in C to allocate memory for a linked list node dynamically.
```c
#include<stdio.h>
#include<stdlib.h>
struct node
{
        int data;
        struct node *nxt;
};
struct node *phead=NULL;
void add_node_to_tail(int x)
{
        struct node *pnew,*ptrav;
        pnew=malloc(sizeof(struct node));
        if(pnew==NULL)
        {
                printf("memory allocation failed\n");
                return;
        }
        pnew->data=x;
        pnew->nxt=NULL;
        if(phead==NULL)
        {
                phead=pnew;
        }
        else
        {
                ptrav=phead;
                while(ptrav->nxt!=NULL)
                {
                        ptrav=ptrav->nxt;
                }
                ptrav->nxt=pnew;
        }
}
void display()
{
        struct node *ptrav;
        if(phead==NULL)
        {
                printf("list is empty\n");
                return;
        }
        ptrav=phead;
        while(ptrav!=NULL)
        {
                printf("%d->",ptrav->data);
                ptrav=ptrav->nxt;
        }
        printf("NULL");
        printf("\n");
}
void main()
{
        add_node_to_tail(10);
        add_node_to_tail(20);
        add_node_to_tail(30);
        add_node_to_tail(40);
        add_node_to_tail(50);
        add_node_to_tail(60);
        display();
}
```
## Implement a C program to simulate memory allocation using the first-fit algorithm. 
```c
#include<stdio.h>
#define MAX_BLOCKS 5
#define MAX_PROCESS 4
void firstfit(int blocksize[],int m,int processize[],int n)
{
        int allocation[n];
        int i,j;
        for(int i=0;i<n;i++)
        {
                allocation[n]=-1;
        }
        for(int i=0;i<n;i++)
        {
                for(j=0;j<m;j++)
                {
                        if(blocksize[j]>=processize[i])
                        {
                                allocation[i]=j;
                                blocksize[j]-=processize[i];
                                break;
                        }
                }
        }
        printf("process no process.size block.no\n");
        for(i=0;i<n;i++)
        {
                printf("%d\t%d\t%d\t",i,processize[i],allocation[i]);
                printf("\n");
        }
}
void main()
{
        int blocksize[MAX_BLOCKS]={200,300,400,500};
        int processize[MAX_PROCESS]={250,350,150,450};
        firstfit(blocksize,MAX_BLOCKS,processize,MAX_PROCESS);
}
```
## Write a C program to simulate memory allocation using the best-fit algorithm. 
```c
#include<stdio.h>
#define MAX_BLOCKS 5
#define MAX_PROCESSES 4
void bestfit(int blocksize[],int m,int processize[],int n)
{
        int allocation[n],i,j;
        for(i=0;i<n;i++)
        {
                allocation[i]=-1;
        }
        for(i=0;i<n;i++)
        {
                allocation[i]=-1;
        }
        for(i=0;i<n;i++)

        {
                int best=-1;
                for(j=0;j<m;j++)
                {
                        if(blocksize[j]>=processize[i])
                        {
                                if(best==-1||blocksize[j]<blocksize[best])
                                {
                                        best=j;
                                }
                        }
                }
                if(best!=-1)
                {
                        allocation[i]=best;
                        blocksize[best]-=processize[i];
                }

        }
        printf("process no process.size block no\n");
        for(i=0;i<n;i++)
        {
                printf("%d\t%d\t%d\n",i+1,processize[i],allocation[i]);
        }
}
void main()
{
        int blocksize[MAX_BLOCKS]={100,500,200,300,600};
        int processize[MAX_PROCESSES]={199,599,50,250};
        bestfit(blocksize,MAX_BLOCKS,processize,MAX_PROCESSES);
}
```
## Develop a C program to simulate memory allocation using the worst-fit algorithm.
```c
#include<stdio.h>
#define MAX_BLOCKS 5
#define MAX_PROCESSES 4
void worstfit(int blocksize[],int m,int processize[],int n)
{
        int allocation[n],i,j;
        for(i=0;i<n;i++)
        {
                allocation[i]=-1;
        }
        for(i=0;i<n;i++)
        {
                int worst=-1;
                for(j=0;j<m;j++)
                {
                        if(blocksize[j]>=processize[i])
                        {
                                if(worst==-1||blocksize[j]>blocksize[worst])
                                {
                                        worst=j;
                                }
                        }
                }
                if(worst!=-1)
                {
                        allocation[i]=worst;
                        blocksize[worst]-=processize[i];
                }
        }
        printf("process.no process.size block.no\n");
        for(i=0;i<n;i++)
        {
                printf("%d\t%d\t%d\n",i,processize[i],allocation[i]);
        }
}
void main()
{
        int blocksize[MAX_BLOCKS]={100,500,600,200,400};
        int processize[MAX_PROCESSES]={250,100,50,220};
        worstfit(blocksize,MAX_BLOCKS,processize,MAX_PROCESSES);
}
```
## Implement a C program to simulate memory allocation using the next-fit algorithm. 
```c
#include<stdio.h>
#define MAX_BLOCKS 5
#define MAX_PROCESSES 4
void nextfit(int blocksize[],int m,int processize[],int n)
{
        int allocation[n];
        int last=0;
        int i,j;
        for(i=0;i<n;i++)
        {
                allocation[i]=-1;
        }
        for(i=0;i<n;i++)
        {
                int count=0;
                j=last;
                while(count<m)
                {
                        if(blocksize[j]>=processize[i])
                        {
                                allocation[i]=j;
                                blocksize[j]-=processize[i];
                                last=j;
                                break;
                        }
                        j=(j+1)%m;
                        count++;
                }
        }
        printf("process.no process.size block.no\n");
        for(i=0;i<n;i++)
        {
                printf("%d\t%d\t%d\n",i,processize[i],allocation[i]);
        }
}
void main()
{
        int blocksize[MAX_BLOCKS]={100,500,600,200,400};
        int processize[MAX_PROCESSES]={250,100,50,220};
        nextfit(blocksize,MAX_BLOCKS,processize,MAX_PROCESSES);
}
```
## Write a C program to demonstrate memory mapping using mmap().
```c
#include<stdlib.h>
#include<unistd.h>
#include<sys/mman.h>
#include<string.h>
#include<fcntl.h>
void main()
{
        char *filename="mmap.txt";
        char *msg="hello from mmap\n";
        int length=1024;
        int fd=open(filename,O_RDWR|O_CREAT,0666);
        if(fd<0)
        {
                printf("failed to open the file\n");
                return;
        }
        ftruncate(fd,length);
        char *data=mmap(NULL,length,PROT_READ|PROT_WRITE,MAP_SHARED,fd,0);
        if(data==MAP_FAILED)
        {
                printf("mmap failed\n");
                close(fd);
                return;
        }
        strcpy(data,msg);
        munmap(data,length);
        close(fd);
        printf("message written to %s using mmap\n",filename);
}
```
## Implement a C program to read from and write to a memory-mapped file.
```c
#include<stdio.h>
#include<stdlib.h>
#include<fcntl.h>
#include<unistd.h>
#include<sys/mman.h>
#include<string.h>
void main()
{
        int fd;
        char *file="mmap_rw.txt";
        int length=1024;
        char *mapped_mem;
        char *msg="this is a message written via mmap\n";
        fd=open(file,O_RDWR|O_CREAT,0666);
        if(fd<0)
        {
                printf("failed to open the file\n");
                return;
        }
        ftruncate(fd,length);
        mapped_mem=mmap(NULL,length,PROT_READ|PROT_WRITE,MAP_SHARED,fd,0);
        strcpy(mapped_mem,msg);
        printf("written to memory mapped file:%s",msg);
        printf("read back from memory mapped file:%s",mapped_mem);
        close(fd);
}
```
## Develop a C program to demonstrate shared memory usage using shmget() and shmat().
```c
#include<stdio.h>
#include<sys/ipc.h>
#include<sys/shm.h>
#include<sys/types.h>
#define SHM_KEY 25223
void main()
{
        int shmid;
        char *shmptr=NULL;
        shmid=shmget(SHM_KEY,512,IPC_CREAT/0660);
        shmptr=shmat(shmid,NULL,0);
        printf("waiting for message from client\n");
        printf("message received successfully\n");
}
```
## Write a C program to create a shared memory segment and synchronize access using semaphores.
```c
#include<stdio.h>
#include<sys/ipc.h>
#include<sys/shm.h>
#include<sys/sem.h>
#include<sys/types.h>

#define SHM_KEY 25532
#define SEM_KEY 20050

void main()
{
        int shmid,semid;
        char *shmptr=NULL;
        struct sembuf smop;
        shmid=shmget(SHM_KEY,512,IPC_CREAT|0666);
        semid=semget(SEM_KEY,2,IPC_CREAT|0666);
        shmptr=shmat(shmid,NULL,0);
        semctl(semid,0,SETVAL,0);
        semctl(semid,1,SETVAL,0);
        smop.sem_num=0;
        smop.sem_op=-1;
        smop.sem_flg=0;
        printf("waiting for message from client\n");
        semop(semid,&smop,1);
        printf("received:%s\n",shmptr);
}
```
