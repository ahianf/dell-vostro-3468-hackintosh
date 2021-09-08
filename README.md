<h1>macOS Catalina/Big Sur on Dell Vostro 3000 series using OpenCore</h1>

![dzfgv](https://user-images.githubusercontent.com/37314164/127522651-94c034cb-848d-43b6-9519-7aca059e20c0.png)
![Captura de Pantalla 2021-07-29 a la(s) 11 12 00 a  m](https://user-images.githubusercontent.com/37314164/127522694-d163089f-451b-4621-840c-5d62fa7ee522.png)



## Important

This repo has a lot of things specific to my laptop, for example all the ACPI tables. It should work in a identic computer, but maybe it won't.

## Instructions

You **must** add your own serialnumber. I recommend [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). Remember to use `MacBookPro14,1`. 

Use this a a starting point, this is no replacement of your own research, trial and error.

Remove kexts asociated with BCM94352Z(DW1560) if you do not have installed one, and do a OCSnapshot in ProperTree to remove them from config.plist.

**Important:** You MUST remove the wifi card from the motherboard, fail to do so will result in bizarre kernel panics during installation, after that you can reinstall again the card.

## What is working

### Completely supported

#### Audio

Audio on speakers and headphones works as intended.

#### CPU

XCPM power management is native supported. HWP is fully enabled as well. Added cpufriend for more energy savings.

#### Wi-Fi & Bluetooth

This laptop comes with an Intel WiFi + Bluetooth combo so I replaced mine with BCM94352Z (DM1560). 
Airport, Handoff are working correctly.

###### Important: If you have an Intel card, remove BCM-related kexts, rescan with ProperTree and start from there.

#### Camera

Camera is functioning normally.

#### USB

USB ports are working as expected.

Use USBInject-All.kext then with Hackintool disable all unused ports and generate a USBPorts.kext

#### Ethernet

Functioning normally.

#### Display and External Monitors

Working fine with hardware acceleration. External monitors work fine with HDMI or VGA.

#### Battery

Detected and correct values.

#### Sensors

Fan Speed, CPU temp and voltage.

#### Touchpad

Functioning with multigestures.

### Partially working

#### Keyboard

Brightness keys not working. Also strange behavior sometimes after waking up, see Sleep.

#### Sleep and Wake

Sometimes weird behavior happens. Example, if a key if pressed when the laptop is waking up from sleep, the keyboard will stop responding, and the key pressed will repeat indefinitely in the password field, the touchpad also dies.

A workaround i've found is when the laptop wakes from sleep, do not press any key inmediately. Wait 5-10 seconds then start typing, that works for me, but sometimes the touchpad just quits anyway.

### Not working

#### Others

Internal SD card Reader


## Additional info, quirks, findings, etc 

`CtlnaAHCIPort` is absolutely necesary to Big Sur. Using `MinKernel` this kext only loads in BirSur 

AirPortBrcm4360 only will load in Catalina (using `MaxKernel` = `19.9.9`). This kext makes Big Sur unable to boot.

When updating, in order to use VoodooI2C without issues, delete `VoodooInput.kext` from `VoodooPS2Controller.kext/Contents/PlugIns/`.

<h2>Laptop Specs</h2>
<table>
  <thead>
    <tr>
      <td style="text-align: center">Feature</td>
      <td style="text-align: center">Specification</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Model</td>
      <td>Dell Vostro 3468</td>
    </tr>
    <tr>
      <td>Processor type</td>
      <td>Intel Core i5-7200U</td>
    </tr>
     <tr>
      <td>VGA</td>
      <td>Intel HD Graphics 620</td>
    </tr>
    <tr>
      <td>Audio</td>
      <td>Realtek ALC256 (layout-id: 21)</td>
    </tr>
    <tr>
    </tr>
  </tbody>
</table>


![Captura de Pantalla 2021-07-29 a la(s) 11 16 00 a  m](https://user-images.githubusercontent.com/37314164/127522685-8d8b5791-a97b-41ec-ba6d-51e70ba82f12.png)

![Captura de Pantalla 2021-07-29 a la(s) 11 17 04 a  m](https://user-images.githubusercontent.com/37314164/127522701-539e44bc-73d7-4426-a8cf-9eee6fdcd7f6.png)

![Captura de Pantalla 2021-07-29 a la(s) 11 16 35 a  m](https://user-images.githubusercontent.com/37314164/127522708-c5c77309-7c38-400f-8c13-59466aade2e3.png)

## Changelog

##### 08/sep/2021:

Updated to OpenCore 0.7.2

Replaced ACPI files with my own compiled for my specific config. 

Framebuffer: Added missing entries and removed unused patches.

Added CPUfriend, now CPU goes below 1300MHz, this should improve battery life.

##### 06/sep/2021:

Now trackpad works using VoodooI2C, with a lot better experience using touchpad

Updated to OpenCore 0.7.2

Now completely cosmetic, no verbose or debug messages.

OCvalidator shows no errors anymore.

Switch from ugly XOSI to GPI0 for trackpad. 

##### 06/jul/2021:

Updated to OpenCore 0.7.1

Kexts updated

##### 08/jun/2021:

Updated to OpenCore 0.7.0

Kexts updated

Audio headphone jack fixed!  Problem was incorrect layout-id (correct is `layout-id` = `21`)

##### 23/mar/2021:

Updated to OpenCore 0.6.7

Added and updated a ton of kexts.

Big Sur now working (yay)!

Audio now works via `DeviceProperties` -> `Add` -> `PciRoot(0x0)/Pci(0x1F,0x3)`

##### 26/nov/2020: 

Removed: `XHCI-unsupported.kext`because is not needed

Added: `SMCDellSensors.kext`, `SMCProcessor.kext`, `SMCSuperIO.kext`for CPU and fan sensor support

Fixed: Wrong iGPU in `DeviceProperties`

Updated: Sleep and Wake findings

##### 25/nov/2020: 

First release
