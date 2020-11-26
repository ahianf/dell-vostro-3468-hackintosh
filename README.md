<h1>MacOS on Dell Vostro 3000 series using OpenCore</h1>
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



## What is working

### Completely supported

#### CPU

XCPM power management is native supported. HWP is fully enabled as well.

#### Wi-Fi & Bluetooth

This laptop comes with an Intel WiFi + Bluetooth combo. I replaced mine with BCM94352Z (DM1560). Airport, Handoff are working correctly.

#### Camera

Camera is functioning normally.

#### USB

USB ports are working as expected.

Use USBInject-All.kext then with Hackintool you should disable all unused ports and generate a USBPorts.kext

#### Ethernet

Functioning normally.

#### Display

Working fine with hardware acceleration.

#### Audio

Driven by AppleALC with `layout-id: 11`. Working fine but headphone jack requires a workaround and is not detected by default (HDMI Audio output has not been tested).

Built-in mic is working

### Partially working

Audio and microphone works, but headphone jack requires a workaround.

#### Keyboard

Functioning except the AltGr key, (which I don't know how to map it correctly) and Fn Keys.

#### Touchpad

Functioning with multigestures, but not detected in System Settings -> Touchpad

#### Headphone jack

Requires a workaround and is not detected.

#### Sleep and Wake

Working but weird behavior. Example, if a key if pressed when waking up, the keyboard will stop working correctly, and the key pressed will repeat indefinitely in the password field. A workaround is to press first the backspace key.

Also Bluetooth freezes frecuently macOS when waking up, in fact is impossible to use Bluetooth audio after sleep.

### Not working

#### Battery

Battery readings not working as ACPI not been patched yet.

#### Others

Internal SD card Reader

### Not tested

HDMI output

## Additional info, quirks, findings, etc 

Remove kexts asociated with BCM94352Z(DW1560) if you do not have installed one.

## Changelog

##### 26/nov/2020: 

Removed: `XHCI-unsupported.kext`because is not needed

Added: `SMCDellSensors.kext`, `SMCProcessor.kext`, `SMCSuperIO.kext`for CPU and fan sensor support

Fixed: Wrong iGPU in `DeviceProperties`

Updated: Sleep and Wake findings

##### 25/nov/2020: 

First release

