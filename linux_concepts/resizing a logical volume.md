1. list disk partitions by below command:
```python
┌──(hyok㉿kali)-[~]
└─$ lsblk
```

2. Additionally, you can use the `fdisk` command to list disk partitions. Here's how:
```python
┌──(hyok㉿kali)-[~]
└─$ sudo fdisk -l
```
This command will display detailed information about disk partitions, including their sizes, filesystem types, and partitioning schemes.

3. Verify the current status of the logical volumes:
```python
┌──(hyok㉿kali)-[~]
└─$ sudo lvdisplay
```
Identify the LV path of the "kali--vg-home" logical volume, for example, it could be something like `/dev/kali-vg/home`.

4. Resize the logical volume:
```python
┌──(hyok㉿kali)-[~]
└─$ sudo lvresize -L +70G /dev/kali-vg/home

  Size of logical volume kali-vg/home changed from <28.27 GiB (7236 extents) to <98.27 GiB (25156 extents).
  Logical volume kali-vg/home successfully resized.
```
This command will increase the size of the logical volume "kali--vg-home" by 70GB.

Note: Make sure to replace `/dev/kali-vg/home` with the actual LV path from Step 6.

5. Resize the filesystem to utilize the newly allocated space:
```python
┌──(hyok㉿kali)-[~]
└─$ sudo resize2fs /dev/kali-vg/home

resize2fs 1.47.0 (5-Feb-2023)
Filesystem at /dev/kali-vg/home is mounted on /home; on-line resizing required
old_desc_blocks = 4, new_desc_blocks = 13
The filesystem on /dev/kali-vg/home is now 25759744 (4k) blocks long.
```