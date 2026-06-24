# Make working design in Logisim 

<small>Mar 3, 2026 5.5 hours</small>

I figured out which chips would work best, and diagrammed it all out using those chips in Logisim evolution, alongside coming up with a basic design for at least the first version of my Turing Machine. It has 4 state bits and 1 tape, which will be expanded soon. There is a read head, which is a binary counter, and the program is made by the user using switches. I am unsure in my final design if I will use real switches, or something like 2 female pins that can be jumped by something like an LED. I intend on adding writing back to the tape, more positions in the tape, and the clock in my next update to it.
![Wiring diagram](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTE0NjI4LCJwdXIiOiJibG9iX2lkIn19--ea054d8a445198a72db548afd47ddc23a9121ad6/image.png)

# Expand tape and improve robustness

<small>Mar 3, 2026 1.5 hours</small>

I've revamped the functioning of the tape, and went through several different designs and prototypes of it, before settling on the current version, which has 4 7474s, which all feed into a 74151, and get their right signal from ANDing the NOT of a 74138 which maintains the write head and the clock signal, while they all take an input from a common output bus (so only one gets pulsed to take in the new data, while they all can see it).

![Wiring diagram](https://blueprint.hackclub.com/user-attachments/blobs/proxy/eyJfcmFpbHMiOnsiZGF0YSI6MTE0NzExLCJwdXIiOiJibG9iX2lkIn19--ce2f621dabef3a1f3b840c62b074dc46c829f0a0/image.png)

# Convert to KiCAD

<small>Mar 20, 2026 5 hours</small>

I've gone through the process of taking my messy, but functional, LogiSim design, and moving the majority of it (with some more progress to be done) to a KiCAD schematic, so that I may start working on actually designing the PCB itself. It's somewhat painstaking work, as the Logisim program wasn't fully working, and so I had to repeatedly go back and fix different parts of it, to make it work. Additionally, Logisim, for some reason, doesn't make it easy to follow how different wires go through the project, and so it required a lot of effort to determine where to go.

![Wiring diagram](https://stasis.hackclub-assets.com/images/1774024659371-rr4vz9.png)
![Wiring diagram 2](https://stasis.hackclub-assets.com/images/1774024671650-ddeokk.png)

# Start work on PCB Layout

<small>Apr 18, 2026 2/3 hours</small>

I added the BOM, using semi-placeholders for the 74** pieces and sockets for the main transition table. I then made it so that the table sockets, which were all imported as a solid chunk, where expanded to be grouped solely with their column indices, to try to make routing easier, though I'm still not sure how I plan on doing it. I also then connected the core small chips in the middle, and will then extend them out. I think I may want to breadboard this first, after designing the PCB, to verify at a cheaper cost that it just works, and then try to actually fabricate a PCB once I'm sure a smaller version works.

![PCB layout](https://stasis.hackclub-assets.com/images/1776536689828-qkxc5d.png)
![PCB layout 2](https://stasis.hackclub-assets.com/images/1776536796931-d577ls.png)

# More work on PCB layout

<small>Apr 18, 2026 0.5 hours</small>

I realized (later than I would've rather!) that the layout was actually kind of messed up, as it mixed up TABLE inputs, so the groups where essentially random, so I've started fixing that, going through and getting search six pairs of TABLE inputs and grouping them together, then bringing them to the bottom by the main chips, where I plan to put everything in a concentric around the main chips in the center.

![PCB Layout](https://stasis.hackclub-assets.com/images/1776546114847-he26s5.png)

# Power, Clock, Write back

<small>Apr 18, 2026 1.5 hours</small>

While wiring up the traces, I realized I hadn't created a VCC or GND, so I started adding those. And when I was adding those, I realized I also hadn't added the clock or the mechanism to write back, so I figured out a way to get a clock that works through stepping through each button press, going between 2 clocks for the 2 different halves of my process. Originally, I tried using some form of interfered with 555 timer, but I changed that up for a more elegant solution, and I had trouble figuring out how to work with the 2 clock outputs. I then also added a mechanism for writing outputs back to the tape counters and for processing the R/L bus. I also realized I needed to add pull down resistors.

![Wiring diagram](https://stasis.hackclub-assets.com/images/1776554282859-03pzm7.png)
![Wiring diagram 2](https://stasis.hackclub-assets.com/images/1776554263793-345big.png)
![Wiring diagram 3](https://stasis.hackclub-assets.com/images/1776554295126-jachml.png)


# Remove old traces, resize, and draw new traces

<small>Apr 25, 2026 2 hours</small>

I removed all of my previous traces, due to not liking the layout nor the size. I decided I would try to, instead, have all of my traces be manufactured through 3d printing the traces, and then pasting copper adhesive on the back, and cutting out around the traces, before soldering the components into holes in the 3d print. With that in mind, I then created more layers (6 more layers, though I've only used 3) and expanded my trace width to 2mm to make it easier to cut them out later. I also spent a while reorganizing my board and finding my different table components, and bringing them down and wiring all of them up properly.

![PCB layout](https://stasis.hackclub-assets.com/images/1777148670211-7e2wd7.png)

# Finish tracing tables

<small>Apr 25, 2026 0.5 hours</small>

I've added a lot of traces, and sorted my earlier tables, adding in a lot of traces so that the majority of my PCB is now done, and I essentially just have to wire up my memory and power.

![PCB layout](https://stasis.hackclub-assets.com/images/1777151127355-asca35.png)

# More routing

<small>Apr 29, 2026 2.5 hours</small>

I've spent a lot of time just dragging wires around, from part to part. I have drawn another around 900 track segments. My entire design goes through around 4 different layers of the PCB so far, but I could see it going through many more. These traces necessitated moving most of my chips to the other part of my board (which may let me shrink it, which is a bonus), but also resulted in me have trouble routing all of these traces between a bunch of different seemingly random nets.

![PCB layout](https://stasis.hackclub-assets.com/images/1777514107243-bqdxd4.png)

# Finish wiring up almost everything

<small>May 8, 2026 3 hours</small>

I spent a lot of time just wiring around the PCB. I had to create several new layers to get it all to work, and there's still a decent amount of work to do. I've had pretty good progress though. It was especially hard getting everything to work in as small of a footprint as I could, in order to keep the PCB (and fabrication costs) as low as I could. I ended up being almost completely unable to place more tracks or vias by the end, due to how cramped it is.

![PCB layout](https://stasis.hackclub-assets.com/images/1778505667042-nktr8j.png)

# Set up power

<small>May 8, 2026 3 hours</small>

I set up the power. I figured out what voltage my chips are designed to run at (74HCxx series), which was 5V, and so I designed a simple system using a USB input into some fuses in order to dampen it a bit and output a pretty straightforward 5v into my flood fill VCC.


![Wiring diagram](https://stasis.hackclub-assets.com/images/1778511652773-6t6tjn.png)
![PCB Layout](https://stasis.hackclub-assets.com/images/1778511652832-fodhtg.png)

# Add feedback

<small>May 14, 2026 1/4 hours</small>

I moved the USB-C port so that it can be properly used and plugged in. I also added some text on the silk screen explaining what it is and how it works.

![PCB layout](https://stasis.hackclub-assets.com/images/1779051017792-tp8c5i.png)

# Resolve errors

<small>Jun 21, 2026 1/2 hours</small>
I moved the USB-C and modified its clearances so it would stop throwing errors in the DRC. I also routed some previously unrouted paths I hadn't seen.
![DRC & PCB Layout](https://cdn.hackclub.com/019eea0b-2eb6-7c73-93a2-8a3013172f92/Screenshot%202026-06-21%20at%207.57.13%E2%80%AFAM.png)

# Improve routing

<small>Jun 22-23, 2026 3.5 hours</small>
I revamped the entire routing, making it a 4-layer PCB with signal/GND/VCC/signal, and made it look better and all around simpler and sleeker.<img width="982" height="507" alt="Screenshot 2026-06-23 at 11 04 55 PM" src="https://github.com/user-attachments/assets/c73e19a8-a553-44cb-b902-a4999c1269fc" />

