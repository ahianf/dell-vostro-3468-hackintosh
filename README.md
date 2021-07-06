<h1>macOS Catalina/Big Sur on Dell Vostro 3000 series using OpenCore</h1>
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
      <td>Intel Core i5 7200U</td>
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

XCPM power management is native supported. HWP is fully enabled as well.

#### Wi-Fi & Bluetooth

This laptop comes with an Intel WiFi + Bluetooth combo so, I replaced mine with BCM94352Z (DM1560). Airport, Handoff are working correctly.

###### Important: If you have an Intel card, remove BCM-related kexts and start from there.

#### Camera

Camera is functioning normally.

#### USB

USB ports are working as expected.

Use USBInject-All.kext then with Hackintool disable all unused ports and generate a USBPorts.kext

#### Ethernet

Functioning normally.

#### Display

Working fine with hardware acceleration.

#### Battery

Detected and correct values.

#### Sensors

Fan Speed, CPU temp and voltage.

### Partially working

#### Keyboard

Fn Keys not working. Also strange behavior sometimes after waking up, see Sleep.

#### Touchpad

Functioning with multigestures, but sometimes "teleports" doing certain gestures.

#### Sleep and Wake

Working but sometimes weird behavior ensues. Example, if a key if pressed when waking up, the keyboard will stop working correctly, and the key pressed will repeat indefinitely in the password field, and touchpad stops working.

A workaround i've found is when the laptop wakes from sleep, do not press any key inmediately, wait 5-10 seconds to start using the keyboard, that works for me, but sometimes the touchpad just quits.

### Not working

#### Others

Internal SD card Reader

### Not tested

HDMI output

## Additional info, quirks, findings, etc 

`CtlnaAHCIPort` is absolutely necesary to Big Sur. Using `MinKernel` this kext only loads in BirSur 

AirPortBrcm4360 only will load in Catalina (using `MaxKernel` = `19.9.9`). This kext makes Big Sur unable to boot.

## Changelog

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
