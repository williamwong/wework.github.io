---
layout:       post
title:        Bridging digital and physical with a MakerBot Replicator 2
author:       Dave Mills
summary:
image:        http://image.shutterstock.com/display_pic_with_logo/1451378/316560056/stock-vector-pumpkin-dressed-up-in-stripy-suit-furry-art-character-halloween-greeting-design-316560056.jpg
categories:   process
---

"Who's in charge of this thing?" I asked no-one in particular. 

Joanna, ever vigilant, told me to talk to Will. "He's grumpy."

Will wasn't that grumpy. I mean, he's a *little* grumpy. But he gave me a 10,000 foot overview of how the MakerBot works, explained extruders and filament, pointed me at Thingiverse, and said "have at it!"

I discussed what to print with my ping-pong hitting partner Alex. He builds our iOS apps. Should I print an Eiffel Tower? Should I print a phone case? Should I try modeling something myself, and if so, what? How many tiny TIE Interceptors could I print with three half-used large spools, and would that be enough to fend off tiny impending rebel assaults?

We decided to try printing a ping-pong paddle. We downloaded ScurtWad's [model](http://www.thingiverse.com/thing:175326), exported the print file from MakerWare at the default settings, and pressed print. Our eyes were filled with wonder as the bot sprang to life. 

Our first print was an epic fail. We refer to it as the ramen paddle.

![ramen paddle](/images/makerbot/failed_paddle.png)

The problem was that the model, oriented like this, needs supports. Without supports, the extruder extrudes into empty space. Who knew? It filled that empty space with a spaghetti-like structure. 

### First Steps

We had a couple laughs, played a round or two with what is arguably the worst paddle ever made, and then tried again. I checked the "supports" checkbox, re-exported the print file, and fired up the bot. 

![grey paddle printing](/images/makerbot/grey_paddle_printing.jpg)

This one came out better. But the side we put supports on was too rough, and it's a little egg-shaped:

![grey paddle rough](/images/makerbot/grey_paddle_rough.jpg)

Will suggested modifying the model to make it rounder, and orienting it diagonally on the build plate so it would need fewer supports and they'd attach to the side rather than the face. Instead, we decided to stop printing ping-pong paddles. 

### A Little Branding 

With a couple failures under my belt, I decided it was time for a win. I asked Will if he could create a model of a `wework` logo that I could sit on the top of my monitor. He said it would be a piece of cake, he just needed to know the thickness of my bezel, and a copy of our logo in vector format. 

So I asked Tracy, one of our amazing designers, if she had a version of our logo that Will could use. And indeed she did! She exported an `.eps` that Will imported into Rhino. There he extruded it, boolean union-ed it with a little sled, and exported an `.stl`. We imported that into MakerWare, added a raft and supports, exported the `.x3g` onto the SD card, and printed it:

![wework blue](/images/makerbot/wework_blue.jpg)

Picking the supports out of the letters is annoying, but it's one of my favorite models, and very popular around the office:

![wework yellow](/images/makerbot/wework_yellow.jpg)

Other people started printing them, and now they're in the strangest places:

![wework natural](/images/makerbot/wework_natural.jpg)

If we modified the raft a bit, we could print it on its side so it wouldn't need supports. Project for another day. 

### We Enclose 

It was at this point that Emiliano on our physical technology team approached me with a proposal. We'd worked together during our last hack-a-thon on a system for monitoring our conference rooms in real-time using a WiFi enabled infrared sensor. He wanted to deploy the system, but couldn't find a case that would fit the motley assortment of circuitboards: 

![circuitry](/images/makerbot/circuitry.jpg)

"I see you've been using the MakerBot - do you think you could make me a box?"

I had no idea how to make a box, but I lied and told him I would do my best. I downloaded [the free trial of Rhino for Mac](http://www.rhino3d.com/download/rhino-for-mac/5/evaluation), read some tutorials on how to make clam-shell enclosures, and went at it. 

I modeled an enclosure with a hole big enough for the IR sensor, little feet for the two other circuitboards, and a 1mm ridge on the top that fit into a 1mm trough on the bottom. It was glorious:

![enclosure v1 model](/images/makerbot/enclosure_v1_model.png)

Coming out of the bot, it looked OK:

![enclosure v1](/images/makerbot/enclosure_v1.jpg)

It had problems. 

 * the ridge/trough 
     * didn't work at all, I couldn't close the case
     * the bot's tolerance isn't good enough to make 1mm parts fit together 
 * the feet for the circuitboards
     * not tall enough to accommodate the circuitry on the backs of the boards
     * the screw holes I modeled didn't come out as holes so much as gnarled bits of plastic  
 * the IR sensor
     * nothing prevented it from being pushed back into the box
 * the box itself was warped

![enclosure v1 warped](/images/makerbot/enclosure_v1_warped.jpg)

### Rabbets and Feet

I was out of my depth. Fortunately, I had a secret weapon. And that weapon was a handsome southern man named [Zach](http://designalyze.com/course/3d-printing-makerbot). The first thing he suggested was to replace my 1mm ridge/trough with a larger [rabbet](https://en.wikipedia.org/wiki/Rabbet). I didn't know what a rabbet was, I thought he said rabbit. He explained it to me like I was 5; they weren't the same thing at all. 

I redid my model with a 1.5mm rabbet, actually modeled the circuitboards so they fit properly, and added a back-stop for the IR sensor:

![enclosure v2 model](/images/makerbot/enclosure_v2_model.png)

It was a big improvement:

 * the circuitry fit better
 * the case snapped shut beautifully on account of the rabbet
 * when I pushed on the IR sensor it didn't fall back inside
 
But the warping was getting worse:

![enclosure v2 warped](/images/makerbot/enclosure_v2_warped.jpg)

Our build plate is a little warped, and I wondered if this was related. Zach said that wasn't the case, that the raft should accommodate for that. The issue was that tension would build up in the filament during the print, causing the edges to pull in and up. 

He said one approach to this problem was to add little nickel-sized feet to the corners of the model. The feet might pull up a little bit, but their diameter is small so the warping would be minimal, and I could just cut them off with an x-acto knife. 

So I added some cute little feet to the model. As an added bonus, when I checked the new version into our repo, Will pointed out that github was doing pretty sweet previews for `.stl` files:

![enclosure v3 model](/images/makerbot/enclosure_v3_model.png)

This one came out great! Everything fit perfectly, and the nice thing about using the translucent filament was that we could see the notification LED through the case. It lights up when the IR sensor detects heat! 

![enclosure v3](/images/makerbot/enclosure_v3.jpg)

The feet not only improved the quality of the print, but they also made it easier to pull the case open, and were kind of adorable. 

### Iterating Quickly

Because I'd modeled the circuitboards, when Emiliano asked for another version of the case with the hole for the IR sensor on the bottom instead of on the side, it was easy to make the modification. 

![enclosure v4 model](/images/makerbot/enclosure_v4_model.png)

We ran out of the translucent yellow filament, so I printed it in blue instead:

![enclosure v4](/images/makerbot/enclosure_v4.jpg)

Look at those cute little feet! 

### Wrapping Up

We've had so much fun with our MakerBot. Aside from enclosures, we've been printing [so](http://www.thingiverse.com/make:168416) [many](http://www.thingiverse.com/make:168410) [different](http://www.thingiverse.com/make:168259) [things](http://www.thingiverse.com/make:167416). 

If you want a nice one, Zach and I (mostly Zach) made some helpful modifications to an [iWatch stand](http://www.thingiverse.com/thing:1108247):

![stand](https://thingiverse-production-new.s3.amazonaws.com/renders/53/8d/04/b3/a6/IMG_20151103_102724_preview_featured.jpg)

Happy printing! 