# [分享一个香橙派PC2的C语言点亮LED程序](http://blog.csdn.net/u013908686/article/details/62422799)

转发自[http://blog.csdn.net/u013908686/article/details/62422799](http://blog.csdn.net/u013908686/article/details/62422799)

[小王子与木头人](http://my.csdn.net/u013908686)

首先要编写字符设备驱动,代码大同小异，随便复制粘贴就行了。  
但是要注意了，一定要保护好寄存器，不要乱搞，要不然系统崩了，就等着你妈妈喊你回家吃饭吧。



led.c

```
#include <linux/module.h>
#include <linux/init.h>
#include <linux/cdev.h>
#include <linux/fs.h>
#include <linux/io.h>
#include<linux/device.h>  
#include "led.h"

#define LED_MAJOR        245                //主设备号 

unsigned int *led_config; 
unsigned int *led_data; 
unsigned int *led_pull; 

struct cdev cdev;
dev_t devno;

int led_open(struct inode *node, struct file *filp)
{
    uint32_t register_dat;

    //000:Input 001:Output 
    led_config = ioremap(PA_CFG1,4);//从datesheet里面查询你的寄存器 这里用的是PA10
    register_dat = readl(led_config);//先读取寄存器值 只操作你需要操作的位段 不要干扰其他端口 
    register_dat &= ~(0x7<<8);//清空PA10的值
    writel(register_dat|0x1<<8,led_config);//PA10 设置成输出

    //00: Pull-up/down disable 01: Pull-up 10: Pull-down 11: Reserved
    led_pull = ioremap(PA_PILL0,4);
    register_dat = readl(led_pull);//读取寄存器值
    register_dat &= ~(0x3<<2*10);//清空PA10设置
    writel((register_dat|0x1<<2*10),led_pull);//PA10 上拉

    led_data = ioremap(PA_DAT,4);

    return 0;
}

long led_ioctl(struct file *filp, unsigned int cmd, unsigned long arg)
{
    uint32_t reg_dat;
    switch (cmd)
    {
        case LED_ON:
        reg_dat = readl(led_data);
            reg_dat &= ~(1<<10);
            writel(reg_dat|0x0<<10,led_data);
            return 0;    

        case LED_OFF:
        reg_dat = readl(led_data);
        reg_dat &= ~(1<<10);
            writel(reg_dat|0x1<<10,led_data);
            return 0;

        default:
            return -EINVAL;
    }
}

static struct file_operations led_fops =
{
    .owner= THIS_MODULE,
    .open = led_open,
    .unlocked_ioctl = led_ioctl,
};

#define DEVICE_NAME "myled"
static struct class*leds_class; 
static int led_init(void)
{
    int ret;
    //注册LED设备为字符设备 
    ret = register_chrdev(LED_MAJOR, DEVICE_NAME, &led_fops); 
    if(ret< 0)  
    {  
        printk(DEVICE_NAME" major number register falid!\n");  
        return    ret;  
    }  

//注册一个类，使mdev可以在/dev/下面建立设备节点 
    leds_class= class_create(THIS_MODULE, DEVICE_NAME);
    if(IS_ERR(leds_class) )  
    {  
        printk("creatleds_class failed!");  
        return-1;  
    }  

//创建一个设备节点，节点名字为DEVICE_NAME
    device_create(leds_class,NULL, MKDEV(LED_MAJOR, 0), NULL, DEVICE_NAME);
    printk(DEVICE_NAME"initialized!");

    return 0;    
}

static void led_exit(void)
{
    //注销设备  
    unregister_chrdev(LED_MAJOR,DEVICE_NAME);  
    //删除设备节点  
    device_destroy(leds_class,MKDEV(LED_MAJOR, 0));  
    //注销类  
    class_destroy(leds_class);  
}

module_init(led_init);
module_exit(led_exit);

MODULE_LICENSE("GPL");  
MODULE_AUTHOR("leo_learning");  
MODULE_DESCRIPTION("myled driver");
```



以下是led.h

这里把所有的GPIO都列出来了

```
#ifndef _LED_H
#define _LED_H

//GPIOA_10
#define GPIO_BASE 0x01C20800 
#define PA_CFG0  GPIO_BASE+0x0000+0*0x24 //GPIOA0-7
#define PA_CFG1  GPIO_BASE+0x0004+0*0x24 //GPIOA8-15
#define PA_CFG2  GPIO_BASE+0x0008+0*0x24 //GPIOA17-21
#define PA_CFG3  GPIO_BASE+0x000C+0*0x24 //GPIOA
#define PA_DAT   GPIO_BASE+0x0010+0*0x24 //GPIOA_DAT
#define PA_DRV0  GPIO_BASE+0x0014+0*0x24
#define PA_DRV1  GPIO_BASE+0x0018+0*0x24
#define PA_PILL0 GPIO_BASE+0x001C+0*0x24 
#define PA_PILL1 GPIO_BASE+0x0020+0*0x24

#define PC_CFG0  GPIO_BASE+0x0000+1*0x24 //GPIOC0-7
#define PC_CFG1  GPIO_BASE+0x0004+1*0x24 //GPIOC8-15
#define PC_CFG2  GPIO_BASE+0x0008+1*0x24 //GPIOC17-21
#define PC_CFG3  GPIO_BASE+0x000C+1*0x24 //GPIOC
#define PC_DAT   GPIO_BASE+0x0010+1*0x24 //GPIOC_DAT
#define PC_DRV0  GPIO_BASE+0x0014+1*0x24
#define PC_DRV1  GPIO_BASE+0x0018+1*0x24
#define PC_PILL0 GPIO_BASE+0x001C+1*0x24 
#define PC_PILL1 GPIO_BASE+0x0020+1*0x24

#define PD_CFG0  GPIO_BASE+0x0000+2*0x24 //GPIOD0-7
#define PD_CFG1  GPIO_BASE+0x0004+2*0x24 //GPIOD8-15
#define PD_CFG2  GPIO_BASE+0x0008+2*0x24 //GPIOD17-21
#define PD_CFG3  GPIO_BASE+0x000C+2*0x24 //GPIOD
#define PD_DAT   GPIO_BASE+0x0010+2*0x24 //GPIOD_DAT
#define PD_DRV0  GPIO_BASE+0x0014+2*0x24
#define PD_DRV1  GPIO_BASE+0x0018+2*0x24
#define PD_PILL0 GPIO_BASE+0x001C+2*0x24 
#define PD_PILL1 GPIO_BASE+0x0020+2*0x24

#define PE_CFG0  GPIO_BASE+0x0000+3*0x24 //GPIOE0-7
#define PE_CFG1  GPIO_BASE+0x0004+3*0x24 //GPIOE8-15
#define PE_CFG2  GPIO_BASE+0x0008+3*0x24 //GPIOE17-21
#define PE_CFG3  GPIO_BASE+0x000C+3*0x24 //GPIOE
#define PE_DAT   GPIO_BASE+0x0010+3*0x24 //GPIOE_DAT
#define PE_DRV0  GPIO_BASE+0x0014+3*0x24
#define PE_DRV1  GPIO_BASE+0x0018+3*0x24
#define PE_PILL0 GPIO_BASE+0x001C+3*0x24 
#define PE_PILL1 GPIO_BASE+0x0020+3*0x24

#define PF_CFG0  GPIO_BASE+0x0000+4*0x24 //GPIOF0-7
#define PF_CFG1  GPIO_BASE+0x0004+4*0x24 //GPIOF8-15
#define PF_CFG2  GPIO_BASE+0x0008+4*0x24 //GPIOF17-21
#define PF_CFG3  GPIO_BASE+0x000C+4*0x24 //GPIOF
#define PF_DAT   GPIO_BASE+0x0010+4*0x24 //GPIOF_DAT
#define PF_DRV0  GPIO_BASE+0x0014+4*0x24
#define PF_DRV1  GPIO_BASE+0x0018+4*0x24
#define PF_PILL0 GPIO_BASE+0x001C+4*0x24 
#define PF_PILL1 GPIO_BASE+0x0020+4*0x24

#define PG_CFG0  GPIO_BASE+0x0000+5*0x24 //GPIOG0-7
#define PG_CFG1  GPIO_BASE+0x0004+5*0x24 //GPIOG8-15
#define PG_CFG2  GPIO_BASE+0x0008+5*0x24 //GPIOG17-21
#define PG_CFG3  GPIO_BASE+0x000C+5*0x24 //GPIOG
#define PG_DAT   GPIO_BASE+0x0010+5*0x24 //GPIOG_DAT
#define PG_DRV0  GPIO_BASE+0x0014+5*0x24
#define PG_DRV1  GPIO_BASE+0x0018+5*0x24
#define PG_PILL0 GPIO_BASE+0x001C+5*0x24 
#define PG_PILL1 GPIO_BASE+0x0020+5*0x24

#define PL_CFG0  GPIO_BASE+0x0000+6*0x24 //GPIOL0-7
#define PL_CFG1  GPIO_BASE+0x0004+6*0x24 //GPIOL8-15
#define PL_CFG2  GPIO_BASE+0x0008+6*0x24 //GPIOL17-21
#define PL_CFG3  GPIO_BASE+0x000C+6*0x24 //GPIOL
#define PL_DAT   GPIO_BASE+0x0010+6*0x24 //GPIOL_DAT
#define PL_DRV0  GPIO_BASE+0x0014+6*0x24
#define PL_DRV1  GPIO_BASE+0x0018+6*0x24
#define PL_PILL0 GPIO_BASE+0x001C+6*0x24 
#define PL_PILL1 GPIO_BASE+0x0020+6*0x24

#define PA_INT_CFG0 0x0200 + 0x00 + 0*0x20
#define PA_INT_CFG1 0x0200 + 0x04 + 0*0x20
#define PA_INT_CFG2 0x0200 + 0x08 + 0*0x20
#define PA_INT_CFG3 0x0200 + 0x0C + 0*0x20
#define PA_INT_CTL 0x0200 + 0x10 + 0*0x20
#define PA_INT_STA 0x0200 + 0x14 + 0*0x20
#define PA_INT_DEB 0x0200 + 0x18 + 0*0x20
#define PF_INT_CFG0 0x0200 + 0x00 + 1*0x20
#define PF_INT_CFG1 0x0200 + 0x04 + 1*0x20
#define PF_INT_CFG2 0x0200 + 0x08 + 1*0x20
#define PF_INT_CFG3 0x0200 + 0x0C + 1*0x20 
#define PF_INT_CTL 0x0200 + 0x10 + 1*0x20
#define PF_INT_STA 0x0200 + 0x14 + 1*0x20
#define PF_INT_DEB 0x0200 + 0x18 + 1*0x20
#define PG_INT_CFG0 0x0200 + 0x00 + 2*0x20
#define PG_INT_CFG1 0x0200 + 0x04 + 2*0x20
#define PG_INT_CFG2 0x0200 + 0x08 + 2*0x20
#define PG_INT_CFG3 0x0200 + 0x0C + 2*0x20
#define PG_INT_CTL 0x0200 + 0x10 + 2*0x20
#define PG_INT_STA 0x0200 + 0x14 + 2*0x20 
#define PG_INT_DEB 0x0200 + 0x18 + 2*0x20

#define LED_MAGIC 'L'

#define LED_ON _IO(LED_MAGIC,1)
#define LED_OFF _IO(LED_MAGIC,0)

#endif
```



Makefile，把这里的KDIR改成你开发板内核源码对应目录，指定交叉编译工具链，如果没有什么问题，make会编译出led.ko，只要insmod led.ko就行了， so easy

```
obj-m := led.o
KDIR := /home/share/OrangePi_H5SDK/kernel
all:
	make -C $(KDIR) M=$(PWD) modules \
	CROSS_COMPILE=/home/share/OrangePi_H5SDK/toolchain/gcc-linaro-aarch/bin/aarch64-linux-gnu- ARCH=arm64
clean:
	rm -f *.ko *.o *.mod.o *.mod.c *.symvers *.bak *.order
```



上面是在PC上给板子交叉编译的，下面给出个在板子上编译的，需要内核头文件。

```
ifneq ($(KERNELRELEASE),)
obj-m:=led.o
else
CURRENT_PATH:=$(shell pwd)
LINUX_KERNEL_PATH:=/lib/modules/$(shell uname -r)/build
all:
    make -C $(LINUX_KERNEL_PATH) M=$(CURRENT_PATH) modules
clean:
    make -C $(LINUX_KERNEL_PATH) M=$(CURRENT_PATH) clean
endif
```

最后是应用软件,安装led.ko内核模块会产生一个/dev/myled的设备节点，现在我们需要打开它，并对其进行读写操作



led\_app.c

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <sys/ioctl.h>
#include <stdlib.h>
#include "led.h"


int main(int argc, char *argv[])
{
     int fd;
     int cmd;
     
     if (argc <2 )
     {
         printf("please enter the second para!\n");
         return 0;	
     }

     cmd = atoi(argv[1]);      
     fd = open("/dev/myled",O_RDWR);

     if (cmd == 1)
         ioctl(fd,LED_ON);
     else
        ioctl(fd,LED_OFF);            

     return 0;

}
```

PC上交叉编译

```
aarch64-Linux-gnu-gcc -o led_app led_app.c
```

板子上编译

```
gcc -o led_app led_app.c
```

通过

./led\_app 0

熄灭LED



./led\_app 1

点亮

然后随便浪吧

##### 注：本文章有删改。



