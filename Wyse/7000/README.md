# Wyse 7000 Series

## Overview

The Dell Wyse 7000 series consists of the 7010 and 7020 model. They are virtually the same with differences in the video capabilities they come with. Details are available here: https://www.dell.com/ae/business/p/wyse-z-class/pd.

They're also referred to as the "z class" thin clients, the one I have examined is a Zx0 unit.

What you'll find here is all the info I have found, both by reading and by doing, as well as tips and tricks to hack it up to run various things, namely Linux.

## Background

A couple years back I wanted to delve into the world of home automation and IoT, mainly to see the real world effects of their security and practical methods to improve that.

I started with the basics, an Echo Dot and some smart bulbs and gradually grew out of those. I decided that I'd like to give Home Assistant a shot and see what that was made of. I started with HA on an ODROID-C2 I had laying around, it hung about every day and had to be hard powered off and on so I set it aside for a year or so. I then tried it on a Pi 3 that came out of a Pi 4 upgrade and while it seemed ok it was a bit slow and again it hung, usually when I compiled ESPHome firmware. Someone on an ESPHome group had mentioned they were running HA on an old Dell Wyse thin client so I picked one up and here we are.

## Specs

### Processor

I have found various data sheets for the 7020 that claim it carries a quad core AMD GX-420CA at 2.0 GHz however the 7020 (more on that later) that I purchased has the following for CPU:

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

The data sheet I was looking at here https://thinclientbenefits.com/uploads/products/downloads/Wyse-7020-Thin-Client-Data-Sheet.pdf could be for a different version. Most of the eBay listings I see for the 7000's say they have the AMD dual-core CPU I have.

Further research seems to indicate that the 7010 did in fact ship with the dual core AMD G-T56N @ 1.5GHz the weird part is when I put the service tag from the unit I have (with the G-T56N processor shows as a 7020 from Dell. There's also the z series model numbers that seem to not be all that different across the 7010 and 7020 units, the one I have carries a tag on it calling it a Zx0Q which in other places shows as a 7020.

End result: watch eBay listings carefully for the 7010 and 7020 models, as well as the ones saying Zx0 on them. Best as I can tell these shipped as:

* Wyse 7010 - Dual-Core AMD G-T56N @ 1.5GHz
* Wyse 7020 - Quad-Core AMD GX-420CA @ 2.0 GHz

Prices can be all over the map on eBay for these and in many cases the faster quad-core CPU doesn't gain much of a price increase. The dual-core unit is quite useable though I still need to pick up a quad-core 7020 to see for real.

## Storage

I'm speaking here on the 7010 I have my hands on but from what I have read it shares the same storage options as the 7020.

There is an onboard 2.5" SATA MLC flash chip, the original ones were made by Apacer and come in various sizes from 8 to 64GB. A laptop 2.5" SSD will NOT fit inside without major modifications. I would leave that alone and just buy a used one off eBay if need be. For most embedded/dedicated type operations, such as Home Assistant, 64GB, or even 32GB, is adequate. I'm writing this right now on the 7010 with a 32GB MLC flash chip running Ubuntu.

In addition to the onboard MLC connector there is an additional SATA II data port that can be used for additional storage. It's not a standard SATA connector, thanks Dell, the power connector is elsewhere on the board. That power connector is a Micro JST (MJST) 1.5mm 4-pin one so a custom cable will be needed to connect to the SATA drive. I just ordered one from Aliexpress to see how it can be made, hopefully I'll remember to update this after I figure that out. One I'll be testing is [here](https://www.aliexpress.com/item/1005003354425090.html?spm=a2g0o.productlist.0.0.1be3c46bK8VdfU&algo_pvid=7212a111-010b-4014-bd9d-2fe072e685d8&aem_p4p_detail=202201160149034875867301834480024840672&algo_exp_id=7212a111-010b-4014-bd9d-2fe072e685d8-4&pdp_ext_f=%7B%22sku_id%22%3A%2212000025369340509%22%7D&pdp_pi=-1%3B2.44%3B-1%3BUSD+2.38%40salePrice%3BUSD%3Bsearch-mainSearch)

The additional disk had a storage caddy available for it from Dell but I have not been able to track down that part number. There is however a 3D printable STL file on the Internet that I hope to try out and see if it fits or can be modded to fit. It says it's for an Optiplex so I'm not all that hopeful but images I have seen of the Wyse caddy don't look all that different. The STL file is [here](https://www.stlfinder.com/model/dell-optiplex-hhd-hard-drive-caddy-s579m5EN/2291325/) if you want to check it out.

## Networking

## Power

The 7010 and 7020 both use a 19V power supply, they're available on eBay or on [Amazon](https://www.amazon.com/APD-Adapter-Client-Class-Compatible/dp/B07PBMNH81)


## Other Resources

* https://www.parkytowers.me.uk/thin/wyse/z/zx0q/
