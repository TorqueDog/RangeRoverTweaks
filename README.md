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

[Firing the Seatbelt Nanny](#firing-the-seatbelt-nanny)

[Letting the air out of Speedometer Inflation](#letting-the-air-out-of-speedometer-inflation)

[New shoes, different size - calibrating for different tyre sizes](#new-shoes-different-size---calibrating-for-different-tyre-sizes)

[Adding some athleticism to the big pudding - enabling Dynamic Terrain Response](#adding-some-athleticism-to-the-big-pudding---enabling-dynamic-terrain-response)


<br />

## What's this all about?

Since about 2002, Land Rovers have gotten increasingly more complex. More modules for more things, more ways to control how the vehicle behaves, how equipment is enabled/disabled, and so on. The L405 Range Rover is a great example of how just a bit of software tweaking can add a good deal of customization and features.

This repo focuses mainly on **2013-2017 L405 Range Rover**, and occasionally will mention things of value to **2006-2009 L320 Range Rover Sport**. Some of the L405 stuff may apply to L494 Range Rover Sport, but I can't confirm it. Feel free to reach out if any of it does and I'll make a note of it here.

<br />
<hr>
<br />

## A word on the vehicle Car Config File

A lot of these things require changes to the vehicle's **Car Config File** or **CCF**. The CCF is a vital piece of the vehicle's operating instructions. Making the wrong changes could prevent your car from working properly, possibly even brick the damn thing and require an expensive trip to the dealer. Any CCF changes you find here, you perform **at your own risk**.  

Stupid reasons to make CCF changes:  
- A value is set to **Undefined** but there is a value in the list that matches your vehicle.  
&bull; Did your car work properly without it? Then it doesn't need it, and there's more risk in you adding it for zero gain. Leave it be, the car doesn't need it.
- I was curious what it did.  
&bull; Ugh, just close the browser tab before you wreck something. Okay, not entirely fair, some of these things *were* learned through my own trial-and-error, but don't blame me if you FA&FO with your expensive British luxobarge.

<br />
<hr>
<br />

## What tools are required?

You have three options, year-dependent:  
- **SDD** - *Jaguar/Land Rover Symptom Driven Diagnostics* software with a *JLR Mongoose OBD-II* interface  
&bull; Works on MY2016.5 and earlier only. I sold mine to a friend who bought my L320.
- **Pathfinder** - *Jaguar/Land Rover Pathfinder* software with the correct VCI and OBD-II interface cable  
&bull; I don't have Pathfinder, none of my Rovers ever needed / supported it, and I know nothing about it. In short, you're on your own.  
- **IID** - *GAP IID Tool*, either BT or Pro, with the correct version for your year of Land Rover  
&bull; G3 for vehicles up to MY2016.5  
&bull; G4 for vehicles MY2017 and later  
&bull; In either instance, you'll need to contact GAP ahead of time and ask them for access to the Complete CCF file.
 
<br />
<hr>
<br />

## Firing the Seatbelt Nanny

> *Dear cars I own;  
> I'm not six, I know to put my seatbelt on before driving, now stop BONG-ing at me!  
> Sincerely, Me*  

*Before we begin:* Lest anyone crawls up my arse for enabling people to drive around without their seatbelt by sharing this, please heed the following: **go away**. If someone is going to do this, they've already bought a seatbelt extender and left it plugged in. For my part, I don't even like *putting the car in gear* without having my seatbelt on, my parents having obviously done a bang-up job making sure that was ingrained in me early on. But that's just it... I do it out of habit, the annoying BONG-ing noise only serves to irritate me, not inform behaviour. For that reason, it's got to go.

The L322 Range Rover, L320 Range Rover Sport, and L319 Discovery 3/LR3 had an easy solution for those of us who didn't enjoy getting nagged about putting on their seatbelt every time the vehicle started. What you did is you buckled and unbuckled the seatbelt ten (10) times while the key was in the 'Run' (or 'On') position. After the tenth time, the seatbelt nanny chime was disabled (including when on the move). To re-enable it, just repeat the process. Needless to say, if you have one of those vehicles, skip this and just do the procedure above. In the L405 (after MY2013 I think), this procedure stopped working. It would disable the visual representation in the instrument cluster of who did and didn't have their seatbelt on (which *is* quite useful), but the car would still incessantly BONG at you (which is decidedly *not*).

The solution is to program it out of the car's Car Config File (CCF). There is a catch, though: there are two settings.
- One disables the annoying key on / ignition chime telling you to put your seatbelt on when stationary, but will still allow the car to bong at you if you're driving around without your seatbelt on which is the setting anyone using their vehicle regularly on a public highway should opt for.
- The other disables seatbelt detection and warning chime entirely, including when driving around. This is useful for when the vehicle is used only on private land in low-speed, constant start-stop driving, such as farm use.

> **Warning:** This may be illegal in your area, or at the very least may be cause for a FAIL on a safety inspection. There are two settings that can be modified. One only disables the audible nagging, while the other disables the seatbelt light in the cluster and will allow driving with your restraint unfastened without audibly alerting you. You make this change at your own peril. Don't be stupid.  

**L405 Range Rover**
|CCF Property|Value|Description|
|:---|:---|:---|
| USA safety belt chime | Disabled | When set to 'Disabled', turns off the key on / ignition on safety belt chime required for North American market vehicles. |
| Safety belt reminder | Enabled | When set to 'Disabled', turns off the safety belt detection and drive-off warning required (visual and audible) for all markets including North America. |

Once you've written that change to your vehicle's CCF, the vehicle will not make noises at you until you put your seatbelt on when stationary. Ah, sweet silence.  
  
If you write with the second one as 'disabled'... again, just don't be stupid, okay?

<br />
<hr>
<br />

## Letting the air out of Speedometer Inflation

Eeeeugh... *inflation*. In 2024, it's all anybody talks about.  
  
Well, I've got news for you: your Rover has been inflating your speedometer for a long time. You might have noticed your phone's GPS speed (Waze, Apple Maps, Google Maps, etc.) was often 2 KM/H or 2% lower than what your vehicle claimed you were doing. *You* think you're doing 60 KM/H, but you're *actually* only doing 58. This is incredibly stupid, unnecessary behavior (BuT sAfEtY!!!1!) and it deserves to be put out of its misery, so let's do that. Into the CCF we go. There are three settings we're interested in, and you want to change them to match what I've got below.

**L405 Range Rover**
|CCF Property|Value|Description|
|:---|:---|:---|
| Market | Market 1 : 2.0% + 0kph | Sets the default scaling to the lowest possible. It still says 2.0%, but we'll disable that later. This setting allows the inflation to be set in one shot based on the market. |
| KPH off-set | + 0.0kph | Sets the fixed speedometer off-set in kilometers per hour. |
| Percentage scaling factor | 0.0% | Sets the percentage by which the speedometer will inflate the speed of the vehicle. |

Why are there both percentage and KPH off-sets? Allegedly, the percentage inflation is applied at higher speeds where a small speed bump -- say, 2 KPH -- isn't sufficient to accomplish the goal of the speedometer inflation feature which is to make people *think* they're driving faster than they are. I haven't tested or confirmed this, but I recall reading it somewhere. In any case, we should turn off both for proper accuracy of the speedometer. It is worth pointing out that this can also be done on the L320 Range Rover Sport (and other LR products), though the CCF Property as listed might not match. Just look for terms like "scaling", "KPH", and "off-set".

> **Note:** After performing this change, I noticed when I set my cruise control to 100 KM/H that the vehicle would accelerate and hold at **102 KM/H**. This isn't the speedometer reading high, this is the vehicle still applying that inflation logic somewhere when cruise is invoked, and I haven't quite figured out why. (This is with dumb cruise control, not adaptive cruise.) It isn't a big deal since now you know how fast you're actually going and you can simply adjust the cruise to give you the desired speed.

<br />
<hr>
<br />

## New shoes, different size - calibrating for different tyre sizes

The facelift L320 Range Rover Sport (MY10-13) had a really clever way to adjust for the fact that people were putting on different tyre sizes than what the factory sent the cars out with. You could go into the navigation system and choose to perform a rolling calibration. The vehicle would compare the vehicle's speed data with the GPS, and adjust for the tyre's rolling circumference accordingly so your speedometer would be accurate (save for the speedometer inflation factor that was applied after the fact). When using SDD or IID to change the value, the L320 required the rolling circumference to be entered in millimeters, as does the L405.  

**L405 Range Rover**
|CCF Property|Value|Description|
|:---|:---|:---|
| Tyre rolling circumference | [Tyre circumference in MM] | Use a tyre size calculator to determine how tall your wheel and tyre combination is in MM. A 275/40R22 tyre will have a rolling circumference of 2446 mm, so find a value as close to that as possible. |

Pretty quick and painless.

<br />
<hr>
<br />

## Adding some athleticism to the big pudding - enabling Dynamic Terrain Response

If you've ever looked inside an L494 Range Rover Sport and noticed an extra little icon on the terrain response controller that looks like a winding road and wondered "what's that for", then you're in the right place. That windy road icon is to put the vehicle into "Dynamic" Terrain Response mode. Dynamic Terrain Response is a mode that backs off the electronic power steering assist a bit for a sportier steering feel, and stiffens the anti-roll bars when cornering. The result is a very big vehicle cornering nice and flat like a much smaller, sportier vehicle without a compromise in comfort. It also changes the instrument cluster and ambient lighting color to red, presumably because red is the universal color for <s>driving like a hooligan</s> <i>racing</i>.

Very cool, but you're probably thinking "How much does it cost to add the parts in to enable it?" I'm happy to report it costs whatever it takes for you to edit the CCF and add it in. Dynamic Terrain Response exists only in software (fitting the appropriate Terrain Response dial is optional), and everything the vehicle needs is already present.

**L405 Range Rover**
|CCF Property|Value|Description|
|:---|:---|:---|
| Dynamic button | Fitted | When set to 'Fitted', the vehicle allows switching Terrain Response to Dynamic mode, which stiffens the anti-roll bar in cornering, backs off the power assist steering a tad, and changes the gauges and ambient lighting color to red. |

But wait, how do I change into it if I don't have the appropriate Terrain Response control with the Dynamic icon? Easy. Take Terrain Response out of 'Auto' so that the normal Terrain Response mode is selected. Then turn the dial one click to the left, as though you're selecting the empty space beside normal mode. The instrument cluster will show you've selected Dynamic, the gauges and ambient lighting will turn red, and the Terrain Response control will not show any mode illuminated. You'll notice a difference on the road in short order.

It's good... very good.

<br />
<hr>
<br />
