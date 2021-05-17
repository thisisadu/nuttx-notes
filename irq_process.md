# key functions
## arch/arm/src/armv7-m/gnu/arm_exception.S
- exception_common
## arch/arm/src/armv7-m/arm_doirq.c
- arm_doirq
## sched/irq/irq_initialize.c
- irq_initialize
## sched/irq/irq_dispatch.c
- irq_dispatch
## sched/irq/irq_attach.c
- irq_attach

# key structures
## sched/irq/irq.h
### struct irq_info_s
#### xcpt_t handler `记录handler`
#### void *arg `记录handler参数`

# key variables
## arch/arm/src/armv7-m/arm_vector.c
### *unsigned* _vectors[] `arm异常向量表`
## sched/irq/irq_initialize.c
### *struct irq_info_s* g_irqvector[] `保存所有的isr`

# irq 初始化过程 
## irq_initialize `设置所有的handler到默认isr`
- 
    ```c
    for (i = 0; i < TAB_SIZE; i++){
      g_irqvector[i].handler = irq_unexpected_isr;
      g_irqvector[i].arg     = NULL;
    }
    ```
# irq 绑定过程
## irq_attach
- 
    ```c
    g_irqvector[ndx].handler = isr;
    g_irqvector[ndx].arg     = arg;
    ```

# irq 派发过程
## _vectors[]
### exception_common
#### arm_doirq
##### irq_dispatch
- 
    ```c
    if (g_irqvector[ndx].handler)
    {
        vector = g_irqvector[ndx].handler;
        arg    = g_irqvector[ndx].arg;
    }
    CALL_VECTOR(ndx, vector, irq, context, arg);
    ```
