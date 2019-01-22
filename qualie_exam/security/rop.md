# The Geometry of Innocent Flesh on the Bone: Return-into-libc without Function Calls (on the x86)

## Terms

```
x86 is a dense ISA, it is easy to find multiple instruction sequences that end in a ret. x86 ISA is Turing complete ISA.
```

### Useful & Boring Instructions
- Useful :
    -   Instructions that can be used in gadgets; instructions that can end in ret instruction and none of the instructions cause the process to transfer execution away.
    -   Principles of useful instructions
        - Suffix of an instruction sequence is also a useful instruction sequence.
        - The frequency of an instruction sequence does not matter, only that it occurs.
    -   Useful instruction sequences are noted in a trie -- the root of the trie is a ret instruction.
    -   The useful instructions are scanned backwards -- all the output instruction sequences are suffixes, so works out well rather than disassemble forwards from every possible location in the hope of finding a sequence of instructions ending in ret, till the maximum length of an instruction.

- Boring :
    -  leave; ret
    - pop %ebp;ret
    - ret; jmp

### Implementation & Performance
 Since there is need to find out what portion of the libc is mapped as an executable segment, the authors parses the libc's ELF headers.
 
### Return-oriented Programming(ROP)
 Organizational Unit : Gadgets. Gadgets can do well-defined operations such as load, an xor or jump. Note that these gadgets are found in libc and are not injected using W xor X.
 Put gadgets together is the goal of ROP.

