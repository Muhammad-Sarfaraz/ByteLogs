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

# Create Bootloader

What does a bootloader do?
A boot loader is a critical piece of software running on any system. Whenever a computing system is initially powered on, the first piece of code to be loaded and run is the boot loader. It provides an interface for the user to load.

# Kernel in C

# Tiny Os in C

# Resources
https://wiki.osdev.org/Main_Page
