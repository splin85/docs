# ARM体系

## ARM有16个通用寄存器
    r0-r12
    r13(sp)
    r14(lr)
    r15(pc)
    cpsr 
    spsr




## ARM MMU
    采用二级页表
    1，一级页表基地址TTB保存在cp15:c2寄存器中
        31   TTB    14|13  SBZ  0 
        
    2，一级页表, PGT
        包含12bit的二级页表基地址
        
    3, 二级页表
        包含20bit的PTE  
     
        