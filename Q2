#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

#define bufferSize 1000
#define printLimit 50

unsigned char buffer[bufferSize];
int buffer_index = 0;
pthread_mutex_t buffer_mutex = PTHREAD_MUTEX_INITIALIZER;

void* sensor_simulator() {
    while (1) {
        int num_bytes = rand() % 6;  // 0 to 5 random bytes
        pthread_mutex_lock(&buffer_mutex);
        for (int i = 0; i < num_bytes; i++) {
            if (buffer_index < bufferSize) {
                buffer[buffer_index++] = rand() % 256;
            }
        }
        pthread_mutex_unlock(&buffer_mutex);
        sleep(1);
    }
    return NULL;
}

void* data_checker() {
    while (1) {
        
        pthread_mutex_lock(&buffer_mutex);
        if (buffer_index >= printLimit) {
            printf("Latest %d bytes in hex:\n", printLimit);
            for (int i = buffer_index - printLimit; i < buffer_index; i++) {
                printf("%02X ", buffer[i]);
            }printf("\n");
            
            buffer_index -= printLimit;
        }
        pthread_mutex_unlock(&buffer_mutex);
    }
    return NULL;
}

int main() {
    srand(time(NULL));
    pthread_t sensor_thread, checker_thread;

    pthread_create(&sensor_thread, NULL, sensor_simulator, NULL);
    pthread_create(&checker_thread, NULL, data_checker, NULL);

    pthread_join(sensor_thread, NULL);
    pthread_join(checker_thread, NULL);

    return 0;
}
