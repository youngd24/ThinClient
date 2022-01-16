# Wyse 7000 Series

## Overview

The Dell Wyse 7000 series consists of the 7010 and 7020 model. They are virtually the same with differences in the processor and video capabilities they come with. Details are available [here](https://www.dell.com/ae/business/p/wyse-z-class/pd). They're also referred to as the "z class" thin clients, the one I have examined is a Zx0 unit.

What you'll find here is all the info I have found, both by reading and by doing, as well as tips and tricks to hack it up to run various things, namely Linux.

## Background

A couple years back I wanted to delve into the world of home automation and IoT, mainly to see the real world effects of their security and practical methods to improve that.

I started with the basics, an Echo Dot and some smart bulbs and gradually grew out of those. I decided that I'd like to give Home Assistant a shot and see what that was made of. I started with HA on an ODROID-C2 I had laying around, it hung about every day and had to be hard powered off and on so I set it aside for a year or so. I then tried it on a Pi 3 that came out of a Pi 4 upgrade and while it seemed ok it was a bit slow and again it hung, usually when I compiled ESPHome firmware.

Someone on an ESPHome group had mentioned they were running HA on an old Dell Wyse thin client so I picked one up and here we are. If you're reading this in the future, beyond 2022, you'll remember the chip shortage we're in the midst of. Finding a Raspberry Pi 4 right now, at least at a reasonable cost, is difficult at best bordering on impossible. So, in theory, my idea was to leverage the lower cost of a thin client for applications where I would normally use a Raspberry Pi.

## Other Models

If someone can compare to the 5000 and 3000 series thin clients here it would be much appreciated.

## Specs

### Processor

I have found various data sheets for the 7020 that claim it carries a quad core AMD GX-420CA at 2.0 GHz however the 7020? (more on that later) that I purchased has the following for CPU:

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

The data sheet I was looking at [here](https://thinclientbenefits.com/uploads/products/downloads/Wyse-7020-Thin-Client-Data-Sheet.pdf) could be for a different version. Most of the eBay listings I see for the 7000's say they have the AMD dual-core CPU I have, at least one most of the 7010 listings. I have however seen eBay listings for what is claimed to be a 7010 with the quad-core and 7020's with the dual-core CPU.

Further research seems to indicate that the 7010 did in fact ship with the dual core AMD G-T56N @ 1.5GHz the weird part is when I put the service tag from the unit I have (with the G-T56N processor shows as a 7020 from Dell. There's also the z series model numbers that seem to not be all that different across the 7010 and 7020 units, the one I have carries a tag on it calling it a Zx0Q which in other places shows as a 7020.

End result: watch eBay listings carefully for the 7010 and 7020 models, as well as the ones saying Zx0 on them. Best as I can tell these shipped as:

* Wyse 7010 - Dual-Core AMD G-T56N @ 1.5GHz
* Wyse 7020 - Quad-Core AMD GX-420CA @ 2.0 GHz

Prices can be all over the map on eBay for these and in many cases the faster quad-core CPU doesn't gain much of a price increase. The dual-core unit is quite useable though I still need to pick up a quad-core 7020 to see for real.

## Memory

The 7010 I picked up came with 4GB RAM, all in (1) DDR-3 chip. There are 2 memory slots on the motherboard and the tech sheet says it can take up to 16GB RAM in (2) DDR-3 8GB chips. Even running a full Ubuntu desktop I'm using around half the memory it has installed but given the relatively low cost of DDR-3 memory a 16GB upgrade is in the near future.

## Display

You have to go into this remembering these things were made in 2015, 2016 and so on and targeted the average corporate "task worker" type user for virtual desktop computing. As a result the base units don't have much in the way of video and only has a DVI connector on it.

I've read that the 7020 had additional options for video, apparently in a daughter card, that could drive up to 4 monitors though I've never seen one like this. 2 ports would be helpful if being used as a workstation but for most headless embedded/dedicated use cases the DVI port will generally be sufficient and go unused.

## Storage

I'm speaking here on the 7010, that I have my hands on, but from what I have read it shares the same storage options as the 7020.

There is an onboard 2.5" SATA MLC flash chip, the original ones were made by Apacer and come in various sizes from 8 to 64GB. A laptop 2.5" SSD will **NOT** fit inside without major modifications. I would leave that alone and just buy a used one off eBay if need be. For most embedded/dedicated type operations, such as Home Assistant, 64GB, or even 32GB, is adequate. I'm writing this right now on the 7010 with a 32GB MLC flash chip running Ubuntu.

In addition to the onboard MLC connector there is an additional SATA II data port that can be used for additional storage. It's not a standard SATA connector, thanks Dell, the power connector is elsewhere on the board. That power connector is a Micro JST (MJST) 1.5mm 4-pin one so a custom cable will be needed to connect to the SATA drive. I just ordered one from Aliexpress to see how it can be made, hopefully I'll remember to update this after I figure that out. One I'll be testing is [here](https://www.aliexpress.com/item/1005003354425090.html?spm=a2g0o.productlist.0.0.1be3c46bK8VdfU&algo_pvid=7212a111-010b-4014-bd9d-2fe072e685d8&aem_p4p_detail=202201160149034875867301834480024840672&algo_exp_id=7212a111-010b-4014-bd9d-2fe072e685d8-4&pdp_ext_f=%7B%22sku_id%22%3A%2212000025369340509%22%7D&pdp_pi=-1%3B2.44%3B-1%3BUSD+2.38%40salePrice%3BUSD%3Bsearch-mainSearch). I am going to assume, for now, it is possible to **NOT** have the MLC installed and boot from the additional SATA disk, at least it _appears_ that way in the BIOS.

The additional disk had a storage caddy available for it from Dell but I have not been able to track down that part number, one of the resources at the end shows has a picture of it. There is however a 3D printable STL file on the Internet that I hope to try out and see if it fits or can be modded to fit. It says it's for an Optiplex so I'm not all that hopeful but images I have seen of the Wyse caddy don't look all that different. The STL file is [here](https://www.stlfinder.com/model/dell-optiplex-hhd-hard-drive-caddy-s579m5EN/2291325/) if you want to check it out.

## Networking

The 7000 series come with onboard Gigabit Ethernet and have an optional WiFi card in some models. The 7010 chassis has the holes for the antennas but no chip. There does appear to be a connector on the motherboard for this option so in theory you can add it later. I believe it's an Intel based chipset.

## USB

These have ample USB ports available, there are (2) USB-2 and (2) USB-3 ports on the back and (2) USB-2 ports on the front. Booting from them works as that's how I installed Ubuntu on it. Well, at least for Linux, haven't tested Windows yet.

## Power

### Connector

The 7010 and 7020 both use a 19V power supply, they're available on eBay or on [Amazon](https://www.amazon.com/APD-Adapter-Client-Class-Compatible/dp/B07PBMNH81). Personally, I would pick up the thin clients on eBay that come with the power supply and include that as part of the cost there. Adding in a new Amazon PS takes the cost up. There's also OEM ones on eBay for less than Amazon.

### Usage

One of the metrics I was curious about was the power used by the unit, is it comparable to a Raspberry Pi or similar? I plugged the 7010 into a Sonoff S31 that has power monitoring on it and fed that data to Home Assistant to monitor. Data to come but from what I can tell it's on par with a Pi 4 in usage.

## BIOS

The BIOS is very typical Dell, press DEL on the POST screen to enter setup mode, the default password is `Fireport`. You can adjust most of the settings here, I took the defaults and it's been fine since. I did notice that on the unit I was testing on, a 7010 without wireless, there was an option to enable the on-board WiFi despite me not finding a chip on the motherboard anywhere.

## Cost

I picked up the 7010 I have, new in the box, with the power supply, stand, mouse and DVI to VGA adapter for $29.99 plus $9 shipping, call it $40. It came with 4GB RAM and no MLC flash storage so I purchsed a 32GB MLC for $18 with free shipping. So, as of today, the cost comes to:

* 7010 4GB RAM - $40
* 32GB MLC flash - $18

__Estimated total cost: $58__

Here's a proposal for a fairly packed system:

* 7020 4GB RAM - $60
* 16GB DDR-3 RAM - $60
* 64GB MLC flash - $40
* 2TB SATA SSD - $90

__Estimated total cost: $250__

That's a bit on the high side for me personally, you're more than half way into a NUC at that point though with this chip shortage it might become even more attractive down the road. Personally I would stick to use cases where 4-8GB RAM and 32-64GB MLC flash is sufficient, that will keep the cost in the $100-125 area, comparable to a Pi kit. There's probably a middle-ground where you bump the RAM _or_ the disk for a given use case.

## Operating Systems

### Linux

Thus far the only OS I have tried is Ubuntu 20.04 LTS, installation was as easy as formatting a USB key (FAT/GUID partition map) on my Mac, downloading the Ubuntu 20.04 ISO and burning it to the USB key using Balena Etcher. I put the USB key in and on boot the BIOS detected no OS on the internal MLC flash and booted straight to the USB key. From there it was an uneventful Ubuntu installation.

### Windows 10

Under construction.

## Use Cases and Ideas

### k3s

A few of these would make a nice little k3s Kubernetes cluster. I have run k3s on Raspberry Pi's however the issue I hit was almost always the fact that most of the container suppliers didn't have arm processor builds available. What's messed up is that k3s doens't tell you it can't run the container, it allows you to deploy it and fail victoriously. With the 7000 series AMD x86_64 architecture this won't be an issue. Then there's the fact it has a gigabit ethernet port, not 100MB like a Pi 3, so you get faster networking. Not sure how well the little AMD CPU would keep up with full-chugging network I/O but it's likely more performant than a Pi 3 is.

### Network Attached Storage (NAS)

It _might_ work ok for this, the gig-e networking port is an upside though only 1 is a ding against it. You can't fit much in the way of disk inside with the single 2.5" SATA disk port. Given there's external USB-2 ports it might be possible to attach a few external USB-SATA disks and serve those out over CIFS/NFS. Maybe, YMMV.

### Home Assistant

Works great, doing it now. More to come in a page dedicated to just that.

### Plex Media Server

The quad-core 7020 version _might_ do ok for that, again, a bit maybe. I have it running on a Pi 4 and it works decently for 1 stream decode though it's a bit slow for that. I might test this out when I get a 7020 and see how it does.

### Octoprint

I suspect it would work wonderfully for Octoprint on your 3D printer though I really like having a Pi 3 for that. It's small enough it can be mounted right on the 3D printer and not have a lot of extra cabling laying around. A 7000 in this use case would be a bit messy on the cabling side.

### Container Host

If you bump the RAM and add an internal disk, say 1-2TB, the quad-core 7020 would make a good little container host machine. Could easily put 3 or more of them into a Docker Swarm and avoid all the Kubernetes complexity.

## Conclusion

Overall it's a decent little machine, especially given what the cost is. It would certainly work as a "daily driver" running Ubuntu for the average  user (think grandma). Windows 10 is a little sluggish on the 7010 (surprise), it might be better on the 7020 with 4 cores along with additional RAM.

As a dedicated/embedded machine for things that don't require a ton of power, that just just sit there and run, it's ideal. If you need more than what the 7000 can do, in either the 7010 or 7020 models, I wouldn't invest much in upgrades and instead opt for a NUC. If you're investing more than $150 in a thin client it's probably a use case that would benefit from more than what the 7000 offers. It really all depends on what you're doing but consider this as an option in your toolkit.

## Other Resources

- [Parky Towers](https://www.parkytowers.me.uk/thin/wyse/z/zx0q/). Great site with all sorts of thin client info, I found the information there quite helpful.
- YouTube videos
	- [Wyse Thin Client Rx0L Teardown](https://www.youtube.com/watch?v=JOrZVa5QehY)
	- [Was it wise to buy the Wyse?](https://www.youtube.com/watch?v=oy6g3zaD4Jc)
	- [Wyse thin client review and demo](https://www.youtube.com/watch?v=gGgBp9N6Vco)
