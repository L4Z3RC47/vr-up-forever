# vr-up-forever
This is an article with tips about how to keep a VR installation up forever

Inspired by Installation_Up_4evr by [laserpilot](https://github.com/laserpilot)

## Table of Contents
1. [Introduction](#introduction)
1. [Building a computer](#building-a-computer)
    * [Oculus minimum specs](#oculus-minimum-specs)
    * [HTC minimum specs](#htc-minimum-specs)
1. [Setting up your computer](#setting-up-your-computer)
1. [Setting up your software](#setting-up-your-software)
    * [Oculus Rift](#oculus-rift)
    * [HTC Vive](#htc-vive)
1. [Hardware Considerations](#hardware-considerations)
    * [Oculus](#oculus)
    * [Vive](#vive)
1. [Useful Links](#useful-links)
    * [Software](#software)
    * [Hardware](#hardware)
    * [Code examples](#code-examples)
1. [Contributing](#contributing)

## Introduction

This document is intended to serve as a general guide for setting up unattended VR installations. There are many different possible configurations depending on your needs. If you have suggestions please feel to submit contributions!

As of this writing msot VR installations are confined to the PC realm so this guide is going to stay focused on Windows configuration for now. It would be great to get a linux section started too. Currently Apple hardware does not officially support the major VR hardware. If Apples hardware gets updated and drivers are made for macOS I'll update this guide to include configurations for those machines as well.

## Building a computer

There are now many different options available when looking for VR compatible machines, including laptops from manufacturers such as MSI and Asus. That being said, I prefer to build my own machines. There's a certain level of comfort when installing a computer that I've built where I know exactly what all of the components are, and exactly what software is installed. Not to say that off the shelf computers are less reliable, its just my personal preference. When building your own machine its also likely that you'll be able to save a bit of money, and if you've never built a computer before you'll learn a lot in the process :)

Building a PC is often a balance between performance and cost of components. Currently my preferred specs are:

* CPU: Intel i7 6700K Skylake 4Ghz
* GPU: MSI GTX 1070 Founder Edition
* RAM: 16GB G.Skill Ripjaws V Series DDR4 2400
* Memory: Samsung 850 EVO 120GB SSD
* Motherboard: Asus Maximus Gene VIII (mATX) LGA 1151
* PSU: CORSAIR RM750X
* Wireless card (optional): TP-LINK TL-WDN4800 Wireless N900 PCI Express Adapter.
* Case: Bitfenix Prodigy Micro ATX
* CPU Fan: CORSAIR Hydro Series H50 120mm CPU Cooler

Both Oclus and HTC also provide their own minimum supported specs. If your installation is minimal you should be able to get by but if possible its always best to test if on the hardware you're planning on using before buying if possible.

#### Oculus minimum specs

* CPU: Intel i3-6100 / AMD FX4350 or greater
* GPU: Nvidia 960 / AMD 290 or greater : Compatible HDMI 1.3 video output
* RAM: 8GB+
* 1x USB 3.0, 2x USB 2.0
* OS: Windows 8 or newer

Oculus also has a page listing 'Oculus ready PCs' [here](https://www.oculus.com/oculus-ready-pcs/).

#### HTC minimum specs

* CPU: Intel™ Core™ i5-4590 or AMD FX™ 8350, equivalent or better
* GPU: NVIDIA GeForce™ GTX 1060 or AMD Radeon™ RX 480, equivalent or better : Video output: 1x HDMI 1.4 port, or DisplayPort 1.2 or newer
* RAM: 4 GB or more
* USB: 1x USB 2.0 port or newer
* OS: Windows™ 7 SP1, Windows™ 8.1 or later or Windows™ 10

HTC also posts their current minimum specs and links to some hardware [here](https://www.vive.com/us/ready/).

## Setting up your computer




## Setting up your software


#### Oculus Rift

Currently when running an Oculus application you must also run the Oculus home application. When launching your app this unfortunately means that often times Oculus home will open and take focus on your main display if you are using one to mirror content outside of the headset. To get around this we setup a simple batch script to ensure that we launch Oculus home first, followed by our application.

#### HTC Vive


## Hardware Considerations


#### Oculus


#### Vive


## Useful Links


#### Software


#### Hardware

* [Xbox One Controller Tether](https://www.lockdownmycontroller.com/collections/lockdown-anti-theft-hardware-for-xbox-one/products/xbox-one-controller-anti-theft-system-permanent-installation) This security tether is a minimal security case and does a decent job of securing the USB cable to the controller so it does't fall out. To prevent users from pressing the 'home' button which will trigger the Oculus home app we were able to epoxy a small piece of metal to the inside of the case over the button.


#### Code Examples


## Contributing

If you'd like to contribute to this project, please fork
the repository and make your changes in a separate branch.

```bash
git clone https://github.com/wjrro/vr-up-forever.git .
cd aic-project
git flow start feature yourinitials-good-description-issuenumberifapplicable
# Make some changes, commit your code
git push origin yourinitials-good-description-issuenumberifapplicable
```

Then on github.com, create a Pull Request to merge your changes into the
`master` branch.
