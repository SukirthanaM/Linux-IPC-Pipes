# Linux-IPC--Pipes
Linux-IPC-Pipes


# Ex03-Linux IPC - Pipes

# AIM:
To write a C program that illustrate communication between two process using unnamed and named pipes

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - pipe(), fifo()

### Step 3:

Testing the C Program for the desired output. 

# PROGRAM:

## C Program that illustrate communication between two process using unnamed pipes using Linux API system calls

```
#include<unistd.h>
#include<stdio.h>
int main(){
int fd[2];
char buffer[100];
pipe(fd);
if (fork()==0){
close(fd[0]);
write(fd[1],"Hello from child",17);
close(fd[1]);
} else {
close(fd[1]);
read(fd[0],buffer,sizeof(buffer));
printf("Received:%s\n",buffer);
close(fd[0]);
}
return 0;
}
```



## OUTPUT
<img width="338" height="80" alt="image" src="https://github.com/user-attachments/assets/00b0888a-f057-4514-8659-2bd9cdcee708" />


## C Program that illustrate communication between two process using named pipes using Linux API system calls
```
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<unistd.h>
#include<stdio.h>
int main(){
char *fifo = "/tmp/myfifo";
char buffer[100];
mkfifo(fifo,0666);
if(fork()==0){
int fd = open(fifo, O_WRONLY);
write(fd, "Hello from child",17);
close(fd);
} else {
int fd = open(fifo, O_RDONLY);
read(fd, buffer, sizeof(buffer));
printf("Received: %s\n", buffer);
close(fd);
}
return 0;
}


```
## OUTPUT

<img width="338" height="92" alt="image" src="https://github.com/user-attachments/assets/7b3bd850-c088-4e38-8110-ea6d87d5201a" />

# RESULT:
The program is executed successfully.
