#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
#include<semaphore.h>
sem_t s;
pthread_t T1, T2;
void *f2()
{
printf("\nF2 called"); 
}
void *f1()
{
printf("\nF1 called"); 
pthread_create(&T2, NULL, f2, NULL);
}
void *fa()
{
sem_wait(&s);
printf("\nThread for fa Entered"); 
sleep(1);
printf("\nThread For fa Done"); 
sem_post(&s);
}
void *fb()
{
sem_wait(&s);
printf("\nThread For fb Entered"); 
sleep(1);
printf("\nFunction fb Thread Done");  
sem_post(&s);
}
void *fc()
{
sem_wait(&s);
printf("\nThread for fc Entered ");  
sleep(1);
printf("\nThread Function fc Done ");  
sem_post(&s);
}
int main()
{
sem_init(&s, 3, 1); 
pthread_create(&T1, NULL, f1, NULL); 
sleep(3);
pthread_create(&T2, NULL, fa, NULL);  
sleep(3);
pthread_create(&T1, NULL, fb, NULL);  
sleep(2);
pthread_create(&T2, NULL, fc, NULL);  
pthread_join(T1, NULL);
pthread_join(T2, NULL);
printf("\nThreads Executed Successfully");  
}
