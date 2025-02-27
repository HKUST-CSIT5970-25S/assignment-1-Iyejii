[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: CHEN YUJIE
### Student Id: 21135353
### Email: ychenni@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    >  **Measurement tool and configuration:**  
    > The measurement tool used in this assignment is Phoronix Test Suite with its default configuration.
    > 
    > **Measurement and values:**  
    > CPU performance is measured by exeucting 7-zip compression and the result is measured in MIPS (Million Instructions Per Second), which represents the speed at which CPU operates instructions. The higher, the better.  
    > Memory performance is measured by exeucting the "copy integer" operation and the result is measured in MB/s (Megabytes per Second), which represents the rate at which data can be transferred to and from memory. The higher, the better.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?
    > **Yes, the performance of EC2 instances increases with more vCPUs and memory**.  
    > t2.micro has 1vCPU and 1GiB memory, t2.medium and c5d.large, both have 2vCPU and 4GiB memory. As shown in the table, the results of t2.medium and c5d.large are close and both show better CPU and memory performance than t2.micro.
    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |3089 MIPS        |10768.56 MB/S        |
    | `t2.medium`  |7880 MIPS        |19464.42 MB/S        |
    | `c5d.large` |6163 MIPS        |13596.71 MB/S        |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.
    > Overall, within the same region, **instances of the same type generally experience higher TCP bandwidth and lower RTT compared to instances of different types.**  
    > For example, m5.large - m5.large shows the performance with 4950 Mbps and 0.181 ms RTT, while m5.large - t3.medium has the lowest performance with 1740 Mbps and 0.875 ms RTT. Thus, network performance is better between instances of the same type.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |3986            |0.256     |
    | `m5.large` - `m5.large`   |4950            |0.181     |
    | `c5n.large` - `c5n.large` |4960            |0.293     |
    | `t3.medium` - `c5n.large` |2860            |0.572     |
    | `m5.large` - `c5n.large`  |3170            |0.414     |
    | `m5.large` - `t3.medium`  |1740            |0.875     |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

3. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.
   > As shown in the table below, **instances deployed in the same region experience much better network performance compared to those in different regions.**

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |32.3            |56.992    |
    | N. Virginia - N. Virginia |4760            |0.275     |
    | Oregon - Oregon           |4870            |0.184     |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
