#THREADS
## Write a C program to create a thread that prints "Hello, World!"? 
```c
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *display(void *args)
{
        for(int i=0;i<5;i++)
        {
                printf("hello world!\n");
                sleep(1);
        }
}
void main()
{
        pthread_t t2;
        pthread_create(&t1,NULL,display,NULL);
        for(int i=0;i<5;i++)
        {
                printf("hello from main thread\n");
                sleep(1);
        }
        pthread_join(t1,NULL);
}
```
## Modify the above program to create multiple threads, each printing its own message?
```c
#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
void *display1(void *args)
{
        for(int i=0;i<5;i++)
        {
                printf("hello from thread1\n");
                sleep(1);
        }

}
void *display2(void *args)
{
        for(int i=0;i<5;i++)
        {
                printf("hello from thread2\n");
                sleep(1);
        }
}
void main()
{
        pthread_t t1,t2;
        pthread_create(&t1,NULL,display1,NULL);
        pthread_create(&t2,NULL,display2,NULL);
        for(int i=0;i<5;i++)
        {
                printf("hello from main thread\n");
                sleep(1);
        }
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
}
```
## Develop a C program to create two threads that print numbers from 1 to 10 concurrently?
```c
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *nums(void *args)
{
        int i;
        for(i=1;i<11;i++)
        {
                printf("from thread 1:%d\n",i);
                sleep(1);
        }
}
void *values(void *args)
{
        int i;
        for(i=1;i<11;i++)
        {
                printf("from thread 2:%d\n",i);
                sleep(1);
        }
}
void main()
{
        pthread_t t1,t2;
        pthread_create(&t1,NULL,nums,NULL);
        pthread_create(&t2,NULL,values,NULL);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
}
```
## Implement a C program to create a thread that calculates the factorial of a given number? 
```c
#include<stdio.h>
#include<pthread.h>
void *fact(void *args)
{
        int n;
        printf("enter a number:\n");
        scanf("%d",&n);
        int Fact=1;
        while(n)
        {
                Fact*=n;
                n--;
        }
        printf("factorial = %d\n",Fact);
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,fact,NULL);
        pthread_join(t1,NULL);
}
```
## Write a C program to create two threads that print their thread IDs? 
```c
#include<stdio.h>
#include<pthread.h>
void *thread_id(void *args)
{
        pthread_t tid=pthread_self();
        printf("threads id:%lu\n",tid);
}
void main()
{
        pthread_t t1,t2;
        pthread_create(&t1,NULL,thread_id,NULL);
        pthread_create(&t2,NULL,thread_id,NULL);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
}
```
## Develop a C program to create a thread that prints the sum of two numbers?
```c
#include<stdio.h>
#include<pthread.h>
void *sum(void *args)
{
        int a,b,sum;
        printf("enter two numbers\n");
        scanf("%d%d",&a,&b);
        sum=a+b;
        printf("sum=%d\n",sum);
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,sum,NULL);
        for(int i=0;i<5;i++)
        {
                printf("this is main thread\n");
                sleep(1);
        }
        pthread_join(t1,NULL);
}
```
## Implement a C program to create a thread that calculates the square of a number?
```c
#include<stdio.h>
#include<pthread.h>
void *square(void *args)
{
        printf("in thread function\n");
        int n=5;
        int sqr=n*n;
        printf("square=%d\n",sqr);
}
void main()
{
        printf("welocme to main thread\n");
        pthread_t t1;
        pthread_create(&t1,NULL,square,NULL);
        pthread_join(t1,NULL);
        printf("main thread finished\n");
}
```
## Write a C program to create a thread that prints the current date and time? 
```c
#include<stdio.h>
#include<pthread.h>
#include<time.h>
void *tim(void *args)
{
        printf("this is thread function\n");
        time_t now;
        struct tm *local;
        time(&now);
        local=localtime(&now);
        printf("current date and time :%s\n",asctime(local));
}
void main()
{
        printf("this is main thread\n");
        pthread_t t1;
        pthread_create(&t1,NULL,tim,NULL);
        sleep(5);
        printf("main thread finished\n");
        pthread_join(t1,NULL);
}
```
## Develop a C program to create a thread that checks if a number is prime.
```c
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
void *prime(void *args)
{
        printf("this is thread function\n");
        int i=8,j,count=0;
        for(j=1;j<=i;j++)
        {
                if(i%j==0)
                {
                        count++;
                }
        }
        if(count==2)
        {
                printf("%d is a prime number\n",i);
        }
        else
        {
                printf("%d is not a prime number\n",i);
        }

        printf("thread function finished\n");
}
void main()
{
        printf("this is main thread\n");
        pthread_t t1;
        pthread_create(&t1,NULL,prime,NULL);
        sleep(2);
        pthread_join(t1,NULL);
        printf("main thread finished\n");
}
```
## Implement a C program to create a thread that checks if a given string is a palindrome?
```c
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<string.h>
void *polindrome(void *args)
{
        printf("this is thread function\n");
        char str[]="madam";
        int len=strlen(str);
        char str1[len+1];
        int i;
        for(i=0;i<len;i++)
        {
                str1[i]=str[len-i-1];
        }
        str1[len]='\0';
        if(strcmp(str,str1)==0)
        {
                printf("%s is a polindrome\n",str);
        }
        else
        {
                printf("%s is not a polindrome\n",str);
        }
        printf("thread fuction complete\n");
}
void main()
{
        printf("this is main thread\n");
        pthread_t t1;
        pthread_create(&t1,NULL,polindrome,NULL);
        sleep(2);
        pthread_join(t1,NULL);
        printf("main thread completed\n");
}
```
## Write a C program to create a thread that prints "Hello, World!" with thread 
synchronization?
```c
#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;
void *message(void *args)
{
        pthread_mutex_lock(&lock);
        printf("hello from thread function\n");
        pthread_mutex_unlock(&lock);
}
void main()
{
        pthread_t t1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,message,NULL);
        pthread_join(t1,NULL);
        pthread_mutex_destroy(&lock);
}
```
## Develop a C program to create two threads that print their thread IDs and synchronize their 
output?
```c
#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;
void *thread_id(void *args)
{
        pthread_mutex_lock(&lock);
        printf("threads id:%lu\n",pthread_self());
        pthread_mutex_unlock(&lock);
}
void main()
{
        pthread_t t1,t2;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,thread_id,NULL);
        pthread_create(&t2,NULL,thread_id,NULL);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
        pthread_mutex_destroy(&lock);
}
```
## Implement a C program to create a thread that generates random numbers and 
synchronizes access to a shared buffer?
```c
#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>
pthread_mutex_t lock;

void *random_generate(void *args)
{
        pthread_mutex_lock(&lock);
        for(int i=0;i<5;i++)
        {
                printf("Random number: %d\n", rand()%100);
        }
        pthread_mutex_unlock(&lock);
}
void main()
{
        pthread_t t1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,random_generate,NULL);
        pthread_join(t1,NULL);
        pthread_mutex_destroy(&lock);
}
```
## Develop a C program to create a thread that prints numbers from 10 to 1 in descending order 
using mutex locks?
```c
#include<stdio.h>
#include<pthread.h>
pthread_mutex_t lock;
void *desc(void *args)
{
        pthread_mutex_lock(&lock);
        int i;
        for(i=10;i>0;i--)
        {
                printf("%d\n",i);
        }
        pthread_mutex_unlock(&lock);
}
void main()
{
        pthread_t t1;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,desc,NULL);
        pthread_join(t1,NULL);
        pthread_mutex_destroy(&lock);
}
```
## Write a C program to create two threads that increment and decrement a shared variable, 
respectively, using mutex locks?
```c
#include<stdio.h>
#include<pthread.h>
int share_var=0;
pthread_mutex_t lock;
void *incr(void *args)
{
        pthread_mutex_lock(&lock);
        for(int i=0;i<10;i++)
        {
                share_var++;
                printf("%d\n",share_var);
        }
        pthread_mutex_unlock(&lock);
        printf("final value in thread 1:%d\n",share_var);
}
void *decr(void *args)
{
        pthread_mutex_lock(&lock);
        for(int i=0;i<5;i++)
        {
                share_var--;
                printf("%d\n",share_var);
        }
        pthread_mutex_unlock(&lock);
        printf("final value in thread 2 :%d\n",share_var);
}
void main()
{
        pthread_t t1,t2;
        pthread_mutex_init(&lock,NULL);
        pthread_create(&t1,NULL,incr,NULL);
        pthread_create(&t2,NULL,decr,NULL);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
        pthread_mutex_destroy(&lock);
        printf("the final value of variable is %d\n",share_var);
}
```
## Develop a C program to create a thread that prints the multiplication table of a given 
number up to a given limit?
```c
#include<stdio.h>
#include<pthread.h>
void *mul(void *args)
{
        int n,lim,i;
        printf("enter a number\n");
        scanf("%d",&n);
        printf("enter the limit\n");
        scanf("%d",&lim);
        for(i=1;i<=lim;i++)
        {
                printf("%d * %d =%d\n",n,i,n*i);
        }
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,mul,NULL);
        pthread_join(t1,NULL);
}
```
## Implement a C program to create a thread that checks if a given number is divisible by 
another given number?
```c
#include<stdio.h>
#include<pthread.h>
void *div(void *args)
{
        int m,n;
        printf("enter two values\n");
        scanf("%d%d",&m,&n);
        if(m%n==0)
        {
                printf("%d is divisible by %d\n",m,n);
        }
        else
        {
                printf("%d is not divisible by %d\n",m,n);
        }
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,div,NULL);
        pthread_join(t1,NULL);
}
```
## Implement a C program to create a thread that checks if a given number is a perfect 
square? 
```c
#include<stdio.h>
#include<math.h>
#include<pthread.h>
void *perfect(void *args)
{
        int n;
        printf("enter a number\n");
        scanf("%d",&n);
        int root=sqrt(n);
        if(root*root==n)
        {
                printf("%d is a perfect square number\n",n);
        }
        else
        {
                printf("%d is not a perfect square number\n",n);
        }
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,perfect,NULL);
        pthread_join(t1,NULL);
}
```
## Develop a C program to create a thread that prints the English alphabet in uppercase
```c
#include<stdio.h>
#include<pthread.h>
void *alpha(void *args)
{
        int i;
        for(i='A';i<='Z';i++)
        {
                printf("%c\t",i);
        }
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,alpha,NULL);
        pthread_join(t1,NULL);
}
```
## Implement a C program to create a thread that prints the factors of a given number?
```c
#include<stdio.h>
#include<pthread.h>
void *fcat(void *args)
{
        int i,n;
        printf("enter a number\n");
        scanf("%d",&n);
        printf("the factors are:\n");
        for(i=1;i<=n;i++)
        {
                if(n%i==0)
                {
                        printf("%d\t",i);
                }
        }
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,fcat,NULL);
        pthread_join(t1,NULL);
}
```
## Develop a C program to create a thread that calculates the average of a given array of 
floating-point numbers? 
```c
#include<stdio.h>
#include<pthread.h>
void *avg(void *args)
{
        float arr[5];
        int i;
        printf("enter the elements of array\n");
        for(i=0;i<5;i++)
        {
                scanf("%f",&arr[i]);
        }
        float sum=0,aveg;
        for(i=0;i<5;i++)
        {
                sum=sum+arr[i];
        }
        aveg=sum/5;
        printf("%f\n",aveg);
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,avg,NULL);
        pthread_join(t1,NULL);
}
```
## Implement a C program to create a thread that prints the ASCII values of characters in a 
given string?
```c
#include<stdio.h>
#include<string.h>
#include<pthread.h>
void *ascii(void *args)
{
        char str[]="SANDEEP";
        int i;
        for(i=0;i<strlen(str);i++)
        {
                printf("%d\t",str[i]);
        }
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,ascii,NULL);
        pthread_join(t1,NULL);
}
```
## Write a C program to create a thread that finds the maximum element in a given array
```c
#include<stdio.h>
#include<pthread.h>
void *max(void *args)
{
        int arr[]={34,65,1,89,54,10};
        int max=arr[0];
        int i;
        for(i=0;i<6;i++)
        {
                if(arr[i]>max)
                {
                        max=arr[i];
                }
        }
        printf("max element=%d\n",max);
}
void main()
{
        pthread_t t1;
        pthread_create(&t1,NULL,max,NULL);
        pthread_join(t1,NULL);
}
```
## Write a C program to create a thread that prints the even numbers between 1 and 20? 
```c
#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
void *even(void *args)
{
        int i;
        for(i=1;i<=20;i++)
        {
                if(i%2==0)
                {
                        printf("%d\t",i);
                }
        }
}
void *odd(void *args)
{
        int i;
        for(i=1;i<=20;i++)
        {
                if(i%2!=0)
                {
                        printf("%d\t",i);
                }
        }
}
void main()
{
        pthread_t t1,t2;
        pthread_create(&t1,NULL,even,NULL);
        pthread_create(&t2,NULL,odd,NULL);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
}
```




