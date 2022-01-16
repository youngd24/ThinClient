# Wyse 7000 Series

## Overview

The Dell Wyse 7000 series consists of the 7010 and 7020 model. They are virtually the
same with differences in the video capabilities they come with. Details are available
here: https://www.dell.com/ae/business/p/wyse-z-class/pd.

They're also referred to as the "z class" thin clients, the one I have examined is a
Zx0 unit.

What you'll find here is all the info I have found, both by reading and by doing, as well
as tips and tricks to hack it up to run various things, namely Linux.

## Specs

### Processor

I have found various data sheets for the 7010 and 7020 that claim it carries a quad
core AMD GX-420CA at 2.0 GHz however the 7020 (more on that later) that I purchased 
has the following for CPU:

```
sysadmin@lab-ws01:~$ cat /proc/cpuinfo
processor       : 0
vendor_id       : AuthenticAMD
cpu family      : 20
model           : 2
model name      : AMD G-T56N Processor
stepping        : 0
microcode       : 0x5000119
cpu MHz         : 1643.010
cache size      : 512 KB
physical id     : 0
siblings        : 2
core id         : 0
cpu cores       : 2
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 6
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid aperfmperf pni monitor ssse3 cx16 popcnt lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch ibs skinit wdt hw_pstate vmmcall arat npt lbrv svm_lock nrip_save pausefilter
bugs            : fxsave_leak sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips        : 3293.23
TLB size        : 1024 4K pages
clflush size    : 64
cache_alignment : 64
address sizes   : 36 bits physical, 48 bits virtual
power management: ts ttp tm stc 100mhzsteps hwpstate

processor       : 1
vendor_id       : AuthenticAMD
cpu family      : 20
model           : 2
model name      : AMD G-T56N Processor
stepping        : 0
microcode       : 0x5000119
cpu MHz         : 1514.965
cache size      : 512 KB
physical id     : 0
siblings        : 2
core id         : 1
cpu cores       : 2
apicid          : 1
initial apicid  : 1
fpu             : yes
fpu_exception   : yes
cpuid level     : 6
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid aperfmperf pni monitor ssse3 cx16 popcnt lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch ibs skinit wdt hw_pstate vmmcall arat npt lbrv svm_lock nrip_save pausefilter
bugs            : fxsave_leak sysret_ss_attrs null_seg spectre_v1 spectre_v2 spec_store_bypass
bogomips        : 3293.23
TLB size        : 1024 4K pages
clflush size    : 64
cache_alignment : 64
address sizes   : 36 bits physical, 48 bits virtual
power management: ts ttp tm stc 100mhzsteps hwpstate
```

The data sheet I was looking at here https://thinclientbenefits.com/uploads/products/downloads/Wyse-7020-Thin-Client-Data-Sheet.pdf must be for a different version. Most of the eBay listings I
see for the 7000's say they have the AMD dual-core CPU I have.

## Networking

## Power

The 7010 and 7020 both use a 19V power supply, they're available on eBay or on Amazon
here: https://www.amazon.com/APD-Adapter-Client-Class-Compatible/dp/B07PBMNH81


## Other Resources

* https://www.parkytowers.me.uk/thin/wyse/z/zx0q/
