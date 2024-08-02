# CZC Chimera Patch for Official Driver

Customised official GK68XPlus driver to recognise CZC Chimera rebranded [SKYLOONG GK68X/GK68XS Kit](https://epomaker.com/products/gk68xs-kit?variant=31744262176841)

Official [CZC Chimera](https://www.czc.cz/software-czc-gaming-chimera/priloha) driver / 
Official [Windows](http://www.jikedingzhi.com/downloadlist?driverID=103) driver / 
Official [MacOS](http://www.jikedingzhi.com/downloadlist?driverID=90) driver

Official installer are also located in this repo for emergency cases. e.g. CZC goes out of business

## Quick Start

 1. Download and Install *Official* driver as usual (e.g GK6XPlus V8 on Windows)
 2. Modify the driver to handle *Chimera* keyboard as GK68X/GK68XS Kit
 2.1. On Windows go into folder `C:\Program Files\GK6+\resources` and replace `app.asar` file with the patched one from this repository (unzip it first)
 2.2.  On MacOS go into folder `/Applications/GK6+.app/Contents/Resources/app/src/drivers` and replace `cor-m3-mk.js` file with the patched one from this repository 
 3. Enjoy customising your CZC Chimera keyboard newly on Windows 11 and MacOS
	
## Overview

What the patch actually does is, when the driver finds the rebranded unsupported keyboard from CZC, it treats it as a GK68X/GK68XS.

 - GK68X - **?** CZC.Gaming Chimera **?**
 - GK68XS - **?** CZC.Gaming Chimera Wireless **?**

### Supported versions

The patch was created at the time when the last version was:

 - for **Windows** GK6XPlus V8 V8.0.6.0 
 更新时间：2024-06-14
 
 - for **MacOS** GK6+Mac App V1.0.0.26
 -更新时间：2024-06-14

I assume that this patch will also work for future versions

## What I did?

I have simply edited the `cor-m3-mk.js` file by adding if statements to rewrite *FWID* and *ModelID* if those are the ones from CZC.

    if (FWID === 2485223445 || FWID === 2535555092) {
	    FWID = 2535555089;
    }

    if (ModelID === 656802019 || ModelID === 656802020) {
	    ModelID = 656801834;
    }

I know that from `modellist.json` file and folders in `C:\Program Files (x86)\CZC Driver\CMSEngine\driver\device`

## Notes

 - I have only tested CZC.Gaming Chimera Wireless

 - For Windows users -  `app.asar` is just an pack file, so i unpack it using this [help](https://stackoverflow.com/questions/38523617/how-to-unpack-an-asar-file), then modify `cor-m3-mk.js` and pack it back

 - If you look at the `modellist.json` file in the CZC driver, for some reason it treats the ModelID *656802020* as GK68XS (you can see that in `C:\Program Files (x86)\CZC Driver\CMSEngine\driver\device\656802020\data\profile*.json`). My CZC.Gaming Chimera Wireless has ModelID *656802019*, which I assume *656802020* is GK68XS, but I have no confirmation, so I'll leave it as CZC has it

 -  I tried to modify `modellist.json` and add folders *656802019, 656802020*, but the application did not work properly
