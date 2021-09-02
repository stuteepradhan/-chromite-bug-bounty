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


   
   
   
   
   
