#include<stdio.h>
#include<unistd.h>
#include<pthread.h>
#include<semaphore.h>
sem_t mutex;
pthread_t t1, t2;
void f2()
{
printf("\nF2 called"); 
}
void f1()
{
printf("\nF1 called"); 
pthread_create(&t2, NULL, f2, NULL);
}
void fa()
{
sem_wait(&mutex);
printf("\nThread for fa Entered"); 
sleep(2);
printf("\nThread For fa Done"); 
sem_post(&mutex);
}
void fb()
{
sem_wait(&mutex);
printf("\nThread For fb Entered"); 
sleep(2);
printf("\nFunction fb Thread Done");  
sem_post(&mutex);
}
void fc()
{
sem_wait(&mutex);
printf("\nThread for fc Entered ");  
sleep(2);
printf("\nThread Function fc Done ");  
sem_post(&mutex);
}
int main()
{
sem_init(&mutex, 3, 1); 
pthread_create(&t1, NULL, f1, NULL); 
sleep(4);
pthread_create(&t2, NULL, fa, NULL);  
sleep(4);
pthread_create(&t1, NULL, fb, NULL);  
sleep(3);
pthread_create(&t2, NULL, fc, NULL);  
pthread_join(t1, NULL);
pthread_join(t2, NULL);
printf("\nThreads Executed Successfully");  
}
