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
		return	ret;  
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



