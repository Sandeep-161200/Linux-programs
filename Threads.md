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
## Develop a C program to create a thread that reads input from the user and synchronizes access to shared resources?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <string.h>

#define SIZE 100

char shared[SIZE];
pthread_mutex_t mutex;

void *input(void *args)
{
    char temp[SIZE];

    pthread_mutex_lock(&mutex);

    printf("Enter a message: ");
    fgets(temp, SIZE, stdin);
    temp[strcspn(temp, "\n")] = 0;

    strncpy(shared, temp, SIZE);

    pthread_mutex_unlock(&mutex);
    return NULL;
}

int main()
{
    pthread_t thread;

    if (pthread_mutex_init(&mutex, NULL) != 0)
    {
        perror("Mutex init failed");
        return 1;
    }

    if (pthread_create(&thread, NULL,input, NULL) != 0)
    {
        perror("Failed to create thread");
        return 1;
    }

    pthread_join(thread, NULL);

    pthread_mutex_lock(&mutex);
    printf("Shared buffer contains: \"%s\"\n", shared);
    pthread_mutex_unlock(&mutex);

    pthread_mutex_destroy(&mutex);
    return 0;
}
```
## Implement a C program to create a thread that prints prime numbers up to a given limit with mutex locks?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <stdbool.h>

pthread_mutex_t mutex;

bool isprime(int num)
{
    if (num <= 1)
    {
            return false;
    }
    for (int i = 2; i * i <= num; i++)
    {
        if (num % i == 0)
        {
            return false;
        }
    }
    return true;
}
void *print_primes(void *arg)
{
    int limit = *(int *)arg;

    for (int i = 2; i <= limit; i++)
    {
        if (isprime(i))
        {
            pthread_mutex_lock(&mutex);
            printf("Prime: %d\n", i);
            pthread_mutex_unlock(&mutex);
        }
    }

    return NULL;
}
int main()
{
    int limit;
    pthread_t thread;

    printf("Enter the upper limit: ");
    scanf("%d", &limit);

    if (pthread_mutex_init(&mutex, NULL) != 0)
    {
        perror("Mutex init failed");
        return 1;
    }
    if (pthread_create(&thread, NULL, print_primes, &limit) != 0)
    {
        perror("Thread creation failed");
        return 1;
    }
    pthread_join(thread, NULL);
    pthread_mutex_destroy(&mutex);
    return 0;
}
```
## Write a C program to create a thread that checks if a given year is a leap year using dynamic programming with mutex locks?
```c
#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

pthread_mutex_t mutex;

void *check_leap_year(void *arg)
{
    int year = *(int*)arg;

    pthread_mutex_lock(&mutex);

    if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0))
    {
        printf("Year %d is a Leap Year.\n", year);
    }
    else
    {
        printf("Year %d is Not a Leap Year.\n", year);
    }

    pthread_mutex_unlock(&mutex);
    return NULL;
}

int main()
{
    int year;
    printf("Enter a year: ");
    scanf("%d", &year);

    pthread_t th;

    pthread_mutex_init(&mutex, NULL);

    pthread_create(&th, NULL, check_leap_year, &year);
    pthread_join(th, NULL);

    pthread_mutex_destroy(&mutex);

    return 0;
}
```
## Write a C program to create a thread that checks if a given string is a palindrome using dynamic programming with mutex locks?
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<pthread.h>

pthread_mutex_t mutex;

void *check_palindrome(void *arg)
{
    char *str = (char *)arg;
    int start = 0;
    int end = strlen(str) - 1;
    int is_palindrome = 1;

    pthread_mutex_lock(&mutex);

    while (start < end)
    {
        if (str[start] != str[end])
        {
            is_palindrome = 0;
            break;
        }
        start++;
        end--;
    }

    if (is_palindrome)
    {
        printf("'%s' is a Palindrome.\n", str);
    }
    else
    {
        printf("'%s' is not a Palindrome.\n", str);
    }

    pthread_mutex_unlock(&mutex);
    return NULL;
}

int main()
{
    char str[100];

    printf("Enter a string: ");
    scanf("%s", str);

    pthread_t th;

    pthread_mutex_init(&mutex, NULL);
    pthread_create(&th, NULL, check_palindrome, str);
    pthread_join(th, NULL);
    pthread_mutex_destroy(&mutex);

    return 0;
}
```
## Implement a C program to create a thread that performs selection sort on an array of integers?
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<pthread.h>

void *check_palindrome(void *arg)
{
    char *str = (char *)arg;
    int start = 0;
    int end = strlen(str) - 1;
    int is_palindrome = 1;

    while(start < end)
    {
        if(str[start] != str[end])
        {
            is_palindrome = 0;
            break;
        }
        start++;
        end--;
    }

    if(is_palindrome)
    {
        printf("The string '%s' is a palindrome.\n", str);
    }
    else
    {
        printf("The string '%s' is not a palindrome.\n", str);
    }
    return NULL;
}

int main()
{
    char str[100];
    printf("Enter a string : ");
    fgets(str,sizeof(str),stdin);
    str[strcspn(str,"\n")] = '\0';
    pthread_t th;
    if(pthread_create(&th, NULL, check_palindrome, str) != 0)
    {
        perror("Failed to create thread");
        exit(EXIT_FAILURE);
    }

    if(pthread_join(th, NULL) != 0)
    {
        perror("Failed to join thread");
        exit(EXIT_FAILURE);
    }

    return 0;
}
```
## Implement a C program to create a thread that performs selection sort on an array of integers?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

typedef struct {
    int *arr;
    int size;
} ThreadData;

void *selection_sort(void *arg)
{
    ThreadData *data = (ThreadData *)arg;
    int *arr = data->arr;
    int n = data->size;

    for (int i = 0; i < n - 1; i++)
    {
        int min_idx = i;
        for (int j = i + 1; j < n; j++)
        {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        int temp = arr[i];
        arr[i] = arr[min_idx];
        arr[min_idx] = temp;
    }

    return NULL;
}

int main()
{
    int n;
    scanf("%d", &n);

    int *arr = malloc(n * sizeof(int));
    for (int i = 0; i < n; i++)
        scanf("%d", &arr[i]);

    pthread_t th;
    ThreadData data = {arr, n};

    pthread_create(&th, NULL, selection_sort, &data);
    pthread_join(th, NULL);

    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");

    free(arr);
    return 0;
}
```
## Develop a C program to create a thread that calculates the area of a triangle?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

typedef struct {
    float base;
    float height;
    float area;
} Triangle;

void *calculate_area(void *arg)
{
    Triangle *tri = (Triangle *)arg;
    tri->area = 0.5f * tri->base * tri->height;
    return NULL;
}

int main()
{
    Triangle tri;
    scanf("%f %f", &tri.base, &tri.height);

    pthread_t th;
    pthread_create(&th, NULL, calculate_area, &tri);
    pthread_join(th, NULL);

    printf("Area of triangle: %.2f\n", tri.area);

    return 0;
}
```
## Write a C program to create a thread that calculates the sum of squares of numbers from 1 to 100?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

typedef struct {
    int start;
    int end;
    long long result;
} Range;

void *sum_of_squares(void *arg)
{
    Range *range = (Range *)arg;
    long long sum = 0;

    for (int i = range->start; i <= range->end; i++)
    {
        sum += (long long)i * i;
    }

    range->result = sum;
    return NULL;
}

int main()
{
    Range data = {1, 100, 0};

    pthread_t th;
    pthread_create(&th, NULL, sum_of_squares, &data);
    pthread_join(th, NULL);

    printf("Sum of squares from %d to %d is %lld\n", data.start, data.end, data.result);

    return 0;
}
```
## Write a C program to create a thread that generates a random array of integers?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <time.h>
#include <unistd.h>

typedef struct
{
    int *arr;
    int size;
} ArrayData;

void *random_array(void *arg)
{
    ArrayData *data = (ArrayData *)arg;
    for (int i = 0; i < data->size; i++)
    {
        data->arr[i] = rand() % 100;
    }
    return NULL;
}

int main()
{
    int n;
    scanf("%d", &n);

    int *arr = malloc(n * sizeof(int));

    srand(time(NULL));

    ArrayData data = {arr, n};

    pthread_t th;
    pthread_create(&th, NULL,random_array, &data);
    pthread_join(th, NULL);

    for (int i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }
    printf("\n");

    free(arr);
    return 0;
}
```
## Implement a C program to create a thread that performs bubble sort on an array of integers?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

typedef struct {
    int *arr;
    int size;
} ThreadData;

void *bubble_sort(void *arg)
{
    ThreadData *data = (ThreadData *)arg;
    int *arr = data->arr;
    int n = data->size;
    int i, j;

    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return NULL;
}

int main()
{
    int n;
    scanf("%d", &n);

    int *arr = malloc(n * sizeof(int));
    for (int i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }

    pthread_t th;
    ThreadData data = {arr, n};

    pthread_create(&th, NULL, bubble_sort, &data);
    pthread_join(th, NULL);

    for (int i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }
    printf("\n");

    free(arr);
    return 0;
}
```
## Write a C program to create a thread that calculates the sum of Fibonacci numbers up to a given limit?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

typedef struct {
    int limit;
    long long sum;
} FibData;

void *sum_fibonacci(void *arg)
{
    FibData *data = (FibData *)arg;
    int limit = data->limit;

    long long a = 0, b = 1;
    long long total = 0;

    while(a <= limit)
    {
        total += a;
        long long next = a + b;
        a = b;
        b = next;
    }

    data->sum = total;
    return NULL;
}

int main()
{
    FibData data;
    scanf("%d", &data.limit);

    pthread_t th;
    pthread_create(&th, NULL, sum_fibonacci, &data);
    pthread_join(th, NULL);

    printf("%lld\n", data.sum);
    return 0;
}
```
## Implement a C program to create a thread that calculates the sum of even numbers from 1 to 100?
```c
#include <stdio.h>
#include <pthread.h>

void *sum_even(void *arg)
{
    int sum = 0;
    for (int i = 1; i <= 100; i++)
    {
        if (i % 2 == 0)
            sum += i;
    }
    int *result = (int *)arg;
    *result = sum;
    return NULL;
}

int main()
{
    int result;
    pthread_t th;

    pthread_create(&th, NULL, sum_even, &result);
    pthread_join(th, NULL);

    printf("%d\n", result);
    return 0;
}
```
## Develop a C program to create a thread that calculates the factorial of a given number using iteration?
```c
#include <stdio.h>
#include <pthread.h>

void *factorial(void *arg)
{
    int n = *(int *)arg;
    unsigned long long fact = 1;

    for (int i = 1; i <= n; i++)
    {	
        fact *= i;
    }

    unsigned long long *result = malloc(sizeof(unsigned long long));
    *result = fact;
    return result;
}
int main()
{
    int n;
    scanf("%d", &n);

    pthread_t th;
    pthread_create(&th, NULL, factorial, &n);

    unsigned long long *fact_result;
    pthread_join(th, (void **)&fact_result);

    printf("%llu\n", *fact_result);
    free(fact_result);
    return 0;
}
```
## Write a C program to create a thread that checks if a given year is a leap year?
```c
#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>

pthread_mutex_t mutex;

void *check_leap_year(void *arg)
{
    int year = *(int*)arg;

    pthread_mutex_lock(&mutex);

    if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0))
    {
        printf("Year %d is a Leap Year.\n", year);
    }
    else
    {
        printf("Year %d is Not a Leap Year.\n", year);
    }

    pthread_mutex_unlock(&mutex);
    return NULL;
}

int main()
{
    int year;
    printf("Enter a year: ");
    scanf("%d", &year);

    pthread_t th;

    pthread_mutex_init(&mutex, NULL);

    pthread_create(&th, NULL, check_leap_year, &year);
    pthread_join(th, NULL);

    pthread_mutex_destroy(&mutex);

    return 0;
}
```
## Implement a C program to create a thread that performs multiplication of two matrices?
```c
#include <stdio.h>
#include <pthread.h>

int A[3][3], B[3][3], C[3][3];
int row1, col1, row2, col2;

void *multiply(void *arg)
{
    for (int i = 0; i < row1; i++)
    {
        for (int j = 0; j < col2; j++)
        {
            C[i][j] = 0;
            for (int k = 0; k < col1; k++)
            {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    return NULL;
}

int main()
{
    scanf("%d %d", &row1, &col1);
    for (int i = 0; i < row1; i++)
    {
        for (int j = 0; j < col1; j++)
        {
            scanf("%d", &A[i][j]);
        }
        printf("\n");
    }

    scanf("%d %d", &row2, &col2);
    for (int i = 0; i < row2; i++)
    {
        for (int j = 0; j < col2; j++)
        {
            scanf("%d", &B[i][j]);
        }
        printf("\n");
    }

    if (col1 != row2)
    {
        printf("Invalid matrix dimensions\n");
        return 1;
    }

    pthread_t th;
    pthread_create(&th, NULL, multiply, NULL);
    pthread_join(th, NULL);

    for (int i = 0; i < row1; i++)
    {
        for (int j = 0; j < col2; j++)
        {
            printf("%d ", C[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
## Develop a C program to create a thread that calculates the average of numbers from 1 to 100?
```c
#include <stdio.h>
#include <pthread.h>

void *calculate_average(void *arg)
{
    int sum = 0;
    for (int i = 1; i <= 100; i++)
    {
        sum += i;
    }

    double *avg = (double *)arg;
    *avg = sum / 100.0;
    return NULL;
}

int main()
{
    double average;
    pthread_t th;

    pthread_create(&th, NULL, calculate_average, &average);
    pthread_join(th, NULL);

    printf("%lf\n", average);
    return 0;
}
```
## Implement a C program to create a thread that generates a random string?
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <time.h>

char str[100];
int length;

void *generate_random_string(void *arg)
{
    char charset[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    int n = length;

    for (int i = 0; i < n; i++)
    {
        str[i] = charset[rand() % (sizeof(charset) - 1)];
    }
    str[n] = '\0';

    return NULL;
}

int main()
{
    scanf("%d", &length);

    srand(time(NULL));

    pthread_t th;
    pthread_create(&th, NULL, generate_random_string, NULL);
    pthread_join(th, NULL);

    printf("%s\n", str);
    return 0;
}
```
## Write a C program to create a thread that checks if a given number is a perfect square?
```c
#include <stdio.h>
#include <pthread.h>
#include <math.h>

void *check_perfect_square(void *arg)
{
    int n = *(int *)arg;
    int root = sqrt(n);
    int *res = (int *)malloc(sizeof(int));

    if (root * root == n)
    {
        *res = 1;
    }
    else
    {
        *res = 0;
    }

    return res;
}

int main()
{
    int n;
    scanf("%d", &n);

    pthread_t th;
    pthread_create(&th, NULL, check_perfect_square, &n);

    int *result;
    pthread_join(th, (void **)&result);

    if (*result)
    {
        printf("Perfect Square\n");
    }
    else
    {
        printf("Not a Perfect Square\n");
    }

    free(result);
    return 0;
}
```
## Write a C program to create a thread that calculates the sum of digits of a given number?
```c
#include <stdio.h>
#include <pthread.h>

void *sum_of_digits(void *arg)
{
    int n = *(int *)arg;
    int sum = 0;

    while (n != 0)
    {
        sum += n % 10;
        n /= 10;
    }

    int *res = (int *)malloc(sizeof(int));
    *res = sum;
    return res;
}

int main()
{
    int n;
    scanf("%d", &n);

    pthread_t th;
    pthread_create(&th, NULL, sum_of_digits, &n);

    int *result;
    pthread_join(th, (void **)&result);

    printf("%d\n", *result);
    free(result);
    return 0;
}
```
## Implement a C program to create a thread that calculates the factorial of a given number using recursion?
```c
#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>

long long recursive_factorial(int n)
{
    if (n == 0 || n == 1)
    {
        return 1;
    }
    else
    {
        return n * recursive_factorial(n - 1);
    }
}

void *factorial_thread(void *arg)
{
    int n = *(int *)arg;
    long long *res = (long long *)malloc(sizeof(long long));
    *res = recursive_factorial(n);
    return res;
}

int main()
{
    int n;
    scanf("%d", &n);

    pthread_t th;
    pthread_create(&th, NULL, factorial_thread, &n);

    long long *result;
    pthread_join(th, (void **)&result);

    printf("%lld\n", *result);
    free(result);
    return 0;
}
```
## Write a C program to create a thread that sorts an array of strings?
```c
#include <stdio.h>
#include <string.h>
#include <pthread.h>

char arr[100][100];
int n;

void *sort_strings(void *arg)
{
    char temp[100];
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (strcmp(arr[i], arr[j]) > 0)
            {
                strcpy(temp, arr[i]);
                strcpy(arr[i], arr[j]);
                strcpy(arr[j], temp);
            }
        }
    }
    return NULL;
}

int main()
{
    printf("Enter array size : ");
    scanf("%d", &n);

    printf("Enter elements in array : ");
    for (int i = 0; i < n; i++)
    {
        scanf("%s", arr[i]);
    }

    pthread_t th;
    pthread_create(&th, NULL, sort_strings, NULL);
    pthread_join(th, NULL);

    for (int i = 0; i < n; i++)
    {
        printf("%s\n", arr[i]);
    }

    return 0;
}
```
## Implement a C program to create a thread that calculates the square root of a number?
```c
#include <stdio.h>
#include <pthread.h>
#include <math.h>
#include <stdlib.h>

void *calculate_sqrt(void *arg)
{
    double n = *(double *)arg;
    double *res = (double *)malloc(sizeof(double));
    *res = sqrt(n);
    return res;
}

int main()
{
    double n;
    printf("Enter a number to calculate square root: ");
    scanf("%lf", &n);

    pthread_t th;
    pthread_create(&th, NULL, calculate_sqrt, &n);

    double *result;
    pthread_join(th, (void **)&result);

    printf("Square root: %lf\n", *result);

    free(result);
    return 0;
}
```





