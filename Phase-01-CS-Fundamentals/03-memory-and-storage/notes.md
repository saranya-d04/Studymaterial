# Topic 03: Memory and Storage

## Why This Matters for DevOps

Every day as a DevOps engineer, you'll deal with:
- "Container killed: OOMKilled" (Out of Memory)
- "Disk space full on node"
- "Application is slow" (could be swap thrashing)
- Setting memory limits in Kubernetes
- Choosing instance types based on memory needs

**Without understanding memory, you'll just guess at solutions.**

---

## 1. Memory vs Storage: The Fundamental Difference

### Analogy: Kitchen vs Pantry

| Concept | Kitchen Counter (Memory/RAM) | Pantry (Storage/Disk) |
|---------|------------------------------|----------------------|
| Purpose | Active work area | Long-term storage |
| Speed | Instant access | Takes time to fetch |
| Size | Limited space | Much larger |
| Persistence | Cleared when done | Stays until removed |
| Cost | Expensive | Cheaper |

### In Computer Terms

```
┌─────────────────────────────────────────────────────────────┐
│                        RAM (Memory)                          │
│  - Temporary, volatile (lost when power off)                │
│  - Fast: nanoseconds access time                            │
│  - Expensive: ~$5 per GB                                    │
│  - Typical: 8GB - 64GB in servers                           │
└─────────────────────────────────────────────────────────────┘
                              ↑↓
┌─────────────────────────────────────────────────────────────┐
│                      Storage (Disk)                          │
│  - Permanent, non-volatile (survives power off)             │
│  - Slower: milliseconds (HDD) to microseconds (SSD)         │
│  - Cheaper: ~$0.10 per GB (SSD)                             │
│  - Typical: 100GB - multiple TB                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 2. The Memory Hierarchy

Speed and cost trade-off - faster = more expensive = smaller:

```
                    ┌───────────┐
                    │ CPU       │  ← Fastest (1 cycle)
                    │ Registers │     128 bytes
                    └─────┬─────┘
                          │
                    ┌─────▼─────┐
                    │   L1      │  ← Very Fast (4 cycles)
                    │  Cache    │     32-64 KB per core
                    └─────┬─────┘
                          │
                    ┌─────▼─────┐
                    │   L2      │  ← Fast (10 cycles)
                    │  Cache    │     256 KB - 1 MB per core
                    └─────┬─────┘
                          │
                    ┌─────▼─────┐
                    │   L3      │  ← Moderate (40 cycles)
                    │  Cache    │     8-64 MB shared
                    └─────┬─────┘
                          │
              ┌───────────▼───────────┐
              │         RAM           │  ← Slower (100+ cycles)
              │    (Main Memory)      │     8-512 GB
              └───────────┬───────────┘
                          │
              ┌───────────▼───────────┐
              │       SSD/NVMe        │  ← Much Slower (10,000+ cycles)
              │                       │     256 GB - 4 TB
              └───────────┬───────────┘
                          │
              ┌───────────▼───────────┐
              │         HDD           │  ← Slowest (millions of cycles)
              │                       │     1 TB - 20 TB
              └───────────────────────┘
```

### Real Numbers (Approximate)

| Level | Access Time | DevOps Analogy |
|-------|-------------|----------------|
| L1 Cache | 1 nanosecond | Thought in your head |
| L2 Cache | 4 nanoseconds | Note on your desk |
| L3 Cache | 12 nanoseconds | File in your drawer |
| RAM | 100 nanoseconds | Book on your shelf |
| SSD | 100 microseconds | File cabinet in the room |
| HDD | 10 milliseconds | Document in warehouse |
| Network | 100+ milliseconds | File in another building |

---

## 3. Cache: The Speed Booster

### What Is Cache?

Cache is a small, fast memory that stores **frequently accessed data** so the CPU doesn't have to wait for slow RAM.

### How Cache Works

```
CPU needs data at address 0x1000
        │
        ▼
┌──────────────────┐
│ Check L1 Cache   │ ──► Found? (Cache HIT) ──► Return data instantly
└────────┬─────────┘
         │ Not found (Cache MISS)
         ▼
┌──────────────────┐
│ Check L2 Cache   │ ──► Found? (Cache HIT) ──► Copy to L1, return
└────────┬─────────┘
         │ Miss
         ▼
┌──────────────────┐
│ Check L3 Cache   │ ──► Found? (Cache HIT) ──► Copy to L2, L1, return
└────────┬─────────┘
         │ Miss
         ▼
┌──────────────────┐
│ Fetch from RAM   │ ──► Copy to L3, L2, L1, return (SLOW!)
└──────────────────┘
```

### Cache Hit vs Miss

- **Cache Hit**: Data found in cache → Fast!
- **Cache Miss**: Data not in cache → Must fetch from slower memory

**Cache Hit Rate** = (Hits / Total Requests) × 100%

A 99% hit rate vs 95% hit rate can mean 5x performance difference!

### DevOps Real-World: Redis Cache

Same concept applies to application caching:

```
User requests product data
        │
        ▼
┌─────────────────┐
│  Check Redis    │ ──► Found? ──► Return instantly (1ms)
│  (Cache)        │
└────────┬────────┘
         │ Miss
         ▼
┌─────────────────┐
│  Query Database │ ──► Fetch data (100ms)
│                 │     Store in Redis
└─────────────────┘     Return to user
```

---

## 4. RAM (Main Memory) Deep Dive

### How RAM Works

RAM = Random Access Memory
- "Random" means any byte can be accessed directly (no sequential reading)
- Organized as a grid of cells, each holding one bit
- Grouped into bytes, each with a unique address

```
RAM Address Space (simplified for 16 bytes):

Address │ Content (1 byte each)
────────┼───────────────────────
0x0000  │ [01001000]  ← "H"
0x0001  │ [01100101]  ← "e"
0x0002  │ [01101100]  ← "l"
0x0003  │ [01101100]  ← "l"
0x0004  │ [01101111]  ← "o"
0x0005  │ [00000000]  ← null terminator
0x0006  │ [????????]  ← other data
  ...   │    ...
```

### Types of RAM

| Type | Full Name | Characteristics |
|------|-----------|-----------------|
| DRAM | Dynamic RAM | Needs refresh, cheaper, used as main memory |
| SRAM | Static RAM | No refresh, faster, expensive, used for cache |
| DDR4/DDR5 | Double Data Rate | Current standard for servers |

### Memory in Servers

```bash
# Check memory on Linux
free -h

# Output explanation:
              total        used        free      shared  buff/cache   available
Mem:           15Gi       8.2Gi       1.1Gi       512Mi       6.1Gi       6.5Gi
Swap:          2.0Gi       100Mi      1.9Gi

# Key terms:
# - total: Physical RAM installed
# - used: Currently in use by applications
# - free: Completely unused (often low, that's OK)
# - buff/cache: Used for disk caching (can be reclaimed)
# - available: Memory available for new applications (free + reclaimable cache)
```

---

## 5. Virtual Memory: The Memory Illusion

### The Problem

- Physical RAM is limited (e.g., 16 GB)
- Programs want to use more memory
- Multiple programs want to run simultaneously
- Programs shouldn't access each other's memory

### The Solution: Virtual Memory

Each process thinks it has its own private, continuous memory space.

```
Process A's View          Process B's View          Physical RAM
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│ 0x0000 - Code   │      │ 0x0000 - Code   │      │ Process A Code  │
│ 0x1000 - Data   │      │ 0x1000 - Data   │      │ Process B Code  │
│ 0x2000 - Heap   │      │ 0x2000 - Heap   │      │ Process A Data  │
│ 0x3000 - Stack  │      │ 0x3000 - Stack  │      │ Process B Heap  │
│      ...        │      │      ...        │      │ [Free]          │
│ 0xFFFF          │      │ 0xFFFF          │      │ Process A Stack │
└─────────────────┘      └─────────────────┘      └─────────────────┘
     Virtual                  Virtual                  Physical
```

### How It Works: Page Tables

Memory is divided into **pages** (typically 4 KB each).

The **Memory Management Unit (MMU)** translates virtual → physical addresses:

```
Virtual Address 0x12345678
        │
        ▼
┌──────────────────────┐
│  MMU + Page Table    │
│                      │
│  Page 0x12345 → 0xABC│  (mapping)
└──────────┬───────────┘
           │
           ▼
Physical Address 0xABC678
```

### Benefits of Virtual Memory

1. **Isolation**: Process A can't crash Process B
2. **Security**: Processes can't read each other's data
3. **Simplicity**: Each process sees clean address space starting at 0
4. **More capacity**: Can use disk as extended memory (swap)

---

## 6. Swap: When RAM Runs Out

### What Is Swap?

Swap is disk space used as "emergency" RAM when physical memory is full.

```
┌─────────────────────────────────────────────────────────────┐
│                        Physical RAM                          │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐           │
│  │Process A│ │Process B│ │Process C│ │Process D│  [FULL!]  │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘           │
└─────────────────────────────────────────────────────────────┘
                              │
         Process E starts, needs memory
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  OS: "I'll move Process A's unused pages to swap (disk)"    │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                        Physical RAM                          │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐           │
│  │Process E│ │Process B│ │Process C│ │Process D│           │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘           │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                        Swap (Disk)                           │
│  ┌─────────────────────┐                                    │
│  │ Process A's pages   │  ← Stored here, MUCH slower!       │
│  └─────────────────────┘                                    │
└─────────────────────────────────────────────────────────────┘
```

### Swap Thrashing: The Performance Killer

When the system constantly moves pages between RAM and swap:

```
Time →
┌──────────────────────────────────────────────────────────┐
│ Normal operation:                                         │
│ CPU: [work][work][work][work][work][work][work]          │
│ Disk: [idle][idle][idle][idle][idle][idle][idle]         │
└──────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────┐
│ Thrashing:                                                │
│ CPU: [wait][work][wait][wait][work][wait][wait]          │
│ Disk: [swap][swap][swap][swap][swap][swap][swap]         │
│                                                           │
│ → System becomes EXTREMELY slow!                          │
└──────────────────────────────────────────────────────────┘
```

### DevOps Critical: Swap in Containers

**Kubernetes best practice: Disable swap on nodes!**

Why?
- Containers have memory limits
- Swap makes memory limits unpredictable
- Thrashing affects ALL containers on the node
- Better to OOMKill one container than slow everything

```bash
# Disable swap
sudo swapoff -a

# Check if swap is disabled
free -h
# Swap line should show 0
```

---

## 7. Storage Types: HDD vs SSD vs NVMe

### Hard Disk Drive (HDD)

```
Physical spinning platter with magnetic coating:

    ┌─────────────────┐
    │   Read/Write    │
    │      Head       │
    │        ↓        │
    │  ╭───────────╮  │
    │  │ ○○○○○○○○○ │  │  ← Spinning platter
    │  │ ○○○○○○○○○ │  │    (5400-7200 RPM)
    │  │ ○○○○○○○○○ │  │
    │  ╰───────────╯  │
    └─────────────────┘

- Must physically move head to location
- Seek time: 5-10 milliseconds
- Sequential read: 100-200 MB/s
- Random read: very slow
```

### Solid State Drive (SSD)

```
No moving parts - electronic chips:

    ┌─────────────────┐
    │  NAND Flash     │
    │  ┌───┬───┬───┐  │
    │  │ █ │ █ │ █ │  │  ← Memory chips
    │  ├───┼───┼───┤  │
    │  │ █ │ █ │ █ │  │
    │  ├───┼───┼───┤  │
    │  │ █ │ █ │ █ │  │
    │  └───┴───┴───┘  │
    │   Controller    │
    └─────────────────┘

- Electronic access, no movement
- Latency: 0.1 milliseconds
- Sequential read: 500-600 MB/s (SATA)
- Random read: Nearly as fast as sequential
```

### NVMe (Non-Volatile Memory Express)

```
SSD + Direct PCIe connection:

    ┌─────────────────┐
    │   NVMe SSD      │
    │  (M.2 or PCIe)  │
    │                 │
    │  Direct PCIe    │ ← No SATA bottleneck
    │  connection     │
    └────────┬────────┘
             │
    ─────────┴───────────  PCIe Bus (CPU direct)

- Same flash technology as SSD
- Faster interface (PCIe vs SATA)
- Latency: 0.02 milliseconds
- Sequential read: 3000-7000 MB/s
- Ideal for databases, high I/O workloads
```

### Comparison Table

| Feature | HDD | SATA SSD | NVMe SSD |
|---------|-----|----------|----------|
| Latency | 10ms | 0.1ms | 0.02ms |
| Sequential Read | 150 MB/s | 550 MB/s | 3500 MB/s |
| Random IOPS | 100 | 90,000 | 500,000 |
| Price/TB | $20 | $80 | $100 |
| Best For | Backups, archives | General workloads | Databases, high I/O |

---

## 8. IOPS: The DevOps Performance Metric

### What Is IOPS?

**IOPS = Input/Output Operations Per Second**

Measures how many read/write operations storage can handle.

### Why IOPS Matters

```
Database server handling 1000 users:
- Each user request = ~10 disk operations
- Total needed: 10,000 IOPS

Your storage:
- HDD: 100 IOPS ← Users wait forever!
- SSD: 90,000 IOPS ← Handles easily
```

### Real Cloud Example (AWS EBS)

| Volume Type | IOPS | Use Case |
|-------------|------|----------|
| gp2 (General SSD) | 3,000-16,000 | Boot volumes, dev/test |
| gp3 (General SSD) | 3,000-16,000 | Most workloads |
| io1/io2 (Provisioned) | Up to 64,000 | Databases |
| st1 (HDD) | 500 | Big data, logs |

---

## 9. Memory in Containers and Kubernetes

### Container Memory Limits

```yaml
# Kubernetes Pod spec
resources:
  requests:
    memory: "256Mi"   # Minimum guaranteed memory
  limits:
    memory: "512Mi"   # Maximum allowed memory
```

### What Happens When Limit Exceeded?

```
Container memory usage over time:

Memory
  512Mi ┤ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ LIMIT ─ ─ ─ ─ ─ ─ ┤
        │                              ╱        │
        │                           ╱           │
  256Mi ┤ ─ ─ ─ ─ REQUEST ─ ─ ─ ╱               │
        │                    ╱                  │
        │                 ╱                     │
        │              ╱                        │
        │           ╱                           │
    0   ┼─────────────────────────────────────→ Time
        
        Container tries to use > 512Mi?
                    │
                    ▼
        ┌─────────────────────┐
        │  KILLED (OOMKilled) │  ← Out Of Memory
        └─────────────────────┘
```

### Common DevOps Memory Issues

| Issue | Symptoms | Solution |
|-------|----------|----------|
| Memory leak | Container restarts repeatedly | Fix application code, profile memory |
| Limit too low | OOMKilled frequently | Increase limit, optimize app |
| No limit set | One container starves others | Always set limits |
| JVM heap issues | Java containers OOMKilled | Set -Xmx less than container limit |

---

## 10. Practical Commands for DevOps

### Check Memory Usage

```bash
# Overall system memory
free -h

# Per-process memory
ps aux --sort=-%mem | head -10

# Detailed memory info
cat /proc/meminfo

# Watch memory in real-time
watch -n 1 free -h

# Interactive process viewer
htop  # or top
```

### Check Disk Usage

```bash
# Disk space by filesystem
df -h

# Directory sizes
du -sh /var/*

# Find large files
find / -type f -size +100M 2>/dev/null

# Disk I/O statistics
iostat -x 1

# Check inode usage (file count limit)
df -i
```

### Container Memory

```bash
# Docker container stats
docker stats

# Kubernetes pod memory
kubectl top pods

# Describe pod (see limits, OOM events)
kubectl describe pod <pod-name>
```

---

## 11. Key Formulas and Numbers to Remember

### Memory Sizes

| Unit | Bytes | Example |
|------|-------|---------|
| KB (Kilobyte) | 1,000 | Small text file |
| KiB (Kibibyte) | 1,024 | |
| MB (Megabyte) | 1,000,000 | Photo |
| MiB (Mebibyte) | 1,048,576 | Kubernetes uses this! |
| GB (Gigabyte) | 1,000,000,000 | Movie |
| GiB (Gibibyte) | 1,073,741,824 | |

### DevOps Memory Rules of Thumb

1. **Application heap should be ~75% of container limit** (leave room for OS)
2. **If swap usage > 0 frequently, add more RAM**
3. **Cache is good** - high buff/cache in `free` is normal
4. **Available memory matters**, not free memory

---

## Summary: What You Must Remember

### For Interviews

1. **Memory hierarchy**: Registers → L1 → L2 → L3 → RAM → SSD → HDD
2. **Cache hit/miss**: Hit = fast, Miss = slow; higher hit rate = better
3. **Virtual memory**: Gives each process isolated address space
4. **Swap**: Disk as emergency RAM; causes thrashing if overused
5. **IOPS**: Storage performance metric; SSDs >> HDDs
6. **OOMKilled**: Container killed for exceeding memory limit

### For Daily Work

1. Use `free -h` to check memory
2. Use `df -h` and `du -sh` for disk
3. Always set memory limits in Kubernetes
4. Disable swap on Kubernetes nodes
5. Choose storage type based on IOPS needs

---

## What's Next?

After completing exercises for this topic, we'll move to:
**Topic 04: Operating Systems Basics** - Kernel, processes, threads, system calls

This will complete Phase 01, preparing you for Linux administration!
