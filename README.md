---
title: Tips and Tweaks for the L405 and L320
author: TorqueDog
description: Tips and Tweaks for the L405 Range Rover and L320 Range Rover Sport
---

# Tips and Tweaks for the L405 Range Rover and L320 Range Rover Sport
A small corner of the internet where I document the interesting and useful things I've learned with my L405 Range Rover and previous L320 Range Rover Sport.
<br /><br />

# Before we begin

[What's this all about?](#whats-this-all-about)

[A word on the vehicle Car Config File](#a-word-on-the-vehicle-car-config-file)

[What tools are required?](#what-tools-are-required)

<hr>

# List of modifications



[Firing the Seatbelt Nanny](#firing-the-seatbelt-nanny)

[Letting the air out of Speedometer Inflation](#letting-the-air-out-of-speedometer-inflation)

[New shoes, different size - calibrating for different tyre sizes](#new-shoes-different-size---calibrating-for-different-tyre-sizes)

[Adding some athleticism to the big pudding - enabling Dynamic Terrain Response](#adding-some-athleticism-to-the-big-pudding---enabling-dynamic-terrain-response)

[Keep your distance with Adaptive Cruise Control](#keep-your-distance-with-adaptive-cruise-control)

[I installed an aftermarket head unit and my GPS is horribly inaccurate; now what?](#i-installed-an-aftermarket-head-unit-and-my-gps-is-horribly-inaccurate-now-what)

[My butt is burning - how to change the heated seat temperature targets](#my-butt-is-burning---how-to-change-the-heated-seat-temperature-targets)

[Chill out, bro! - Enabling Timed Climate](#chill-out-bro---enabling-timed-climate)

[Auto apply the parking brake at key off](#auto-apply-the-parking-brake-at-key-off)

[Experimental and unknowns](#experimental-and-unknowns)

<hr>
<br />

## What's this all about?

Since about 2002, Land Rovers have gotten increasingly more complex. More modules for more things, more ways to control how the vehicle behaves, how equipment is enabled/disabled, and so on. The L405 Range Rover is a great example of how just a bit of software tweaking can add a good deal of customization and features.

This repo focuses mainly on **2013-2016.5 L405 Range Rover**, and occasionally will mention things of value to **2006-2009 L320 Range Rover Sport**. Some of the L405 stuff may apply to L494 Range Rover Sport, but I can't confirm it. Feel free to reach out if any of it does and I'll make a note of it here. This repository is a combination of stuff I figured out on my own, stuff found in GAP's documentation, and on various Range Rover forums and groups, such as [RangeRovers.net](https://www.rangerovers.net/forums/range-rover-mark-iv-l405.24/).

<br />
<hr>
<br />

## A word on the vehicle Car Config File

A lot of these things require changes to the vehicle's **Car Config File** or **CCF**. The CCF is a vital piece of the vehicle's operating instructions. Making the wrong changes could prevent your car from working properly, possibly even brick the damn thing and require an expensive trip to the dealer. Any CCF changes you find here, you perform **at your own risk**.  

Stupid reasons to make CCF changes:  
- An attribute is set to **Undefined**, **Unsupported**, or some other such value, but there is a value in the list that matches your vehicle.  
&bull; Did your car work properly without it? Then it doesn't need it, and there's more risk in you adding it for zero gain. Leave it be, the car doesn't need it.
- I was curious what it did.  
&bull; Ugh, just close the browser tab before you wreck something. Okay, not entirely fair, some of these things *were* learned through my own trial-and-error, but don't blame me if you FA&FO with your expensive British luxobarge.

<br />
<hr>
<br />

## What tools are required when modifying the CCF?

You have two options:  
- **SDD** - *Jaguar/Land Rover Symptom Driven Diagnostics* software with a *JLR Mongoose OBD-II* interface  
&bull; Works on MY2016.5 and earlier only. I sold mine to a friend who bought my L320.
- **IID** - *GAP IID Tool*, either BT or Pro, with the correct version for your year of Land Rover  
&bull; G3 for vehicles up to MY2016.5  
&bull; G4 for vehicles MY2017 and later (which I largely don't cover in this guide because things moved to DoIP for MY2017 and lots has changed.)  
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
  
Well, I've got news for you: your Range Rover has been inflating your speedometer for a long time. You might have noticed your phone's GPS speed (Waze, Apple Maps, Google Maps, etc.) was often 2 KM/H or 2% lower than what your vehicle claimed you were doing. *You* think you're doing 60 KM/H, but you're *actually* only doing 58. This is incredibly stupid, unnecessary behavior (BuT sAfEtY!!!1!) and it deserves to be put out of its misery, so let's do that. Into the CCF we go. There are three settings we're interested in, and you want to change them to match what I've got below.

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

>[Note]
>This section needs some fixing particularly with the explanation, and here's why: My rolling circumference based on the wheel/tyre combo I run is 2446 mm. This is all well and good except that the speedometer is accurate while the below value **is not set correctly for that circumference**. I've even reached out to GAP Diagnostic themselves, who have replied back that they "cannot tell honestly as these values are not explained in LR literature. This is why we suggest changing and comparing with a GPS". So if you're gonna mess with tyre sizes outside of the normal spec, well, you're stuck messing with this value and seeing what it does. This isn't under [Experimental and unknowns](#experimental-and-unknowns) because **we know this is the right value to change**, but our understanding of what to change it **to** is still incomplete.

The facelift L320 Range Rover Sport (MY10-13) had a really clever way to adjust for the fact that people were putting on different tyre sizes than what the factory sent the cars out with. You could go into the navigation system and choose to perform a rolling calibration. The vehicle would compare the vehicle's speed data with the GPS, and adjust for the tyre's rolling circumference accordingly so your speedometer would be accurate (save for the speedometer inflation factor that was applied after the fact). When using SDD or IID to change the value, the L320 required the rolling circumference to be entered in millimeters.  

**L405 Range Rover**
|CCF Property|Value|Description|
|:---|:---|:---|
| Tyre rolling circumference | [Tyre circumference in MM] | ~~Use a tyre size calculator to determine how tall your wheel and tyre combination is in MM. A 275/40R22 tyre will have a rolling circumference of 2446 mm, so find a value as close to that as possible.~~ Apparently some arbitrary value, see note above. |


<br />
<hr>
<br />

## Adding some athleticism to the big pudding - enabling Dynamic Terrain Response

If you've ever looked inside an L494 Range Rover Sport and noticed an extra little icon on the terrain response controller that looks like a winding road and wondered "what's that for", then you're in the right place. That winding road icon is to put the vehicle into "Dynamic" Terrain Response mode. Dynamic Terrain Response is a mode that backs off the electric power steering assist a bit for a sportier steering feel, and stiffens the anti-roll bars when cornering. The result is a very big vehicle cornering nice and flat like a much smaller, sportier vehicle without a compromise in comfort. It also changes the instrument cluster and ambient lighting color to red, presumably because red is the universal color for <s>driving like a hooligan</s> <i>racing</i>.

Very cool, but you're probably thinking "How much does it cost to add the parts in to enable it?" I'm happy to report it costs whatever it takes for you to edit the CCF and add it in. Dynamic Terrain Response exists only in software (fitting the appropriate Terrain Response dial is optional), and everything the vehicle needs is already present-... at least on high-spec L405 models. You _must_ have adaptive anti-roll bars for this to work properly.

**L405 Range Rover**
|CCF Property|Value|Description|
|:---|:---|:---|
| Dynamic button | Fitted | When set to 'Fitted', the vehicle allows switching Terrain Response to Dynamic mode, which stiffens the anti-roll bar in cornering, backs off the power assist steering a tad, and changes the gauges and ambient lighting color to red. |

But wait, how do I change into it if I don't have the appropriate Terrain Response control with the Dynamic icon? Easy. Take Terrain Response out of 'Auto' so that the normal Terrain Response mode is selected. Then turn the dial one click to the left, as though you're selecting the empty space beside normal mode. The instrument cluster will show you've selected Dynamic, the gauges and ambient lighting will turn red, and the Terrain Response control will not show any mode illuminated. You'll notice a difference on the road in short order.

It's good... very good. If you want, you can try and find the appropriate part number that includes the Dynamic Terrain Response mode on the dial, but I haven't bothered; it simply isn't necessary.

<br />
<hr>
<br />

## Keep your distance with Adaptive Cruise Control

My L405 Range Rover was an interesting mix of options from the original owner. I have the 875W Meridian audio system, but no rear entertainment. I have massaging and heated/cooled front seats, but no four-zone climate or center fridge (peltier-based chiller yes, fridge no). Automatic high beam assist, blind spot monitoring, traffic sign recognition, and lane departure warning, but no adaptive cruise control (ACC).

I have had my misgivings about ACC in the past with a Mercedes whose DISTRONIC PLUS system would occasionally be rendered useless by radio frequency interference on my drive out east to visit my parents from time to time; the cruise control became entirely inoperable, and having DISTRONIC PLUS fitted meant foregoing the ability to fall back to 'dumb' cruise. But I do still miss having the ability to let the car manage the distance so I just need to change lanes and let it resume the speed I set it to, rather than having to cancel the cruise lest I rear-end this dummy in front of me going 10-under.

Enabling it does require physical parts, a CCF update, and a post-install calibration.

**L405 Range Rover**

Parts list:
|Part Name|Part Number|Description|
|:---|:---|:---|
| Radar Unit (front Bumper Mounted), (adaptive cruise) | **LR062658** _(VIN:FA000001-GA999999)_ | This is the part that makes it possible for the vehicle to detect if it is approaching an object in front. As Land Rover have different P/Ns based on VIN series for L405, check [Scuderia Car Parts](https://www.scuderiacarparts.com/part-finder/landrover/range-rover/oe/471/4471/82542) to confirm the part you should use. |
| Radar Unit (ALTERNATE PARTS) | &bull; **FPLA-9G768-AC** <br /> &bull; **DPLA-9G768-AC** <br /> &bull; **DPLA-9G768-AD** <br /> &bull; **GX73-9G768-AD** <br /> &bull; Basically any **XXXX-9G768-XX** sensor, pre-2017 | Note: **These are alternate part numbers.** As anyone reading this should be aware, Ford owned Land Rover and Jaguar for a time, and the Ford sensors are considerably cheaper than the JLR versions. Plenty of people have gotten these alternate Ford P/Ns to work, but you will likely need to flash their firmware, so you attempt these at your own risk. |
| Radar sensor mounting bracket | &bull; **LR060076** _(VIN:to HA999999)_ *Mine <br /> &bull; **LR100509** _(VIN:JA000001-on)_ | Allows mounting the radar sensor to the cutout in the front impact bar behind the bumper cover. Your sensor may come with this included if you buy it second-hand. |
| Hex bolts, M6 x 14MM | &bull; **RYG500160** | The bolts required to mount the radar sensor and bracket. |
| Cruise Control Switch (steering wheel mounted) (adaptive cruise, heated wheel) | &bull; **LR087486** _(VIN:GA283361-HA999999)_| A new cruise control switch with the distance adjustment (left and right buttons) is needed to adjust the following distance between your vehicle and the one in front. Again, check which P/N you need by checking [Scuderia Car Parts](https://www.scuderiacarparts.com/part-finder/landrover/range-rover/oe/471/4481/82930) based on VIN and what options you have fitted. |

CCF edits required (if it doesn't work, re-check these values):
|CCF Property|Value|
|:---|:---|
| Speed control | Adaptive speed control is fitted |
| Speed Control | Adaptive speed control with queue assist |
| Speed Control | Adaptive speed control, stop and go |
| Adaptive Cruise Control Indication In Instrument Cluster | Enabled |
| Adaptive Speed Control ECU | Enabled |
| Adaptive Speed Control ECU | North America, Canada, Mexico, Australia |
| Adaptive Speed Control ECU | Standard blockage level -40dB |
| Collision Mitigation By Braking | Fitted |
| Collision Mitigation By Braking | Collision mitigation by braking GEN 3 |
| Forward Collision Warning | Fitted |
| Forward Collision Warning | Forward collision warning GEN 3 |
| Front Crash Sensing System | Front crash sensing system – Upfront sensor |
| Standard Speed Control Display Type | Adaptive speed control full display plus priority messages |

Once this is done, you'll need to invoke the ACC calibration process. This is pretty easy to do with IID, SDD might take a bit of hunting around to kick it off. Basically find a nice straight road with a speed of 50 KM/H or higher and minimal traffic (keep a good distance between you and the cars in front of you if there are other cars out there), pick the lane closest to the curb with all the signage and such, and drive until the ACC lamp in the instrument cluster stops flashing. That'll signal that the calibration is complete. The radar is looking for stationary objects like lamp posts and signage to calibrate itself.

If you have difficulties, contact GAP Diagnostics themselves and they can help, including flashing a new firmware on the radar unit if need be.

Variation in available values that aren't yet understood:
|CCF Property|Value|Notes|
|:---|:---|:---|
| Speed Control | &bull; Adaptive speed control, stop and go <br /> &bull; Adaptive speed control, brake limit 2 <br /> &bull; Adaptive speed control, stop and go, brake limit 2 | It's unknown at this time what 'brake limit 2' does or adds to the functionality here. I've set mine to '[...] stop and go, brake limit 2' and have no observed any difference in behaviour. |
| Front Crash Sensing System | &bull; Front crash sensing system – Upfront sensor <br /> &bull; Front crash sensing system – Closing velocity <br /> &bull; Front crash sensing system – Upfront sensor and closing velocity | It's unknown at this time what the addition of 'closing velocity' does to this feature. Mine is set to 'Upfront sensor and closing velocity' and no errors or faults have occurred. |
| Collision Mitigation By Braking | &bull; Collision mitigation by braking GEN 3 <br /> &bull; Collision mitigation by braking GEN 3 – Level 2 | The question here is "What's the difference between GEN 3 – Level 2 and plain ol' GEN 3" and at this time I'm unsure. The inability to test such a feature without trying to rear end the car in front of me will slow getting clarity here. Mine is set to "Level 2" with no fault codes thrown. |

Features that work in conjunction with ACC radar units:

**Low speed intelligent emergency braking (IEB)**
|CCF Property|Value|
|:---|:---|
| Low speed intelligent emergency braking | Fitted |
| Low speed intelligent emergency braking | Front and Rear |
>[NOTE] When I enabled these settings on my L405, once the CCF writing was complete, I immediately got a 'Park Brake Fault' error in the cluster. Weirdly, the parking brake worked just fine and would engage and disengage without issue, but the vehicle insisted there was something wrong with it. I suspect there is a requisite hardware component missing in my L405's build for IEB that causes the vehicle to report that fault, or another CCF property that IEB is dependent on to work properly.

**Some of these values are directly from GAP Diagnostic's FAQ, thank you to GAP for publishing them. Others were added via independent CCF research, and from places like [RangeRovers.net](https://www.rangerovers.net/forums/range-rover-mark-iv-l405.24/) forums.

<br />
<hr>
<br />

## I installed an aftermarket head unit and my GPS is horribly inaccurate; now what?

You went on Amazon / AliExpress / some other website and you bought either a piggyback or a full screen replacement to get in on that sweet wireless Apple CarPlay and Android Auto action, and perhaps even a nicer screen. It looks so slick and brings the vehicle's otherwise woeful infotainment into the modern era. But when you start using Waze, Apple Maps, Google Maps--... whatever you use -- and have it navigate for you, it goes completely haywire. The vehicle bounces around or shows on the incorrect street, the speed is inconsistent (sometimes you're stopped and the car thinks you've blown through the next two intersections), or -- my personal favourite -- you're powersliding sideways down the highway at 110 KM/H. It's funny the first time, and annoying every other time after.

This is a problem with Range Rovers with solar attenuated glass. The phone is unable to get a GPS lock because the attenuation layer is blocking the signal. This is the same reason why radar detectors don't work well in Range Rovers either unless you tuck them right beside the sun-visor where the solar attentuation layer is not present (you can see it clearly up close).

Thankfully, this is easily dealt with. But first, time to go shopping.

|Part needed|Where / Cost|What it does|
|:---|:---|:---|
| Fakra C Male to dual Fakra C Female splitter | [Amazon](https://www.amazon.ca/JAGTRADE-Splitter-Pigtail-Antenna-Extension/dp/B0CS6DSVX1) <br /> $14 CAD | This takes the GPS coaxial that comes in from the vehicle's own GPS antenna and splits it so you can send one to the vehicle's head-unit, and the other to our new GPS amplifier.|
| Fakra C Male to SMA Male adapter | [Amazon](https://www.amazon.ca/dp/B07MCL8R3G) <br /> $15 CAD | Connect this to the free end of the Fakra splitter above, and connect it to the GPS amplifier. |
| GPS Signal Amplifier and Receiver | [eBay](https://www.ebay.com/itm/195879327702) <br /> $26 CAD | This receives the GPS signal from the vehicle's onboard GPS antenna and amplifies it. This contains both an amplifier (SMA female coax wire and USB cable) and antenna (one SMA male coax wire), but we are **only** using the amplifier. |
| 12V to USB 5V step down voltage converter | [Amazon](https://www.amazon.ca/dp/B07V6158V3) <br /> $18 CAD | This is what we'll use to power the GPS amplifier. |
| Add-a-Circuit Micro2 fuse taps | [Amazon](https://www.amazon.ca/dp/B08S78VD5H) <br /> $12 CAD | We'll use the fuse-taps to tap in to an existing ignition-switched load in the passenger compartment fuse box, behind the lower glove box. |

I'll draw a nice little diagram at some point, but for now:
- Find somewhere convenient to mount the GPS signal amplifier. Remeber, this is the little black puck with both an SMA female cable and a USB cable. I mounted mine behind the trim that you remove to remove/install the infotainment screen.
- Connect the male end of the Fakra splitter to the vehicle's GPS that is currently connected to the head unit.
- Connect one female end of the Fakra splitter to the vehicle head unit.
- Connect the other female end of the Fakra splitter to the Fakra to SMA adapter.
- Connect the SMA adapter end to the GPS signal amplifier's SMA female cable.
- Route the amplifier's USB cable behind the head unit and screen over to the fuse box behind the lower glove box.
- Wire the voltage converter's red (positive) wire to a fuse-tap lead and find a chassis ground near the glove box to affix the black (negative) ground wire to (behind the trim tucked under the door weatherstripping is a good location). Make sure the ground wire is secure!
- Find an ignition switched load to add the fuse tap. I try to find non-critical loads that already use 5A fuses so we don't overload the circuit.
- Plug the USB from the GPS amplifier into the voltage converter.

> Note
> I got some of these details from a user at RangeRovers.net, but their solution was incomplete. They insisted that powering the GPS amplifier was unnecessary as the GPS signal from the vehicle is already amplified, but when I attempted this, the amplifier did nothing whatsoever until I provided it with power (just for testing, I used a USB battery bank). You need to power the GPS amplifier. You could run a USB cable directly to one of the vehicle's own USB ports but I wouldn't recommend this and it makes for a far more difficult install.

Once you've wired this up, go for a drive and you should get a nice stable GPS lock and no more weird behavior.

<br />
<hr>
<br />

## Chill out, bro! - Enabling Timed Climate

In European markets, Land Rover equipped L405 models -- typically diesels -- with timed climate and fuel burning parking heaters with remotes, which is a brilliant idea. In North America, we largely got nothing (until much later in the L405 production run), presumably due to the fear that some idiot was going to freeze himself to death relying on the park heater, and a wrongful death suit would be forthcoming. Being upstairs neighbours with the most litigious country in the world has its drawbacks, as Canada would have been an ideal place to sell the petrol version of the fuel-burning park heater option.

The park heater isn't a huge loss for me, personally; I typically try to park indoors -- out of the harsh elements -- but the reality is that isn't always going to be an option. Plus, winter isn't the only consideration, it gets hot in Canada during the summer. I had an E39 BMW M5 that had a 'Rest' function in the HVAC that would allow the driver to set the ventilation system to cool the car down for about half an hour. It could -- if I remember correctly -- be scheduled, *timed*. This clever BMW feature found its way into the Range Rover L322, which was designed during Munich's ownership of Land Rover from 1994 to 2000, and used a good deal of BMW electronics. If you're me -- driving a Santorini black L405 with black Windsor hides, black headlining, and piano black veneers in a hot Canadian summers, no amount of solar attenuated glass nor the trick automatic sunroof shade is going to help the fact that it's gonna be *hot* in that interior if you leave it parked in the mid-day sun for five hours.

While we can't get park _heat_ working without spending a thousand bucks or more, there are -- thankfully -- some elements of this system that require no additional hardware to operate: Timed Climate. And with timed climate, we can at least get scheduled _ventilation_.

It should be pointed out that this is **just ventilation**, not actual 'cooling'. The engine isn't running, the A/C compressor isn't spinning, there's no refrigerant involved here. This is just get the cooler air from outside the vehicle in, and expel the hot air inside the greenhouse known as your Range Rover.


**Enabling Timed Climate**
|CCF Property|Value|Where found|
|:---|:---|:---|
| FBH Call Start | Radio | Confirmed CCF - BCM Body Control |
| Fuel Burning Heater | Fuel fired parking heater (FFPH) | Confirmed CCF - BCM Body Control
| Timed Climate | Fitted | Confirmed CCF - BCM Body Control |
| Callstart of parking heater | Callstart of parking heater - Accessory only (via radio) | Complete CCF (Untested) |
>[NOTE] When I enabled these settings on my L405, my Ventilation ECU would show a fault that the fuel burning park heater was not responsive; this is normal and will persist, but Timed Climate will show up and work.

Once this completed, you'll see some changes:
- a new button in the Climate screen called 'Rest heat'. This is perpetually greyed out for me, I will check again when I'm actually parked somewhere that it's bloody cold out, but in my 19 degree Celsius parking garage with the engine fully warmed up, this remained greyed out.
- from the main infotainment menu, navigate to the 'Extras' pane and you should see there is an extra page. Go to it and all by its lonesome -- depending on what other options you have -- you will see Timed Climate.

In the Timed Climate menu, you'll see the two different timer options and the following buttons:
- 7 Day Timer
- Single event
- Manual heat
- Manual vent
- Timer
- Stop Event

'Manual heat' and 'Manual vent' are greyed out for me, just like 'Rest heat' in the Climate screen. I tried with engine off, on, nothing. I'll update if I ever get an idea of what needs to fall into place for these to work.

There are two ways to use Timed Climate:
- 7 Day Timer - Allows you to set two different timer reschedules from Sunday to Saturday. Let's say you start driving to work at 07:30 and driving home at 17:00, you can set your two 7 day timer schedules to 07:00 and 16:30 daily, so your vehicle will start venting and cooling itself down 30 minutes before you start driving to work.
- Single event - Let's say you're going to an outdoor event that you know ends at 16:30 -- set your single event to today's date and 16:00 and the vehicle will do the rest. You can even set this to a date in the future, though I'm not sure I'm that much of a planner that I could use it that way.

Select the one you want and press the 'Timer(s)' button to configure when you want to run Timed Climate venting. In theory, this should also  enable maintaining the cabin's temperature in cold climates through residual engine heat, but I haven't tested this and depending how cold it is, who knows how effective it'll be.

When Timed Climate is configured, you'll see the 'Auto' light flash on the driver's side of the HVAC controls when set (assuming you have the physical buttons) and the A/C lamp slow blink continuously while Timed Climate is in operation.

<br />
<hr>
<br />

## Auto apply the parking brake at key-off

Live in San Francisco or somewhere with excessive inclines and declines and need to use the parking brake more often than usual? You can program the vehicle to set it as soon as you turn off the vehicle.

|CCF Property|Desired value|Possible values|
|:---|:---|:---|
| Electronic park brake key out apply | Key out apply | &bull; Undefined <br /> &bull; Without key out apply <br /> &bull; Key out apply |

Yes, it's called "key out" but we have proximity keys, there is no _key out_. When you put the vehicle into any directional gear, the electronic park brake will automatically disengage. I personally kept this one off. It isn't really necessary for me.


<br />
<hr>
<br />

## My butt is burning - how to change the heated seat temperature targets

There's a value that allows you to change the temperature range of your seat heaters. It's a universal value and will affect both front and rear heaters.

|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| Seat heat calibration | Low temperature 36Â°C - High temperature 43Â°C | &bull; Undefined <br /> &bull; Without seat heating <br /> &bull; Low temperature 28Â°C - High temperature 35Â°C <br /> &bull; Low temperature 30Â°C - High temperature 36Â°C <br /> &bull; Low temperature 30Â°C - High temperature 37Â°C <br /> &bull; Low temperature 31Â°C - High temperature 37Â°C <br /> &bull; Low temperature 31Â°C - High temperature 38Â°C <br /> &bull; Low temperature 32Â°C - High temperature 38Â°C <br /> &bull; Low temperature 33Â°C - High temperature 39Â°C <br /> &bull; Low temperature 34Â°C - High temperature 40Â°C <br /> &bull; Low temperature 35Â°C - High temperature 41Â°C <br /> &bull; Low temperature 36Â°C - High temperature 43Â°C <br /> &bull; Low temperature 40Â°C - High temperature 46Â°C <br />|

Before you go cranking this from the default to the maximum Low 40°C - High 46°C, you should know that when I did this, it simply disabled the seat heaters; the Climate module threw a fault code saying that its configuration was incorrect, and I could no longer turn on the seat heaters (or seat ventilation) for front or rear passengers. I had to set the value back to my default and clear the code, then restart the vehicle for it to work again. So while you can likely use this property to back off the seat heaters if they're *too hot* for you, if you want to feel the heat of an Arizona summer on your backside, the value that allows for 46°C is not likely going to work, just stick with the 43°C max.

<br />
<hr>
<br />

### Experimental and unknowns

Remember how I said a good deal of the knowledge here was learned through trial and error? Well, trial, error, and _research_ to be exact.

Listed here are some rather interesting entries in the L405 CCF. These may not be present in your CCF, especially given that my 2016 L405 is a late production 'MY2016**.5**'. If they are and you have different values set than what I have here, I'd love to hear from you, so please reach out. I will try and group related entries together in a single table for readability's sake. Now, without further ado, the curious entries.

<hr>
<br />


**Eliminating the 'DRL Wink' when using turn-signals (Unsolved mystery!)**

If you aren't sure what I mean by this, this is the behavior that shuts off the front 'signature LED tube' DRL on the side for which you have switched on the turn signal indicator. This is mandated by US D.O.T. regulations; if the indicator and LED DRL are too close in proximity then the DRL on that side must be switched off while the indicator is operating (so sayeth the regulation). It gets applied to all North American-spec vehicles because Canada and the US are (mostly) harmonized on their federally-mandated vehicle safety requirements. Of course, this doesn't apply to the UK and many places in the EU, so I thought 'There must be a way to change this behavior in the CCF'. It is entirely possible that this behaviour is baked into the NAS headlamps themselves, since the North American specification also has different headlamps to incorporate the amber side reflectors that aren't required elsewhere. So LR067204 and LR067213 might be needed (LHD adaptive bi-xenon headlamps, non-NAS spec).

Testing protocol:
With the vehicle outside on a bright day: <br />
&bull; Start the vehicle with the headlamp stalk in Auto<br />
&bull; Put the rotary gear selector in D (Do this BEFORE applying the parking brake)<br />
&bull; Apply the parking brake (DO NOT FORGET THIS and for the love of god MAKE SURE IT HOLDS THE VEHICLE BEFORE PROCEEDING)<br />
&bull; Turn on the driver's side indicator and check the front headlamp to see the behavior of the LED DRL.<br />
Does it stay on or shut off while the amber indicator is flashing?<br />

So far, I've been defeated. If anyone has any leads on how to accomplish this, please get in touch!
Here's the list of things I've identified in the CCF and -- if I've tried them -- what the result was. Obviously my default values don't work. It is very possible that it requires a combination of settings to work correctly.

|CCF Property|(My) Default Value|Possible Values|What did the changed value do?|
|:---|:---|:---|:---|
| Front DRL Type | Incorporated DRL and Pos | &bull; Not supported <br /> &bull; Not fitted <br /> &bull; Dip as DRL <br /> &bull; Dedicated DRL <br /> &bull; Incorporated DRL and Pos <br /> &bull; Error | Dedicated DRL <br /> &bull; Behaviour unchanged. |
| Front DRL profile | Diagnostic profile 11 | &bull; Not supported <br /> &bull; Diagnostic profile 1 <br /> &bull; Diagnostic profile 3 | Untested |
| Dedicated daylight running behaviour - Market | North American specification | &bull; North American specification <br /> &bull; Japanese <br /> &bull; ECE <br /> &bull; Disabled | Japanese and ECE <br /> &bull; Behaviour unchanged. |
| North American specification lamps are fitted. | Fitted | &bull; Not fitted <br /> &bull; Fitted <br /> | Behaviour unchanged. | 
| Daytime running lamps enable | Active | | Untested |
| Scandinavian daylight running lamps enable | Disabled | | Untested |
| Canadian daylight running lamps enable | Disabled | | Untested | 
| Daytime running lamps | Standard dipped lighting (non daytime running light) | | Untested |
| Headlights symmetry | USA symmetry | &bull; Left hand symmetry <br /> &bull; Right hand symmetry <br /> &bull; USA symmetry | Left hand symmetry <br /> &bull; Behaviour unchanged. |
| DRL Auto Switching | Disabled | | Untested |

<br />
<hr>
<br />

**Lane Keep Assist**

|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| Lane keep assist | Not supported | &bull; Not supported <br /> &bull; Not fitted <br /> &bull; Fitted <br /> &bull; Error |

_Whaaaaa...?_ Lane Keep Assist is officially available on the 2017+ L405 models (and 2018+ models also have the option of a Cruise Steering Assist (CSA) mode). If you're familiar with Lane Departure Warning, LKA is the same thing except the vehicle will _also_ gently steer itself back into the lane, as well as vibrate the steering wheel. This is described as sort of a 'ping pong'-type behavior where the vehicle doesn't have any intelligence in keeping the vehicle in the middle of the lane, it just stops you leaving your lane. On the other hand, CSA will try to keep the vehicle steering relatively straight and true in the lane, and will even negotiate gentle curves in the roadway without any input from the driver. 

The **Not supported** default value originally didn't give me much hope, but my MY16.5 L405's manual _does_ make specific reference to it being an option and -- given a vehicle with Park Assist (ability for the vehicle to move the steering wheel itself) plus ACC and LDW -- it is curious that it is present in the CCF all the same, though this is likely due to Jaguar already having this as a RPO in their models. 

When 'Lane keep assist' is set to **Fitted** on my own L405, there is still no LKA option in the cluster and LKA does not work, but LDW continues to function normally. This is the case both with and without ACC enabled. Prior to MY2017, L405 didn't have the stereo camera IPMA module fitted at any point in its production as far as I can tell.

Hypothetically, an attempted retrofit would require -- at minimum -- the following components be procured and installed or replaced:
- windshield, upgraded to a MY2017 part
- rear-view mirror
- pre-DoIP IPMA Premium module (must be 'Premium' not 'Enhanced'; 2016 Jag X260 would be a suitable donor)

This makes some heavy assumptions:
- updated MY2017 windshield will fit (physically, it should)
- IPMA Premium harness even exists in an L405 and/or the pigtail can be fitted to the main harness
- IPMA Premium module from a pre-DoIP Jaguar that has LKA will communicate successfully

Seems like a long shot, but unless someone who makes a living from YouTube wants to give it a try, this one will likely stay a theoretical possibility rather than a proven option.

<br />
<hr>
<br />

**Night Vision**
|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| Night vision | Not fitted | &bull; Not supported <br /> &bull; Not fitted <br /> &bull; Fitted <br /> &bull; Error |

This one doesn't seem to do anything in my testing. My L405 has the surround cameras, and when it's dark out, I can turn on the front camera and the camera goes into an infrared mode similar to what the reverse camera does when it's dark out. It did that irrespective of what this setting is. I mean hey, at least we have some sort of night vision! It would be cool to have a secondary night vision camera that is roughly at windshield height though, and one that displays in the driver's cluster instead of the center screen.

**Deployable sidesteps / Retractable running board**

|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| Deployable sidesteps | Not supported | &bull; Not supported <br /> &bull; Not fitted <br /> &bull; Fitted <br /> &bull; Error |
| Retractable running board | Undefined | &bull; Undefined <br /> &bull; Without retractable running board <br /> &bull; Retractable running board - Button controlled |

I've always thought the deployable sidesteps was a great option, and I've been curious what would be needed to fit the factory steps to my 2016 L405. I suspect both settings are part of a complete fitting solution, as the instructions to use the deployable sidesteps from Land Rover do mention a function switch to operate the side steps manually to get them into Terrain Response Override mode and Roof Access mode.

<br />
<hr>
<br />

**Cluster alert graphics / Gauge variant / ECO data driver information display**

|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| Cluster alert GFX | Not supported | &bull; Not supported <br /> &bull; Generic Warning Display <br /> &bull; Market Derivative Warning Display <br /> &bull; Jaguar Branded Warning Display <br /> &bull; LR Branded Warning Display <br /> &bull; Error |
| Gauge variant | Scale 1 | &bull; Scale 1 <br /> &bull; Scale 2 <br /> &bull; Scale 3 <br /> &bull; Scale 4 |
| ECO data driver information display | Display information level 5 | &bull; Disabled <br /> &bull; Display information level 1 <br /> &bull; Display information level 2 <br /> &bull; Display information level 3 <br /> &bull; Display information level 4 <br /> &bull; Display information level 5 <br /> &bull; Display information level 6 <br /> &bull; Display information level 7 <br /> &bull; Display information level 8 |

I have no idea what the hell any of these are supposed to do, frankly. My curiosity is mainly because we can't get the el neato "SVAutobiography" cluster like the 2018+ L405s can, so there has to be _something_ to get a cool hidden gauge cluster appearance, right? _Right?_


<br />
<hr>
<br />

**Wade sensing**

|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| Wade sensing | Not fitted | &bull; Undefined <br /> &bull; Not fitted <br /> &bull; Fitted |

No mystery here; this is to enable Wade Sensing (how deep the water you're driving through is relative to the vehicle's water fording abilities), which was never made available in the North American market. Basically, you need to add the side mirror wade sensors (parking sensors that mount into the wing mirrors, requires different mirror frames), the wade sensing module (general proximity sensor module or GPSM), and the GPSM harness for it. This will likely have its own entry complete with part numbers to make it work at some point, but for now, it's stuck in this section.

<br />
<hr>
<br />

**TPMS variant**

|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| TPMS variant | Standard | &bull; Fitted <br /> &bull; Standard <br /> &bull; Premium Chassis <br /> &bull; ECO <br /> &bull; Error |

No clue what the different variants do, but I'm quite curious. Will be updated once tested.



<br />
<hr>
<br />

**Service interval**

|CCF Property|(My) Default Value|Possible Values|
|:---|:---|:---|
| Service interval | Undefined | &bull; Undefined <br /> &bull; User defined service interval <br /> &bull; Service interval 1 - 15000 km <br /> &bull; Service interval 2 - 7500 miles <br /> ... and so on. |

To be blunt, I think Land Rover's recommended / default servicing interval for these things is absurdly long, and I would happily define my own service interval around or between 5,000 - 10,000 km. Strangely, my service interval in the CCF is set to 'Undefined' but I'm quite certain it is counting down from the factory 26,000 km (!!!) interval. I tried changing this to a lower value (5,000 KM) but it did not have any influence on what the vehicle thinks is the service interval.

26,000 KM, no wonder people have problems with these bloody things.


<br />
<hr>
<br />

