# H3的mainline uboot启动bsp内核

只要用两句uboot启动魔法参数命令

```
setenv machid 1029
setenv bootm_boot_mode sec
```

就能启动 bsp 内核

