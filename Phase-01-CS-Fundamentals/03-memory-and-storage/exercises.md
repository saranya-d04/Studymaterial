# Topic 03: Exercises - Memory and Storage

Complete these exercises to reinforce your understanding.

---

## Exercise 1: Memory Hierarchy

Put these in order from FASTEST to SLOWEST:

| # | Your Order | Component |
|---|------------|-----------|
|   |            | RAM |
|   |            | L1 Cache |
|   |            | HDD |
|   |            | L3 Cache |
|   |            | SSD |
|   |            | CPU Registers |
|   |            | L2 Cache |

---

## Exercise 2: Memory vs Storage

Classify each characteristic as Memory (RAM) or Storage (Disk):

| Characteristic | Memory or Storage? |
|----------------|-------------------|
| Volatile (data lost on power off) | |
| Measured in terabytes typically | |
| Nanosecond access time | |
| Stores your files permanently | |
| Where running programs live | |
| Cheaper per gigabyte | |
| Where your OS boots from | |

---

## Exercise 3: Cache Concepts

### Part A: Cache Hit Rate Calculation

A system has:
- 950 cache hits
- 50 cache misses

1. What is the total number of memory requests?
   
   Your answer: ____________

2. What is the cache hit rate?
   
   Your answer: ____________%

3. If each hit takes 1ns and each miss takes 100ns, what's the average access time?
   
   Calculation:
   
   Your answer: ____________ns

### Part B: Real-World Cache

A Redis cache shows:
- 1,000,000 requests
- 980,000 hits
- 20,000 misses (database queries)

1. What is the hit rate?
   
   Your answer: ____________%

2. If database queries take 50ms each and cache takes 1ms, how much time was saved compared to no cache?
   
   Calculation:
   
   Your answer: ____________

---

## Exercise 4: Linux Memory Commands

### Given this `free -h` output:

```
              total        used        free      shared  buff/cache   available
Mem:           16Gi        10Gi       512Mi       256Mi        5Gi        5.5Gi
Swap:          4Gi         2Gi        2Gi
```

Answer these questions:

1. How much total physical RAM does this server have?
   
   Your answer: ____________

2. How much memory is actually available for new applications?
   
   Your answer: ____________

3. Is this server under memory pressure? Why or why not?
   
   Your answer: ____________

4. How much swap is being used?
   
   Your answer: ____________

5. Should you be concerned about the swap usage? Why?
   
   Your answer: ____________

---

## Exercise 5: Virtual Memory

### True or False

| # | Statement | T/F |
|---|-----------|-----|
| 1 | Each process sees its own private address space starting at 0 | |
| 2 | Virtual memory allows processes to access each other's memory | |
| 3 | Pages are typically 4 KB in size | |
| 4 | The MMU translates virtual addresses to physical addresses | |
| 5 | Virtual memory requires a disk to function | |
| 6 | Two processes can have the same virtual address but different physical addresses | |

### Short Answer

7. Why is process isolation important?
   
   Your answer: ____________

8. What happens if Process A tries to access Process B's memory?
   
   Your answer: ____________

---

## Exercise 6: Swap and OOM

### Scenario A: Server Analysis

A Kubernetes node shows:
```
Mem:  total=32Gi  used=31Gi  free=100Mi  available=500Mi
Swap: total=8Gi   used=7Gi   free=1Gi
```

1. Is this node healthy?
   
   Your answer: ____________

2. What is likely happening?
   
   Your answer: ____________

3. What would you do to fix this?
   
   Your answer: ____________

### Scenario B: Container OOMKilled

A pod spec shows:
```yaml
resources:
  limits:
    memory: "512Mi"
```

The container keeps getting OOMKilled. Logs show the application uses ~600Mi.

1. Why is the container being killed?
   
   Your answer: ____________

2. What are two possible solutions?
   
   Solution 1: ____________
   
   Solution 2: ____________

3. Which solution is better and why?
   
   Your answer: ____________

---

## Exercise 7: Storage Types

### Part A: Match the Use Case

Match each use case to the best storage type (HDD, SATA SSD, NVMe SSD):

| Use Case | Best Storage |
|----------|-------------|
| Production PostgreSQL database | |
| Log archive storage (rarely accessed) | |
| Boot volume for development server | |
| High-frequency trading application | |
| Video file storage | |
| Container registry cache | |

### Part B: IOPS Calculation

A database server handles:
- 500 users
- Each user query = 20 disk operations
- Peak load = all users active simultaneously

1. How many IOPS are needed at peak?
   
   Calculation:
   
   Your answer: ____________ IOPS

2. Can an HDD (100 IOPS) handle this?
   
   Your answer: ____________

3. What type of storage would you recommend?
   
   Your answer: ____________

---

## Exercise 8: Kubernetes Memory

### Given this pod specification:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
spec:
  containers:
  - name: app
    image: myapp:latest
    resources:
      requests:
        memory: "256Mi"
        cpu: "250m"
      limits:
        memory: "512Mi"
        cpu: "500m"
```

Answer these questions:

1. What is the minimum memory guaranteed for this pod?
   
   Your answer: ____________

2. What is the maximum memory this pod can use?
   
   Your answer: ____________

3. If the pod tries to use 600Mi of memory, what happens?
   
   Your answer: ____________

4. If this is a Java application, what should you set `-Xmx` to?
   
   Your answer: ____________ (and why?)

---

## Exercise 9: Practical Troubleshooting

### Scenario: Slow Application

Users report your application is very slow. You SSH into the server and run these commands:

**Command 1: `free -h`**
```
              total        used        free      shared  buff/cache   available
Mem:           8Gi         7.8Gi       50Mi      100Mi        200Mi       100Mi
Swap:          2Gi         1.9Gi       100Mi
```

**Command 2: `top` (shows)**
```
%Cpu(s):  10.0 us,  5.0 sy,  0.0 ni, 20.0 id, 65.0 wa
```

Answer:

1. What does `65.0 wa` mean?
   
   Your answer: ____________

2. What is the most likely cause of slowness?
   
   Your answer: ____________

3. What evidence supports your conclusion?
   
   Your answer: ____________

4. What would you recommend to fix this?
   
   Your answer: ____________

---

## Exercise 10: Memory Math

Calculate the following (show your work):

1. A server has 64 GiB of RAM. How many MiB is that?
   
   Calculation:
   
   Your answer: ____________ MiB

2. A container limit is set to 2048Mi. How many GiB is that?
   
   Calculation:
   
   Your answer: ____________ GiB

3. How many 4 KB pages fit in 1 GiB of RAM?
   
   Calculation:
   
   Your answer: ____________ pages

4. A page table entry is 8 bytes. How much memory is needed for page table entries to map 16 GiB of virtual address space (using 4KB pages)?
   
   Calculation:
   
   Your answer: ____________ MiB

---

## Exercise 11: Fill in the Blanks

1. When a cache lookup succeeds, it's called a cache ____________.

2. When physical RAM is full, the OS moves inactive pages to ____________.

3. Excessive swapping that severely degrades performance is called ____________.

4. In Kubernetes, when a container exceeds its memory limit, it is ____________.

5. IOPS stands for ____________.

6. The ____________ translates virtual addresses to physical addresses.

7. NVMe SSDs are faster than SATA SSDs because they connect directly via ____________.

8. The command to check disk space usage in Linux is ____________.

---

## Exercise 12: Mini DevOps Scenarios

### Scenario 1

Your CI/CD pipeline builds are extremely slow. The build server has:
- 32 GB RAM (barely used)
- 1 TB HDD
- Builds involve compiling large projects and running tests

What is likely the bottleneck and how would you fix it?

Your answer: ____________

---

### Scenario 2

A production database shows:
- 99.9% cache hit rate in the application
- Response times still slow (500ms average)
- "iowait" consistently at 40%

What is the problem?

Your answer: ____________

---

### Scenario 3

After deploying to Kubernetes, pods keep restarting with status "OOMKilled". The application worked fine on a traditional VM with 4GB RAM. The pod limit is set to 4Gi.

Why might this happen?

Your answer: ____________

---

## Bonus Challenge

1. Explain why "available" memory in `free` output matters more than "free" memory for determining if a server needs more RAM.

   Your answer: ____________

2. A system running containers shows 0% swap usage but applications are still slow. What other memory-related issues could cause this?

   Your answer: ____________

3. Why do databases benefit more from NVMe storage than web servers serving static files?

   Your answer: ____________

---

## Checklist Before Moving On

- [ ] I understand the memory hierarchy (registers → cache → RAM → disk)
- [ ] I can explain cache hit/miss and calculate hit rates
- [ ] I understand virtual memory and process isolation
- [ ] I know what swap is and why it causes performance issues
- [ ] I can interpret `free -h` output correctly
- [ ] I understand the difference between HDD, SSD, and NVMe
- [ ] I know what IOPS means and why it matters
- [ ] I can set appropriate memory limits in Kubernetes
- [ ] I can troubleshoot basic memory issues

---

*Complete these exercises, then we'll do the evaluation!*
