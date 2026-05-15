---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-03-15T16:16
updated: 2026-04-03T15:42
---
### The Recommended Scaling Sequence

Keep your OpenMP threads fixed at `OMP_NUM_THREADS=4` for almost the entire test, as this optimally saturates a single NUMA node. You will scale down by removing entire nodes, then entire sockets, then NUMA domains.

1. **128 Cores (Max):** 4 Nodes × 8 MPI Ranks (32 total MPI) × 4 OMP
    
2. **64 Cores:** 2 Nodes × 8 MPI Ranks (16 total MPI) × 4 OMP _(Shows inter-node network scaling efficiency)_
    
3. **32 Cores:** 1 Node × 8 MPI Ranks (8 total MPI) × 4 OMP _(Shows the boundary of leaving the network and running purely on shared memory/bus)_
    
4. **16 Cores:** 1 Node × 4 MPI Ranks (4 total MPI) × 4 OMP _(Exactly 1 Socket. Shows inter-socket QPI/UPI bus overhead)_
    
5. **8 Cores:** 1 Node × 2 MPI Ranks (2 total MPI) × 4 OMP
    
6. **4 Cores:** 1 Node × 1 MPI Rank (1 total MPI) × 4 OMP _(Exactly 1 NUMA domain. Pure OpenMP performance essentially)_
    
7. **1 Core (Absolute Baseline):** 1 Node × 1 MPI Rank × 1 OMP Thread _(Required if you want to calculate absolute parallel speedup)_
    

### What data to record in your CSV:

To allow the Python script in the Canvas to automatically calculate efficiency, you should add these columns to your results CSV when you run the tests:

- `num_nodes` (e.g., 4, 2, 1)
    
- `total_mpi_ranks` (e.g., 32, 16, 8, 4, 2, 1)
    
- `omp_threads` (e.g., 4, 1)
    
- `total_cores` (Just `total_mpi_ranks` * `omp_threads`)
    

### What this sequence will reveal:

By stepping down this way, your resulting efficiency graphs will show exactly where your bottlenecks are. For example:

- If efficiency drops sharply between **Step 3 and Step 2**, your bottleneck is the cluster's network interconnect (MPI).
    
- If efficiency drops between **Step 4 and Step 3**, your bottleneck is the inter-socket communication on the motherboard.
    

Once you have generated this data and added those columns to your CSV, let me know! I can then immediately update the Python script in the Canvas to generate standard HPC Strong Scaling, Weak Scaling, and Parallel Efficiency curves.

Ah, sorry for the confusion! Let me break down exactly what happens in the hardware at Steps 4, 3, and 2, and why comparing them is so important for analyzing your code's performance.

When we talk about these steps, we are looking at how far your data has to travel to get from one processor to another.

**Step 4: Running on Exactly 1 Socket (16 Cores)**

- **The Hardware:** You are using just **one physical CPU chip** on the motherboard.
    
- **What it means:** All 4 of your MPI ranks (and their OpenMP threads) are physically sitting right next to each other on the same piece of silicon. They share the same local memory channels. Communication here is extremely fast.
    

**Step 3: Running on Exactly 1 Node (32 Cores)**

- **The Hardware:** You are now using **both physical CPU chips (Sockets)** on a single motherboard.
    
- **What it means:** Your MPI ranks now have to talk across the motherboard. To send data from Socket 1 to Socket 2, it has to cross a physical bridge on the motherboard (called a UPI or QPI link).
    
- **The Insight:** By comparing the performance of Step 4 to Step 3, you can see exactly how much "penalty" your code pays for having to cross that motherboard bridge.
    

**Step 2: Running on 2 Nodes (64 Cores)**

- **The Hardware:** You are now using **two completely separate server boxes**.
    
- **What it means:** To share data, the information must leave the motherboard entirely, go out through a network card, travel across a physical cable (like InfiniBand or Ethernet) through a switch, and into the other server.
    
- **The Insight:** Comparing Step 3 (all inside one box) to Step 2 (going across network cables) shows you your **Network MPI Overhead**. If your code slows down dramatically here, it means your code is sending too many small MPI messages across the network.
    

**In Summary:**

- **Step 4 -> Step 3:** Shows the cost of communicating across the **motherboard**.
    
- **Step 3 -> Step 2:** Shows the cost of communicating across the **network cables**.
    

By tracking these specific steps in your CSV, you can tell your professors or colleagues exactly _where_ the bottleneck in the cluster is!

---

all the confs:

### 1. The Maximum Run (128 Cores / 4 Nodes)

_Tests maximum cluster throughput._

Bash

```
#SBATCH --nodes=4                   # 4 Compute Nodes
#SBATCH --ntasks-per-node=8         # 8 MPI Ranks per node
#SBATCH --cpus-per-task=4           # 4 Cores per Rank (for OpenMP) 
```

### 2. The 2-Node Run (64 Cores / 2 Nodes)

_Shows how well your MPI scales across the network cables._

Bash

```
#SBATCH --nodes=2                   # 2 Compute Nodes
#SBATCH --ntasks-per-node=8         # 8 MPI Ranks per node
#SBATCH --cpus-per-task=4           # 4 Cores per Rank (for OpenMP) 
```

### 3. The Single Node Run (32 Cores / 1 Node)

_Removes network cables. Tests communication across the motherboard between the 2 sockets._

Bash

```
#SBATCH --nodes=1                   # 1 Compute Node
#SBATCH --ntasks-per-node=8         # 8 MPI Ranks per node
#SBATCH --cpus-per-task=4           # 4 Cores per Rank (for OpenMP) 
```

### 4. The Single Socket Run (16 Cores / 1 Socket)

_Restricts execution to a single physical CPU chip. Removes motherboard cross-talk overhead._

Bash

```
#SBATCH --nodes=1                   # 1 Compute Node
#SBATCH --ntasks-per-node=4         # 4 MPI Ranks per node (1/2 the node)
#SBATCH --cpus-per-task=4           # 4 Cores per Rank (for OpenMP) 
```

### 5. Two NUMA Domains (8 Cores)

_Tests intermediate memory access scaling on a single socket._

Bash

```
#SBATCH --nodes=1                   # 1 Compute Node
#SBATCH --ntasks-per-node=2         # 2 MPI Ranks per node
#SBATCH --cpus-per-task=4           # 4 Cores per Rank (for OpenMP) 
```

### 6. Single NUMA Domain (4 Cores / Pure OpenMP)

_All 4 cores share the exact same local L3 cache. This essentially acts as a pure OpenMP test, removing almost all MPI overhead._

Bash

```
#SBATCH --nodes=1                   # 1 Compute Node
#SBATCH --ntasks-per-node=1         # 1 MPI Rank per node
#SBATCH --cpus-per-task=4           # 4 Cores per Rank (for OpenMP) 
```

### 7. The Absolute Baseline (1 Core / Sequential-ish)

_Your true baseline. Used to calculate your absolute "Speedup" factor in the Strong Scaling chart._

Bash

```
#SBATCH --nodes=1                   # 1 Compute Node
#SBATCH --ntasks-per-node=1         # 1 MPI Rank per node
#SBATCH --cpus-per-task=1           
```



