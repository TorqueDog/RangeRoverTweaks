---
title: Tips and Tweaks for the L405 and L320
author: TorqueDog
description: Tips and Tweaks for the L405 Range Rover and L320 Range Rover Sport
---

# Tips and Tweaks for the L405 Range Rover and L320 Range Rover Sport
A small corner of the internet where I document the interesting and useful things I've learned with my L405 Range Rover and previous L320 Range Rover Sport.
<br /><br />

# List of RR stuff

[What's this all about?](#whats-this-all-about)

[A word on the vehicle Car Config File](#a-word-on-the-vehicle-car-config-file)

[What tools are required?](#what-tools-are-required)

[I'm not six, I know to put my seatbelt on, stop BONG-ing at me!](#im-not-six-i-know-to-put-my-seatbelt-on-stop-bong-ing-at-me)


<br />

## What's this all about?

Since about 2002, Land Rovers have gotten increasingly more complex. More modules for more things, more ways to control how the vehicle behaves, how equipment is enabled/disabled, and so on. The L405 Range Rover is a great example of how just a bit of software tweaking can add a good deal of customization and features.

<br />

## A word on the vehicle Car Config File

A lot of these things require changes to the vehicle's **Car Config File** or **CCF**. The CCF is a vital piece of the vehicle's operating instructions. Making the wrong changes could prevent your car from working properly, possibly even brick the damn thing and require an expensive trip to the dealer. Anything CCF changes you find here, you perform on your own vehicle **at your own risk**.  

Stupid reasons to make CCF changes:  
- A value is set to **Undefined** but there is a value in the list that matches your vehicle.  
&bull; Did your car work properly without it? Then it doesn't need it, and there's more risk in you adding it for zero gain. Leave it be, the car doesn't need it.
- I was curious what it did.  
&bull; Ugh, just close the browser tab before you wreck something. Okay, not entirely fair, some of these things *were* learned through my own trial-and-error, but don't blame me if you FA&FO with your expensive British luxobarge.

<br />

## What tools are required?

You have three options, year-dependent:  
- *Jaguar/Land Rover Symptom Driven Diagnostics* software with a *JLR Mongoose OBD-II* interface (henceforth referred to as simply **SDD**)  
&bull; Works on MY2016.5 and earlier only. I sold mine to a friend who bought my L320.
- *Jaguar/Land Rover Pathfinder* software with the correct OBD-II interface cable (henceforth known as **Pathfinder**)  
&bull; I don't have Pathfinder and know nothing about it. You're on your own.  
- *GAP IID Tool*, either BT or Pro, with the correct version for your year of Land Rover  
&bull; G3 for vehicles up to MY2016.5  
&bull; G4 for vehicles MY2017 and later  
 
<br />

## I'm not six, I know to put my seatbelt on, stop BONG-ing at me!

*Before we begin:* Lest anyone crawls up my arse for enabling people to drive around without their seatbelt by sharing this, please heed the following: **go away**. If someone is going to do this, they've already bought a seatbelt extender and left it plugged in. For my part, I don't even like *putting the car in gear* without having my seatbelt on, my parents having obviously done a bang-up job making sure that was instilled in me early on. But that's just it... I do it out of habit, the annoying BONG-ing noise only serves to irritate me, not inform behaviour. For that reason, it's got to go.

The L322 Range Rover, L320 Range Rover Sport, and L319 Discovery 3/LR3 had an easy solution for those of us who didn't enjoy getting nagged about putting on their seatbelt every time the vehicle started. What you did is you buckled and unbuckled the seatbelt ten (10) times while the key was in the 'Run' (or 'On') position. After the tenth time, the seatbelt nanny chime was disabled. To re-enable it, just repeat the process. In the L405 (after MY2013 I think), this procedure stopped working. It would disable the visual representation in the instrument cluster of who did and didn't have their seatbelt on (which is quite useful), but the car would still incessantly BONG at you.

The solution is to program it out of the car's Car Config File (CCF).  

> **Warning:** This may be illegal in your area, or at the very least will be cause for a FAIL on a safety inspection. This *not only* disables the audible nagging but also the **seatbelt lamp in the cluster**, though -- again -- the graphical "who isn't wearing their seatbelt" tattle-tale screen shows in the cluster.

Using either IID Tool or SDD, you'll need to edit the car config file. For IID Tool users, GAP will need to grant you access to the "Complete CCF". Out of the box, you'll only see 'Confirmed CCF' and it's a fraction of a fraction of what the entire CCF contains. Send them an e-mail stating you want full access to the CCF and you accept the responsibility if you screw up your car, and they can do it for you.
