Here lie sporadic journals written in the moment. Properly structured project logs can be found in `DEVLOGS.md`

**Total time spent:** - 13.5h  [*last updated: July 25th*] 
## July 20-22nd 
>This log was written retrospectively.

Coming off the high of a [hardware hackathon](http://fallout.hackclub.com/), I was itching to work on a new project, and to make it with more intention than I had ever before. I decided to participate in [Unfold](http://unfold.garden/): a six week program to ship a technical project

Inspired by vintage Casio watches, and my measly watch collection, I'm making a custom watch! I'm planning to mod an existing watch such as the Casio F-91W (the obvious choice, following in the steps of the Sensor Watch and Ollee Watch), and Casio LA variants.  

I got a cheap notebook while traveling, and did lots of ideating/planning in it throughout my trip.

*Time spent - 2 hours*  
## July 23rd
After way too much deliberation (and a flight + HSR ride later), I decided to not settle for a segmented LCD display (from a Casio watch). I don't love the limitation of the segments for text and images.  

Looking through [small displays](https://www.crystalfontz.com/products/smallest-lcds-oleds-and-epaper-displays.php), I researched everything from monochrome OLED to monochrome LCDs.

I ended up going with E-Paper! Specifically the [GDEM0122T21](https://www.good-display.com/product/548.html) from Goodisplay.  
- 1.22" size, one of the smallest I could find  
- 0.3s partial refresh duration, really great for my watch! (see demo vid here)  
- low power. it's e-paper
- persistent display (for fun images)  

I also considered some charging methods, but didn't get too far.

> I would much rather use an unsegmented LCD for its limitless display options; Though, it would destroy the battery life.

*Time spent - 3 hours*  
## July 24th
Copied over a previous project's e-ink section, and modified it for the GDEM0122T21.

![[Pasted image 20260725202734.png]]

I was able to swap some parts to lower voltage ratings (saving money!), and smaller packages (saving space!!).

*Time spent - 1 hour*  
### July 25th
To sufficiently power all my features, a standard coin cell (CR2016 as seen in the F-91W) won't cut it. I need something with a greater current capacity.

Initially, I considered using micro USB to charge, in addition to uploading firmware. But this design would require consistent charging, meaning disassembly every few days. Given how often I forget to charge my other devices, I decided against this.

As I was looking into Seiko's discontinued line, I stumbled across a dive watch (SDGA001) and an accompanying [blog post](https://www.fratellowatches.com/seiko-watches/dear-seiko-bring-back-the-sdga001/).

There I found my solution: Solar power. 

Possible implementations I've found so far:
- Amorphous silicon transparent solar cells
- Standard solar cell
	- Placed in the bezel of the watch, or just above
	- Procurement:
		1. Panasonic: Amotron, their Amorphous silicon solar cells
		2. Disassembly of an existing solar watch (e.g. the Casio Tough Solar)

LightInk is a really cool open-source, solar powered Watchy. Really hyped to see that there is a community for this type of thing. 

Set up some `README.md` automations with [mustache](https://mustache.github.io/) among other repo cleanup. This is a really neat template and I'm really enjoying using it! The author's blog is also pretty interesting.

With solar power settled as the charging solution, next up is figuring out exactly which cell type and part will work best. I've just arrived at my relatives' place, hence I have more time to work on this! 

*Time spent - 5 hours*  

## July 26-27th
(grouped the two together to keep the dive uninterrupted)

Today I continued the deep dive on solar cells from yesterday! Zooming out from Amotron, I focused on solar cells as a whole. Here's a recap of what I learned:

*heads up: I went down a bit of a rabbit hole*

Solar cells are classified as either 'Amorphous silicon (a-Si)' or crystalline. Crystalline cells (c-Si) are suited for outdoor use; they **transform sunlight into electricity (through photovoltaism, PV)**. These are used in the large solar panels you see outdoors. 

Sunlight is composed of IR, UV, and visible light. Crystalline cells depend on the intensity of sunlight to overcome their high internal resistance, to produce a current. They are optimized for the high wavelengths of Near-Infrared (NIR, IR with high frequency aka closest to the visible spectrum) light within sunlight. 

The remaining UV and visible light in sunlight are in such high quantity that they can contribute as well. This means that indoor lighting conditions cannot provide sufficient visible light (or other types) to start up a c-Si. A big caveat. Crystalline cells are superior in most applications. But for small-scale, compact electronics, they are overly thick and rigid.

Following in the footsteps of giants, I will not be using crystalline cells, and opting for their counterpart: Amorphous silicon. 

A-Si is a micro-thin material, around 1-2 um thick (approx. 150x thinner than c-Si). Furthermore, it's made of silicon gas, giving it the properties of the material it is deposited onto, providing it the ability to be flexible. This is a big plus over the rigidity of c-Si. 

Unlike c-Si, a-Si is tuned to accept wavelengths on the visible spectrum. You may be wondering as I was, **what happens when it is inevitably introduced to higher frequency light sources?** 

In commercial products (think of your calculators and watches) it *does* have a negative impact on the a-Si solar cell, it damages it. Though, it is minimized via a UV filter. 

>It doesn't filter out higher frequency/energy radiation, notably X-rays.
>
>X-ray radiation is not commonly received, and requires a much denser material (a.k.a something made up of an element with a higher atomic number) to filter it out. Without such a barrier, it would destroy the solar cell.
>
>(Think of the thick, heavy vests you wear when taking an X-ray.)
>
> Looking further up the electromagnetic spectrum, if you're exposed to Gamma rays you have bigger fish to fry...

These products use a variant of the a-Si: the a-Si:H, Hydrogenated amorphous silicon. 

Amorphous, meaning 'having no definite form : shapeless' describes the ever-changing structure of connected silicon atoms. Not all atoms in the structure are fully bonded (tetrahedrally), in contrast to solid silicon, leaving loose ends. These 'loose ends' can be electrically surprising, so to make them more-or-less unreactive, we dose it with Hydrogen, which attaches to all the loose ends. 

There are other solar cell alternatives which are difficult to source (such as [Exeger Powerfoyle](https://www.exeger.com/powerfoyle/)) as they are limited to B2B partnerships.

*Time spent - 2.5 hours*  

