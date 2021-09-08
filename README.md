# Chromite Bug Bounty 
## Week-1 
1. The __ratified__ extensions of the unprivileged spec are :

   a) M
   
   b) A
   
   c) F
   
   d) D
   
   e) Q
   
   f) C
   
   g) Zicsr
   
   h) Zifencei
   
2. Any 4 __unratified__ extensions of the unprivileged spec are:
   
   a) B
   
   b) J
   
   c) T
   
   d) Zam
   
3. The immediates have such a weird encoding. Why is that?
   
   The S-type breaks up the immediate into imm[11:5] and imm[4:0]. This is done to match the positions with the R-type format, so that there is uniformity of sorts.
   Whereas the B-type has a weirder encoding i.e. imm[12, 10:5], imm[4:1, 11]. This is done because B-type actually has 13-bit immediate as compared to 12-bit immediate of S-type.    The LSB is actually 0 which is not stored. So it actually has to encode 12 bits but because they are actually shifted in actual usage( left by one, i.e. multiply by 2), all the 
   bits are actually off by 1 bit. This requires a shifter which increases hardware cost. So to avoid shifting as much as possible, so as to have a similar alignment as S-type, 
   the B-type and J-type have such weird encodings. Therefore using such weird encodings, we achieve 2 things:
   
   * Sharing the decoding units between all instruction formats.
   * Reducing hardware cost and reducing fan-out during decoding. 
 
4. Within the 32-bit instruction format, we can add __18__ more instructions. 11 instructions are already in use and 3 are reserved. 

## Week-2

1. The minimum number of CSRs required for implementation is 0 for a small core and 4 for a general purpose 64-bit core.

2. Functions should be exhaustive with respect to every possible combination of the dependency values. Hence WARL functions which can’t be represented by the syntax defined should    be non-exhaustive.

3. The performance counters a processor/core must have are:
   a) Processor time
   
   b) Privileged time
   
   c) User time
   
   d) Queue Length
   
   e) Current Disk Queue Length
   
   f) Idle Time
   
   g) Avg. Disk sec/Read
   
   h) Disk Reads/sec
   
   i) Available MBs
   
   j) Pages/sec and Paging file usage
   
4. Paging is the main mechanism used to provide user mode with the illusion of having an AEE -- like most things in computer architecture, it turns out that memory is the            difficult part. The following are the kew points to be kept in mind while designing RISC-V's supervisor virtual memory interface:
   
   a)Pages are 4KiB at the leaf node, and it's possible to map large contiguous regions with every level of the page table.
   
   b)RV32I-based systems can have up to 34-bit physical addresses with a three level page table.
   
   c)RV64I-based systems can have multiple virtual address widths, starting with 39-bit and extending up to 64-bit in increments of 9 bits.
   
   d)Mappings must be synchronized via the sfence.vma instruction.
     
   e)There are bits for global mappings, supervisor-only, read/write/execute, and accessed/dirty.

   f)There is a single valid bit, which allows storing XLEN-1 bits of flags in an otherwise unused page tables. Additionally, there are two bits of software flags in mapped pages.

   g)Address space identifiers are 9 bits or RV32I and 16 bits on RV64I, and they're a hint so a valid implementation is to ignore them.

   h)The accessed and dirty bits are strongly ordered with respect to accesses from the same hart, but are optional (with a trap-based mechanism when unsupported).



   
   
   
   
   
