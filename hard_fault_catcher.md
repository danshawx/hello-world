# RAM:M0+
## stack frame after go to HardFault_Handler

|stack frame| remark|
| --------  | -------- |
|previous  |<-SP points here before interrupt
|xPSR      |SP+0x1c
|PC        |SP+0x18  <-address before goto HardFault_Handler ***
|LR        |SP+0x14
|R12       |SP+0x10
|R3        |SP+0x0c
|R2        |SP+0x08
|R1        |SP+0x04
|R0        |<-SP points here after interrupt(SP0)

struct stack frame in C
```
typedef struct
{
    uint32_t r0;
    uint32_t r1;
    uint32_t r2;
    uint32_t r3;
    uint32_t r12;
    uint32_t lr;
    uint32_t pc;
    uint32_t psr;
} stackregisters;
```

## save core registers to a new buffer
- addr_start_buffer,addr_end_buffer
- in order to save core registers, new SP points to addr_end_buffer
  
|core registers|
| -------- |
|msp(SP0) |<-SP'-0x2c
|psp |SP'-0x28
|exceptionPSR|SP'-0x24
|r4|SP'-0x20
|r5|SP'-0x1c
|r6|SP'-0x18
|r7|SP'-0x14
|r8|SP'-0x10
|r9|SP'-0x0c
|r10|SP'-0x08
|r11|SP'-0x04
|exceptionLR|<-SP'(addr_end_buffer)

struct core registers in C

```
typedef struct
{
    uint32_t msp;
    uint32_t psp;
    uint32_t exceptionPSR;
    uint32_t r4;
    uint32_t r5;
    uint32_t r6;
    uint32_t r7;
    uint32_t r8;
    uint32_t r9;
    uint32_t r10;
    uint32_t r11;
    uint32_t exceptionLR;
}core_registers;
```
