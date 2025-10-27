# Operating System

27 May 2024 - 31 May 2024

- Study point of views about operating systems
- Linux, Open source and free software
- History: Minix and others operating systems
- Kernel
  - Kernel is the core of every operating system. It connects applications to the actual processing of data. It also manages all communications between software and hardware components to ensure usability and reliability.
- PC startup sequence, kernel, service levels and bootloaders
- Kernel Types: Monolytic, Microkernel, hybrid, modular,
  - Power On → POST → BIOS/UEFI → Bootloader (like GRUB or Windows Boot Manager).
Bootloader → Load Kernel → Kernel Manages System Resources.
Kernel Initializes System → Runlevel is Set (determines the services to start).
System Ready for User Interaction.

- Unikernel, Exokernel
  - Exokernel: Definition: A minimalistic kernel that gives applications direct access to hardware resources, avoiding abstraction layers.
Key Points: Highly flexible, allows applications to manage resources directly for maximum performance.
  - Unikernel: Definition: A minimalistic, single-purpose operating system that combines only the necessary parts of the OS with the application into one executable, running directly on hardware or a hypervisor.
Key Points: Highly efficient, secure, and optimized for specific applications.

- Extended Machine study point
- Virtualization history
- Virtualization Types
- Hypervisors
- Cloud Computing
- Cloud Services
- Cloud classification
- Operating systems level virtualization
- Docker, containers and orchestrator
- Kubernetes
- Cloud Native
- Cloud Computing and Providers
- Serverless
- Process concept
  - Process: A process is a program in execution, which includes the program code and its current activity.
- Process Control Block(PCB)
  - A data structure in the operating system kernel containing the information needed to manage a particular process.
- Process memory segmentations
  - Process memory segmentation is a way to divide a process's memory into different segments, each serving a specific purpose. 
- Process management
  - 
- Mutual Exclution
  - Mutual exclusion ensures that only one process or thread can access a shared resource at any given time, preventing conflicts and ensuring data integrity in concurrent programs.
- Deadlock
  - Deadlock occurs when two or more processes are unable to proceed because each is waiting for the other to release a resource.
- Inter Process Communication(Semaphores, shared memory, queues and sockets)
  - Inter-process communication (IPC) methods include semaphores, shared memory, message queues, and sockets. They enable communication and synchronization between processes running on a system.
- Threads and tasks
  - A thread is a basic unit of CPU utilization. In general, a thread is composed of a thread ID, program counter, register set and the stack. 
  - Threads and tasks are units of execution in a program. Threads are lightweight processes within a single process, sharing memory space, while tasks typically refer to higher-level units of work managed by a scheduler or executor.
- Concurrency and Parallelism
  - Concurrency involves multiple tasks making progress over overlapping time periods, often on a single processor. Parallelism, on the other hand, involves executing multiple tasks simultaneously, typically across multiple processors or cores, to achieve faster execution.
- Scheduler disciplines
- Corutines
  - Coroutines are lightweight concurrency primitives that enable cooperative multitasking within a single thread.
- Dekker algorithms
- Producer-consumer
- Parallel programming languages
- Concurrency problems
- Load balancing algoritms
- Map Reduce and NoSQL
- Raft Algorithm
- Distribute systems
  - A distributed System is a collection of autonomous computer systems that are physically separated but are connected by a centralized computer network that is equipped with distributed system software. The autonomous computers will communicate among each system by sharing resources and files and performing the tasks assigned to them.
- Containers orquestration
- Process Monitoring
  - Process monitoring is the practice of overseeing and managing the activities and performance of running processes on a computer system to ensure efficient operation, troubleshoot issues, and maintain system stability.
- Observability, Telemetry and Monitoring
- Service Meshes
  - Service Meshes are a dedicated infrastructure layer built to handle service-to-service communication within distributed applications. They provide capabilities like service discovery, load balancing, encryption, authentication, and monitoring. By abstracting away complex networking concerns, Service Meshes enable developers to focus on building and deploying applications without worrying about the underlying network infrastructure. Popular implementations include Istio, Linkerd, and Consul Connect.
- IO Blocking
  - I/O blocking occurs when a program is paused while waiting for input/output operations to complete, typically during file reading/writing or network communication. This synchronous process temporarily halts program execution until the I/O operation finishes, potentially causing inefficiencies in resource utilization and impacting system performance.
- Brokers
  - Brokers in operating systems act as middlemen, helping different parts of a system talk to each other smoothly. They're crucial for managing communication, resources, and services in complex setups like cloud systems or microservices. For example, message brokers ensure messages get where they need to be, service brokers help find and set up services on the fly, and resource brokers keep everything running smoothly by managing computing resources. Overall, brokers make sure everything works together seamlessly in modern computing environments.
- Streaming
  - 
In the context of operating systems (OS), streaming refers to the continuous and real-time transfer of data, such as audio and video, between devices or applications. The OS manages this by buffering data to ensure smooth playback, handling network resources to maintain quality, and using protocols like RTP, RTSP, and HLS for data transmission. Streaming allows for immediate processing and playback of data as it is received, which is essential for services like Netflix, YouTube, Spotify, and live broadcasting applications like Zoom and Twitch.
- Websockets 
  - A socket is an endpoint for sending and receiving data across a network. It is used to establish a connection between two devices, allowing them to communicate over a network using standard protocols like TCP (Transmission Control Protocol) or UDP (User Datagram Protocol).
  - Protocols: TCP, UDP, and others.
  - WebSocket is a protocol providing full-duplex communication channels over a single TCP connection. It is designed for real-time communication between a client (typically a web browser) and a server.
  - 
- Social Network Architectures

- Assembler?
  - An assembler acts as a translator for low level language. Assembly codes, written using mnemonic commands are translated by the Assembler into machine language.

- Concurrency vs Parallels? (in case single CPU core and multiple CPU cores)
  - What is critical zone?
  - What is race condition and how to handle this case?
  - What is locking mechanism? mutex? semaphore? spinlock? read lock vs write lock?
  - What is deadlock and how to avoid deadlock?

- How does memory is managed in the OS?

  - What is virtual memory? Why do we need it? How does it work?
  - How large virtual memory is?
  - What is paging?
  - Can 2 processes map to the same physical address? How and in which case?
  - What is heap space and stack space?
  - What will happen with memory when you open an application?
  - What will happen you call another function (with parameters) or return from a function?
  - What will happen with stack? (why we do not use heap here?)?
  - What will happen with registers?
  - What causes stack overflow?
  - What is dynamic allocating? How does it work?
  - How does deallocation work?
  - What happens when your computer is full of memory?
  - Why you do not need to "deallocate" local variable?
  - How does Garbage Collection work? When it will be triggered?
  - What is a pointer? What difference between pass by value and pass by reference?
  - Where global variable will be saved?

- Why in Linux everything is "file"?
  - How does mouse/keyboard/monitor... communicate with your computer?
  - What is file descriptor?
  - What is buffer? Why do we need buffer?
  - What will happen if 2 processes read/write to the same file?
  - What is system call (syscal)?

- How to do a syscal?
  - What happens with CPU when we execute a syscal?
  - What is user space and kernel space?
- Caching:
  - What is in-memory cache? (memcached/redis)
  - LRU? implement LRU in your program language! (How about multi-thread?)
  - How to migrate Cache stampede?

# EVERYTHING IS LOOP

# BIOS
BIOS (Basic Input/Output System) initializes hardware and boots the operating system, crucial for system startup and hardware communication. It shows system information, performs hardware checks, and loads the OS from storage.
```asm
ORG 0x7C00  ; Set origin to boot sector address

start:
    ; Display BIOS message
    mov si, message
    call print_string

    ; Perform hardware initialization
    call initialize_hardware

    ; Load operating system from disk
    call load_os

    ; Transfer control to operating system
    jmp 0x7E00  ; Jump to operating system start address

; Function to print a null-terminated string
print_string:
    mov ah, 0x0E  ; BIOS function to print character
.loop:
    lodsb  ; Load next character from SI into AL
    cmp al, 0  ; Check for null terminator
    je .done  ; If null terminator, exit loop
    int 0x10  ; Call BIOS interrupt to print character
    jmp .loop  ; Repeat for next character
.done:
    ret

; Function to initialize hardware
initialize_hardware:
    ; Perform hardware initialization routines here
    ret

; Function to load operating system from disk
load_os:
    ; Disk loading routine here (e.g., INT 0x13)
    ret

message db "Welcome to Tiny BIOS!", 0

TIMES 510 - ($ - $$) db 0  ; Fill rest of boot sector with zeros
DW 0xAA55  ; Boot signature

```

# Create Bootloader

What does a bootloader do?
A boot loader is a critical piece of software running on any system. Whenever a computing system is initially powered on, the first piece of code to be loaded and run is the boot loader. It provides an interface for the user to load.
```asm
BITS 16        ; Set code to 16-bit mode

ORG 0x7C00     ; Set origin to boot sector address

start:
    jmp main    ; Jump to the main bootloader code

; Define a simple message to be printed
message db 'Hello, World!', 0

main:
    ; Set up segment registers
    xor ax, ax  ; Clear AX register
    mov ds, ax  ; Set DS segment register to 0
    mov es, ax  ; Set ES segment register to 0

    ; Print the message
    mov si, message ; Load address of message into SI
    call print_string ; Call print_string subroutine

    ; Infinite loop to prevent bootloader from exiting
    jmp $       ; Jump back to current instruction indefinitely

; Subroutine to print a null-terminated string
print_string:
    lodsb       ; Load next byte from SI into AL
    or al, al   ; Check if AL is zero (end of string)
    jz .done    ; If zero, exit subroutine
    mov ah, 0x0E ; Set AH to BIOS teletype output function
    int 0x10    ; Call BIOS interrupt to print character
    jmp print_string ; Repeat for next character
.done:
    ret         ; Return from subroutine

TIMES 510 - ($ - $$) db 0 ; Fill rest of boot sector with zeros
DW 0xAA55       ; Boot signature

```

# Kernel in C
Kernel is  basically acts as an interface between user applications and hardware.
```c
// Entry point of the kernel
void kernel_main() {
    // Call initialization function
    initialize_kernel();
    
    // Enter infinite loop to keep the kernel running
    while(1) {
        // Kernel idle loop
    }
}

// Function to initialize the kernel
void initialize_kernel() {
    // Initialize hardware
    initialize_hardware();
    
    // Enable interrupts
    enable_interrupts();
    
    // Load additional OS components into memory
    load_os_components();
    
    // Start scheduler
    start_scheduler();
}

// Function to initialize hardware
void initialize_hardware() {
    // Code to initialize hardware components
}

// Function to enable interrupts
void enable_interrupts() {
    // Code to enable interrupts for handling hardware events
}

// Function to load additional OS components into memory
void load_os_components() {
    // Code to load additional components of the operating system into memory
}

// Function to start scheduler
void start_scheduler() {
    // Code to initialize task scheduler for managing processes and threads
}

```

# Tiny Os in C
An Operating System (OS) is an interface between a computer user and computer hardware

```c
#include <stdio.h>

// Entry point of the operating system
int main() {
    // Print a welcome message
    printf("Welcome to TinyOS!\n");
    
    // Enter an infinite loop to keep the OS running
    while(1) {
        // OS idle loop
    }
    
    return 0;
}

```

### What is Mounting?

Mounting = making a storage device (disk, volume, or file system) accessible at a certain path on your operating system.

When you mount a file system, your OS links it into your directory tree so you can read/write files like normal.

# Resources
https://wiki.osdev.org/Main_Page
