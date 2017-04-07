# vr-up-forever
This is an article with tips about how to keep a VR installation up forever

This doc is a work in progress and I'll continue to add new things as they come up. If you have questions feel free to tweet me [@WJRRo](https://twitter.com/wjrro)

Inspired by Installation_Up_4evr by [laserpilot](https://github.com/laserpilot)

## Table of Contents
1. [Introduction](#introduction)
1. [Building a computer](#building-a-computer)
    * [Oculus minimum specs](#oculus-minimum-specs)
    * [HTC minimum specs](#htc-minimum-specs)
1. [Setting up your computer](#setting-up-your-computer)
1. [Setting up your software](#setting-up-your-software)
    * [Unity 3D apps](#unity-3d-apps)
        * [Installation with a mirrored monitor](#installation-with-a-mirrored-monitor)
            * [Configuring an attract screen](#configuring-an-attract-screen)
    * [Unreal Engine apps](#unreal-engine-apps)
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

This document is intended to serve as a general guide for setting up unattended VR installations. There are many different possible configurations depending on your needs. A lot of this doc is compiled from my experience setting up installations for [DiMoDA](https://dimoda.art). If you have suggestions please feel to submit contributions!

As of this writing most VR installations are confined to the PC realm so this guide is going to stay focused on Windows configuration for now. It would be great to get a linux section started too. Currently Apple hardware does not officially support the major VR hardware. If Apples hardware gets updated and drivers are made for macOS I'll update this guide to include configurations for those machines as well.

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
* OS: Windows 10 (64)

Both Oculus and HTC also provide their own minimum supported specs. If your installation is minimal you should be able to get by but if possible its always best to test if on the hardware you're planning on using before buying if possible.

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

#### Free and minimal


#### Not free but easy


## Setting up your software

#### Unity 3D apps

There are several different settings and configurations that you can setup when compiling your application. For the purposes of this documentation I will cover basic configurations for the two most common types of installation, one with a monitor mirroring the content on the headset and a 'headless' installation with just the VR headset.

##### Basic Setup

1. Download and import the [Oculus Utilites for Unity](https://developer.oculus.com/downloads/package/oculus-utilities-for-unity-5/)

  You don't necessarily need to use any of these tools but they will come in handy later down the line. Additionally if you want to host your app on the Oculus store then you'll need to use Oculus' utilities to verify your application on launch.

1. In the player settings in your Unity project under 'Resolution and Presentation' set 'Display Resolution Dialog' to 'Disabled'. This prevents the resolution dialog from popping up when you start your application on launch which can get in the way when trying to automate your startup and shutdown of an installation.

    ![Unity Resolution and Presentation Example](images/unity_resolution_and_presentation.png)

    Then in 'Other settings' make sure that the 'Virtual Reality Supported' box is checked.

    ![Unity Other Settings Example](images/unity_other_player_settings.png)

##### Installation with a mirrored monitor

Generally I prefer to run installations with a monitor for several reasons. First, this makes setup and configuration a lot easier. It can be very difficult to next to impossible to troubleshoot issues if you only have a VR headset as a display. If you're physically with the machine its also much quicker to interface with the machine directly if you can rather than relying on Remote Desktop or a VNC like solution. Additionally I find that having a monitor makes your users experience a bit more social so that other users/visitors can watch alongside as the person in the headset goes through the VR experience.

###### Handling headset removed

Most likely you'll want to trigger some event or switch scenes based on whether someone is wearing your headset or not. You can easily manage these events with the OVRManager which is a part of the Oculus Utilities package. Its best not to modify these scripts so instead we'll setup a delegate to handle the calls in our own script.

You'll need to attach an OVRManager script to one object in your scene. You can only have one OVRManager in a scene. Its best to attach this object to something that will not get destroyed when you load another scene.

```C#
using UnityEngine;

// Uncomment if you want to switch scenes based on the headset status.
// using UnityEngine.SceneManagement;

public class OVRHeadsetDelegate : MonoBehaviour {


	void OnEnable () {

		OVRManager.HMDMounted += HandleHMDMounted;
		OVRManager.HMDUnmounted += HandleHMDUnmounted;

	}

	void OnDisable () {

		OVRManager.HMDMounted -= HandleHMDMounted;
		OVRManager.HMDUnmounted -= HandleHMDUnmounted;

	}

	void HandleHMDMounted() {

		Debug.Log("HMD Mounted");

    // Trigger something here

	}

	void HandleHMDUnmounted() {

		Debug.Log("HMD UnMounted");

    // Trigger something here

	}
}
```

###### Configuring an attract screen

By default rendering will stop and you'll get either a paused game screen or just black on your external monitor when the headset is not mounted (on someones head). To get around this you'll need to modify the OVRManager script to allow for running in the background. To do this find the 'runInBackground' bool and set it's value to 'true'

``` C#
internal static bool runInBackground = true;
```
Now when you run your app when the headset is removed the Oculus headset will turn off its display but your external monitor will continue running! From there you can use the OVRHeadsetDelegate script from above to manage loading a scene with a video or a slideshow to use as an attract screen for your experience.

** Tip! ** <br>
When transitioning between scenes I find that its less jarring for your players/users/visitors to first fade out. Oculus provides a fading utility as a part of the Oculus Utilities that you can use but it must be modified to enable fading both in and out. I've uploaded my implementation of this script INSERT LINK. Using this script you can trigger a fade and then use the fade time to delay triggering your scene change.

##### Headless installation

More info coming soon!

#### Unreal Engine apps

More info coming soon!

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
