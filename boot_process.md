# key functions
## arch/arm/src/stm32l4/stm32l4_start.c
- __start
## arch/arm/src/stm32l4/stm32l4_rcc.c
- stm32l4_clockconfig
## arch/arm/src/stm32l4/stm32l4_gpio.c
- stm32l4_gpioinit
## arch/arm/src/stm32l4/stm32l4_lowputc.c
- stm32l4_lowsetup
## arch/arm/src/common/arm_initialize.c
- up_initialize
## boards/arm/stm32l4/stm32l475-pandora/src/stm32_boot.c
- stm32l4_board_initialize
## boards/arm/stm32l4/stm32l475-pandora/src/stm32_autoleds.c
- stm32l4_autoled_initialize
## boards/arm/stm32l4/stm32l475-pandora/src/stm32_bringup.c
- stm32l4_bringup
## sched/init/nx_bringup.c
- nx_bringup
## sched/init/nx_start.c
- nx_start

# key variables
## arch/arm/src/armv7-m/arm_vector.c
### *unsigned* _vectors[] `arm异常向量表`

# 系统启动过程 
## _vectors[]
### __start `入口函数`
- stm32l4_clockconfig
- stm32l4_fpuconfig
- stm32l4_lowsetup
- stm32l4_gpioinit()
- clear bss section 
- move data section to sram 
- stm32l4_board_initialize
    - board_autoled_initalize
- nx_start
    - nxsem_initialize
    - task_initialize
    - fs_initialize
    - irq_initialize
    - wd_initialize
    - clock_initialize
    - timer_initialize
    - nxsig_initialize
    - nxmq_initialize
    - net_initialize
    - up_initialize
    - board_early_initialize
    - shm_initialize
    - lib_initialize
    - syslog_initialize
    - nx_bringup
        - nx_pgworker
        - nx_workqueues
        - nx_create_initthread
            - kthread_create(nx_start_task)
                - nx_start_application
                    - board_late_initialize
                        - stm32l4_bringup
                    - nxtask_create("init")

