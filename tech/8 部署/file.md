## tail

```bash
# 对比两个目录下的文件差异
diff <(cd folder1 && find |sort) <(cd folder2 && find | sort) -y | grep -E '>|<'

# 查找一段时间内被修改过的文件（不含删除）
find . -type f -newermt "2024-04-05 00:00:00" ! -newermt "2024-04-06 00:00:00"

# 查看文件改动信息
stat ./file.txt

# 统计文件数量
find . -type f | wc -l

# 查找文件大小超过10M的文件
find . -type f -size +10M

# 查找文件大小超过10M的文件并着色
find . -xdev -size +10M -type f -print0 | xargs -0 ls -Ssh1 --color

# 查找文件大小在10M到20M之间的文件并着色
find . -xdev -size +10M -size -20M -type f -print0 | xargs -0 ls -Ssh1 --color

# 判断系统是 BIOS 还是 UEFI
ls /sys/firmware/efi  # 该目录存在为 UEFI 系统，否则为 BIOS 系统

# 创建软链接
ln -s /etc/filename... ~/
```

## CPU 使用率

```bash
#!/bin/bash

# 存储 CPU 总时间和空闲时间
PREV_IDLE=0
PREV_IDLE=0

while true; do

  # 读取 CPU 统计数据
  CPU=($(sed -n 's/^cpu\s//p' /proc/stat))
  IDLE=${CPU[3]}
  TOTAL=0

  # 累加到 TOTAL 中
  for VALUE in "${CPU[@]:0:8}"; do
    TOTAL=$((TOTAL+VALUE))
  done

  # 计算当前与上一次的 CPU 总时间差并四舍五入
  DIFF_IDLE=$((IDLE-PREV_IDLE))
  DIFF_TOTAL=$((TOTAL-PREV_TOTAL))
  DIFF_USAGE=$(((1000*(DIFF_TOTAL-DIFF_IDLE)/DIFF_TOTAL+5)/10))

  echo -en "\rCPU: $DIFF_USAGE% \b\b"

  # 更新使用率以便于下一次使用
  PREV_TOTAL="$TOTAL"
  PREV_IDLE="$IDLE"

  sleep 1

done
```

tail -f demo.log | awk '{now=starftime("%F %T%z\t"); sub(/^/, now);print}'
