- Template:
	- Paper or framework or optimization dimension
	- Comment paper from which we get comments on the particular framework
	- comments

----------------
# 1 Enable stack customization of L2–L7

## 1.1 mOS[NSDI'2017]

### ClickNF[ATC'18]

In mOS, the design of a modular middlebox platform based on mTCP is presented.

## 1.2 PDP data plane[INFOCOM WKSHPS'2016]

### ClickNF[ATC'18]

In this paper, authors introduce an overview of the control and data planes of a modular architecture, with focus on hardware acceleration.

# 2 Proposed Network stacks to overcome the I/O inefﬁciencies of OS

## 2.1 IX[OSDI'2014]

### ClickNF[ATC'18]

IX separates the control plane and data plane processing. 

## 2.2 Arrakis[OSDI'2014]

### ClickNF[ATC'18]

Arrakis is a customized OS that provide applications with direct access to I/O devices, allowing kernel bypass for I/O operations.

## 2.3 mTCP [NSDI'2014]

### ClickNF[ATC'18]

mTCP is a user-level TCP implementation proposed for multicore systems. It provides a socket API for application development supporting L2–L4 zero copy.

## 2.4 Stackmap [ATC'16]

### ClickNF[ATC'18]

Stackmap provides packet I/O acceleration to TCP kernel implementation obtaining better performance compared to Linux TCP.

## 2.5 Sandstorm [SIGCOMM'14]

### ClickNF[ATC'18]

 Sandstorm [35] proposes a specialized network stack with zero-copy APIs merging application and  network logics. 
 
## 2.6 Modnet [NSDI'2015]

### ClickNF[ATC'18]

 Similarly to ClickNF, Modnet has a modular approach for providing customizable networking stack, but modularity is limited to L2–L4. 

## 2.7 [OpenFastPath](https://openfastpath.org/index.php/service/technicaloverview/)

### ClickNF[ATC'18]

Providing efﬁcient, sometimes modular, networking stacks but cannot completely beneﬁt of L2–L7 modularity provided by ClickNF. 

## 2.8  [6windgate](https://www.6wind.com/vrouter-solutions/6windgate/)

### ClickNF[ATC'18]

Providing efﬁcient, sometimes modular, networking stacks but cannot completely beneﬁt of L2–L7 modularity provided by ClickNF. 

## 2.9 [FD.io](https://fd.io/)

### ClickNF[ATC'18]

Providing efﬁcient, sometimes modular, networking stacks but cannot completely beneﬁt of L2–L7 modularity provided by ClickNF. 


## 2.10 VPP 

### High-speed Software Data Plane by Vectorized Packet Processing [ScienceDirect'2018]

Vector Packet Processor (VPP) is one of such frameworks, representing an interesting point in the design space in that it oﬀers:
1. in user-space networking
2.  the ﬂexibility of a modular router (Click and variants) with 
3.  the beneﬁts brought by techniques such as batch processing that have become commonplace in high-speed networking stacks (such as netmap or DPDK). 
4. Similarly to Click, VPP lets users arrange functions as a processing graph, providing a full-blown stack of network functions.
5. unlike Click where the whole tree is traversed for each packet, in VPP each traversed node processes all packets in the batch (called vector) before moving to the next node.

**Modularity and batch processing**

In a nutshell, VPP combines the ﬂexibility of a modular router (retaining a programming model similar to that of Click) with high-speed performance. Additionally, it does so in a very eﬀective way, by extending beneﬁts brought by techniques such as batch processing to the whole packet processing path, increasing as much as possible the number of instructions per clock cycle (IPC) executed by the microprocessor. This is in contrast with existing batch processing techniques, that are merely used to either reduce interrupt pressure (e.g., as done by lower-building blocks such as or are non-systematic and pay the price of a high-level implementation (e.g., in FastClick batch processing advantages are oﬀset by the overhead of managing linked-lists). 

**Packet processing rate**

VPP can sustain a rate of up to 12 millions packets per second (Mpps) with general-purpose CPU.

**Advantages of vpp comparing with other KB solutions**
*Table 1: State of the art in KBnet frameworks*
| Framework [Ref.] | LFMT | IOB | RSS | Z-C | CB | CC&L | LLP | Main Purpose |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DPDK | ✔ | ✔ | ✔ | ✔ |  |  |  | Low-level IO |
| netmap| ✔ | ✔ | ✔ | ✔ |  |  |  | Low-level IO |
|  |  |  |  | |  | |  |  |
| PacketShader| ✔ | ✔ | ✔ |  |  |  |  | Routing  |
| MTclass| ✔ | ✔ | ✔ |  |  |  |  | Classiﬁcation  |
| Augustus| ✔ | ✔ | ✔ | ✔ |  |  |  | Name-based fwd  |
| HCS| ✔ | ✔ | ✔ | ✔ |  |  |  | Caching  |
| |  |  |  | |  | |  |  |
| Click|  |  |  |  |  |  |  | Modularity   |
| RouteBricks| ✔ |  | ✔ |  |  |  |  | Modularity   |
| DoubleClick| ✔ | ✔ | ✔ | ✔ |  |  |  | Modularity  |
| FastClick| ✔ | ✔ | ✔ | ✔ | partial |  |  | Modularity   |
| BESS/SoftNIC| ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |  | Modularity   |
| VPP (this work)| ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | Modularity   |

## 2.11 Click[TCOS'00]

### ClickNF[ATC'18]

Click misses sever functionalities t make itself one **full-stack** data plane for network functions, which contain:
1. L4 native implementation
	- prevents cross-layer optimizations and stack customization.
2. No support for blocking I/O primitives
	- forcing applications to use more complex asynchronous non-blocking I/O.
3. Click applications must resort to OS stack
	- incurs severe IO bottlenecks.
4. Despite recent improvements, Click does not support hardware offload and efficient time management.
	- preventing it to scale at high-speed in particular scenarios.

### High-speed Software Data Plane by Vectorized Packet Processing [ScienceDirect'2018]

In particular, the original Click placed most of the high-speed functionalities as close as possible to the hardware, which were thus implemented as separate kernel modules. However, whereas a kernel module can directly access a hardware device, user-space applications need to explicitly perform system-calls and use the kernel as an intermediate step, thus adding overhead to the main task. 

## 2.12 FastClick [ANCS'15]

### High-speed Software Data Plane by Vectorized Packet Processing [ScienceDirect'2018]

**batch processing**: Batch processing in FastClick is non-systematic and pays the price of a high-level implementation. In FastClick batch processing advantages are oﬀset by the overhead of managing linked-lists.

## 2.13 Routebricks [SIGOPS'09]

## 2.14 Fast Userspace Packet Processing [ANCS'15]



# 3 Low-level building blocks to bypass kernel

## 3.1 netmap [ATC'12]

### High-speed Software Data Plane by Vectorized Packet Processing [ScienceDirect'2018]

a tendency has emerged to implement high-speed stacks bypassing operating system kernels (aka kernel-bypass networks, referred to as KBstacks in what follows) and bringing the hardware abstraction directly to the user-space, with a number of eﬀorts (cfr. Sec. 2) targeting (i) low-level building blocks for kernel bypass like netmap [38] and the Intel Data Plane Development Kit (DPDK).

**batch processing**: netmap just uses batch processing to reduce interrupt pressure.

## 3.2 DPDK 

### High-speed Software Data Plane by Vectorized Packet Processing [ScienceDirect'2018]

a tendency has emerged to implement high-speed stacks bypassing operating system kernels (aka kernel-bypass networks, referred to as KBstacks in what follows) and bringing the hardware abstraction directly to the user-space, with a number of eﬀorts (cfr. Sec. 2) targeting (i) low-level building blocks for kernel bypass like netmap [38] and the Intel Data Plane Development Kit (DPDK).

**batch processing**: DPDK just uses batch processing to reduce interrupt pressure.


# 4 Very specific kernel-bypass functions

1. PacketShader[SIGCOMM'10]

2. Wire-speed statistical classiﬁcation of network traﬃc on commodity hardware [ACM IMC, 2012]

3. Caesar [ANCS'14]

4. Hierarchical Content Stores in High-speed ICN Routers: Emulation and Prototype Implementation [ACM ICN, 2015]


# 5 Advances of one packet processing framework

1. hardware offloading
2. multicore scalability
3. timing wheels
4. epoll-based API to improve performance

# 6 General-purpose kernel stack

### High-speed Software Data Plane by Vectorized Packet Processing [ScienceDirect'2018]

More generally, thanks to the recent improvements in transmission speed and network cards capabilities, a general-purpose kernel stack is far too slow for processing packets at wire-speed among multiple interfaces.[Fast userspace packet processing, In ACM/IEEE ANCS, 2015]
