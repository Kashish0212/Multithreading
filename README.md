# BRIEF
The above code has two concurrent threads sensor_simulator() and data_checker() , the first thread simulates a sensor and generate 0 to 5 number of random bytes and adds it to the global buffer, while the latter runs an infinite loops and checks if there are 50 bytes in the buffer and prints the latest 50 bytes.
The threads are made Thread safe using mutex locks to make sure race conditions don't ensue.
The main function creates the two threads and waits for them to complete but since both the threads run an infinite loop , that won't happen.
