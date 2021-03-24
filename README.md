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
      <td>Controller</td>
      <td>Realtek ALC3246/256 (layout-id: 11)</td>
    </tr>
    <tr>
    </tr>
  </tbody>
</table>

## Instructions

You **must** add your own serialnumber. I recommend [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). Remember to use `MacBookPro14,1`. 

Use this a a starting point, this is no replacement of your own research, trial and error.



## What is working

### Completely supported

#### CPU

XCPM power management is native supported. HWP is fully enabled as well.

#### Wi-Fi & Bluetooth

This laptop comes with an Intel WiFi + Bluetooth combo so, I replaced mine with BCM94352Z (DM1560). Airport, Handoff are working correctly.

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

Audio and microphone works, but headphone jack requires a workaround.

Driven by AppleALC with `layout-id: 11`. Working fine but headphone jack requires a workaround and is not detected by default (HDMI Audio output has not been tested).

Built-in mic is working

#### Keyboard

Fn Keys not working. Also strange behavior sometimes after waking up, see Sleep.

#### Touchpad

Functioning with multigestures, but sometimes "teleports" doing certain gestures.

#### Headphone jack

Requires a workaround and is not detected.

#### Sleep and Wake

Working but sometimes weird behavior ensues. Example, if a key if pressed when waking up, the keyboard will stop working correctly, and the key pressed will repeat indefinitely in the password field, and touchpad stops working.

### Not working

#### Others

Internal SD card Reader

### Not tested

HDMI output

## Additional info, quirks, findings, etc 

Remove kexts asociated with BCM94352Z(DW1560) if you do not have installed one.

`CtlnaAHCIPort` is absolutely necesary to Big Sur. Using `MinKernel` this kext only loads in BirSur 

AirPortBrcm4360 only loads in Catalina (using `MaxKernel` = `19.9.9`). This kext makes Big Sur unable to boot.

## Changelog

##### 23/mar/2021:

Added and updated a ton of kexts.

Updated to OpenCore 0.6.7

Big Sur now working (yay)!

Audio now works via `DeviceProperties` -> `Add` -> `PciRoot(0x0)/Pci(0x1F,0x3)`-> `layout-id` = `11`

##### 26/nov/2020: 

Removed: `XHCI-unsupported.kext`because is not needed

Added: `SMCDellSensors.kext`, `SMCProcessor.kext`, `SMCSuperIO.kext`for CPU and fan sensor support

Fixed: Wrong iGPU in `DeviceProperties`

Updated: Sleep and Wake findings

##### 25/nov/2020: 

First release

