# Operating System

27 May 2024 - 31 May 2024

- Study point of views about operating systems
- Linux, Open source and free software
- History: Minix and others operating systems
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
- Containers orquestration
- Process Monitoring
- Observability, Telemetry and Monitoring
- Service Meshes
- IO Blocking
- Brokers
- Streaming
- Websockets
- Social Network Architectures




# Create Bootloader

What does a bootloader do?
A boot loader is a critical piece of software running on any system. Whenever a computing system is initially powered on, the first piece of code to be loaded and run is the boot loader. It provides an interface for the user to load.

# Kernel in C

# Tiny Os in C

# Resources
https://wiki.osdev.org/Main_Page
