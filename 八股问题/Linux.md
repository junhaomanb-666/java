# Linux

> 原标题为 Linux 10 题，目前实际提供 9 题。第 10 题待后续补充。

## 1. 如何查看系统资源使用情况？

**答案：**

- `top`：查看 CPU、内存、进程
- `free -h`：查看内存
- `df -h`：查看磁盘
- `vmstat`：查看虚拟内存、CPU、IO 等
- `iostat`：查看磁盘 IO

## 2. 如何查看端口是否被占用？

**答案：**

```bash
netstat -tulnp | grep :端口号
ss -tulnp | grep :端口号
lsof -i:端口号
```

## 3. 软链接和硬链接的区别？

**答案：** 软链接指向文件路径，删除源文件后软链接会失效，可以跨分区；硬链接指向 inode，删除源文件后仍可使用，通常不能跨分区。

## 4. Linux 的启动流程？

**答案：** BIOS 加电自检 -> 加载 MBR 引导 GRUB -> GRUB 加载内核 -> 启动 `init` / `systemd` -> 进入多用户或图形模式 -> 用户登录。

## 5. 如何给文件添加执行权限？

**答案：**

```bash
chmod +x script.sh
chmod 755 script.sh
```

## 6. 如何查看进程详细信息？

**答案：**

```bash
ps aux | grep 进程名
top -p PID
cat /proc/PID/status
```

## 7. 如何查看系统日志？

**答案：**

- `/var/log/messages`：常见系统日志路径
- `journalctl -xe`：查看最近系统错误和 systemd 日志

## 8. inode 是什么？

**答案：** inode 用于存储文件元数据，包括文件大小、权限、时间戳、数据块位置等。每个文件都有对应的 inode。

## 9. Linux 系统负载高如何排查？

**答案：** 先用 `uptime` 查看负载，再用 `top` 定位高 CPU 进程，用 `iostat` 检查 IO，用 `free` 检查内存，最后结合 `dmesg` 或 `journalctl` 查看系统日志。

## 10. 待补充

**答案：** 当前未提供。
