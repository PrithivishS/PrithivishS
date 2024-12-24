## Hi there 👋

<!--
**PrithivishS/PrithivishS** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

Linux Debugging 
Day 2 
----------
Core Linux Tracers: 
Enabling Ftrace --> Which .config to look for 
perf --> Profiling tool 
BPF --> Berkeley Packet Filter
bpftrace --->
BCC  --> 


Ways to collect data
Kprobes
Ftrace
   - trace-cmd
   - kernelshark
   - 
perf_events
LTTng Linux Trace Tools
   - 
eBPF 

Flame graph


Where is ltrace useful in debugging
- Multithreaded apps use the pthread library. Ltrace very useful for debugging multithreaded applications.
- Ltrace can give you times and counts of library functions that are being used by the application
   - giving a clue to which library call are taking lot of time and also bulk of time in % of time a function is comsuming.
   - So it is like a user space profiler
 

Strace: 


-->
Strace can show you that the linux loader i.e. ld.so memory maps the glibc for any running process into the processes address space to enable the direct library calling. 

Strace depends upon debugfs 
- To verify look at the path /sys/kernel/debug/tracing
   - Can also be verified by checking tracefs by
      -  mount | grep tracefs
      -  mount point is  /sys/kernel/debug/tracing      


Some of the commands that I used for lab exercise
--------------------------------------------------
ls /sys/kernel/tracing/per_cpu/cpu0/
cat trace
pwd
cd /sys/kernel/tracing/per_cpu/cpu0/
ls
less trace
pwd
cd ../../
 echo 0 > tracing_on
cat available_tracers
echo function_graph > current_tracer
echo 1 > tracing_on ; sleep 1 ; echo 0 > tracing_on
cp trace /tmp/trace.txt
ll trace
cp -iv trace /tmp/trace.txt
cp -iv per_cpu/cpu0/trace  /tmp/trace.txt
less /tmp/trace.txt
ls options/
cat options/ function-proc
echo 1 > options/function-proc
echo 1 > options/funcgraph-proc

echo 1 > tracing_on ; sleep 1 ; echo 0 > tracing_on
cp -iv per_cpu/cpu0/trace  /tmp/trace.txt
less /tmp/trace.txt

End of lab exercise
--------------------------------------------------

To debug KVM for AMD 
filter amd.ko + kvm.ko 


command line history
 echo 0 > tracing_on
cat available_tracers
echo function_graph > current_tracer
echo 1 > tracing_on ; sleep 1 ; echo 0 > tracing_on
cp trace /tmp/trace.txt
ll trace
cp -iv trace /tmp/trace.txt
cp -iv per_cpu/cpu0/trace  /tmp/trace.txt
less /tmp/trace.txt
ls options/
cat options/ function-proc
echo 1 > options/function-proc
echo 1 > options/funcgraph-proc
echo 1 > tracing_on ; sleep 1 ; echo 0 > tracing_on
cp -iv per_cpu/cpu0/trace  /tmp/trace.txt
less /tmp/trace.txt
history
less /tmp/trace.txt
 echo 1 > tracing_on ; sleep 1 ; echo 0 > tracing_on
 ls
 cd /sys/kernel/tracing/per_cpu/cpu0/
 cd ..
 cd ..
 ;ls
 ls
 ls
 ll trace
 echo 1 > tracing_on ; /home/amd/prithvi/L1_sysprg_trg/helloworld  ; echo 0 > tracing_on
 echo 1 > tracing_on ; /home/amd/prithvi/L1_sysprg_trg/helloworld/helloworld  ; echo 0 > tracing_on
 less trace
 cp -iv trace /tmp/trace
 cp -iv ./trace /tmp/trace
 less trace
 ll trace
 cp -iv ./trace /tmp/trace
 less /tmp/trace
 less trace
 ll /tmp/trace
 du -h /tmp/trace
 less trace
 echo 1 > tracing_on ; /home/amd/prithvi/L1_sysprg_trg/helloworld/helloworld  ; echo 0 > tracing_on
 cp -iv ./trace /tmp/trace
 du -h /tmp/trace
 less  /tmp/trace
 cat available_filter_functions | less
 cat available_filter_functions | wc -l
 pwd
 lsmod | grep e*
 lsmod | grep e1*
yum install trace-cmd
trace-cmd
trace-cmd reset
echo ":mod:nft_fib_inet"  > set_ftrace_filter
ls
ll funcgraph
echo 1 > tracing_on ; ping -t yahoo.com   ; echo 0 > tracing_on
echo 1 > tracing_on ; ping -t 127.0.0.1   ; echo 0 > tracing_on
echo 1 > tracing_on ; ping  127.0.0.1   ; echo 0 > tracing_on
echo function_graph > current_tracer
echo 1 > tracing_on ; ping -c 127.0.0.1   ; echo 0 > tracing_on
echo 1 > tracing_on ; ping -c 5 127.0.0.1   ; echo 0 > tracing_on
cp -iv ./trace /tmp/trace

To redirect printk to ring buffer 
 echo z > /proc/sysrq-trigger

Trace-cmd lab exercise
--------------------------------------
Trace-cmd is a front end for tracefs 
yum install trace-cmd --allowerasing
record -p  function_graph -F ~amd/prithvi/L1_sysprg_trg/helloworld/helloworld
trace-cmd record -p  function_graph -F ~amd/prithvi/L1_sysprg_trg/helloworld/helloworld
cd ~amd/prithvi/L1_sysprg_trg/helloworld/
trace-cmd record -p  function_graph -F helloworld
trace-cmd record -p  function_graph -F ./helloworld
trace-cmd report -l
trace-cmd report -l | wc -l
less /tmp/history

------------------------------------------------
git clone https://github.com/kaiwan/trccmd.git  --> Trace cmd tool to help filter functions and events for debug

Kernel-Shark
------------------
kernel-shark is a front end for tracefs


Linutronix - Company started by Thomas Gliexner who has ported Linux to be an RTOS
https://lttng.org/features



LTTng
-----------------------------------
Linux Tracing Tool Kit

lttng enable-event --kernel sched_switch, sched_process_fork
lttng 

start
lttng start

lttng stop
lttng 


-------------------------------------------
TraceCompass Gui (www.tracecompass.org)

Demand Paging Algorithm
- User space application calling malloc
     -  vmalloc returns with an address that might correspond to an entry in the process's address space/ 
     -  If page not already in memory
          - then page fault generated and mmu checks for the existence /range  of newly assigned memory objects. Checks for valid range.  
          - Page fault handler checks
               - If new item then fault brings in a physical page that can correspond to the virtual page that contains the  malloc , if offset was validated above.
               - 
           


****
sysctl kernel.panic_on_oops

The NULL Trap
-------------------
Entire page0 consisting of 4095 bytes is used by the compiler and the system as a null trap. 
All pointers or references that are made in address range 0 to 4096 are considered faulty addresses (either directly null or derived from NULL) 

Frame Pointer
---------------------
Compilers embed framepointers as link list to link all the stack pointers of previous calling functions
It helps in unwinding the stack which helps in generating an accurate stack trace when debugging. 

ORC Stack Unwinder
------------------------


When debugging kernel modules it is a prerequisite that the kernel has been compiled in with symbol and debug support. 
Adding debug and symbol information for the kernel modules will not have much impact for debugging if the kernel was not a debug kernel. \

addr2line
----------------------
addr2line ./oops_tryv1.ko
addr2line oops_tryv1.ko
cp oops_tryv1.ko
cp oops_tryv1.ko a.out
cp oops_tryv1.ko a.out
addr2line a.out
addr2line a.out
addr2line a.out
vim
gdb -q ./oops_tryv1.ko
   -l *try_oops_init+0x7a
../../../linux-6.5.9/scripts/**faddr2line** --list ./oops_tryv1.ko  try_oops_init+0x7a

KASLR 
------


DAY 3
------------
Kdump 
Allows to dump kernel into a ram location with specified size and location
in the dump kernel there is a file called /proc/vmcore which is RAM content of the original kernel.  There are tools that can give you an insight of the ram content
copy the content of the /proc/vmcore onto storage for analysis.  Crash is the tool that allows to inspect the kernel dump image. 

There are two ways to boot 
- Using keys
- Using Kexec -- Allows for a warm boot. Retaining the contents of RAM.

To check if the kernel that you are going to build is going to be relocatable for crash debugging the following CONFIG FLAGS should be present in the .config 
of the built kernel

[amd@localhost prithvi]$ cd linux-6.5.9/
[amd@localhost linux-6.5.9]$ grep CONFIG_SYSFS .config
CONFIG_SYSFS_SYSCALL=y
CONFIG_SYSFS=y
[amd@localhost linux-6.5.9]$ grep CONFIG_KEXEC .config
CONFIG_KEXEC=y
CONFIG_KEXEC_FILE=y
CONFIG_KEXEC_SIG=y
CONFIG_KEXEC_SIG_FORCE=y
CONFIG_KEXEC_BZIMAGE_VERIFY_SIG=y
CONFIG_KEXEC_JUMP=y
CONFIG_KEXEC_CORE=y
[amd@localhost linux-6.5.9]$

Add command line parameter in file /etc/default/grub
checking for CONFIG_KEXEC             [OK]
checking for CONFIG_KEXEC_CORE        [OK]
checking for CONFIG_CRASH_CORE        [OK]
checking for CONFIG_SYSFS             [OK]
checking for CONFIG_DEBUG_INFO        [OK]
checking for CONFIG_CRASH_DUMP        [OK]
checking for CONFIG_PROC_VMCORE       [OK]
checking for CONFIG_RELOCATABLE       [OK]

sudo dnf install crash

crash help
   >vtop
   >task
   >file
   >files
   >  





