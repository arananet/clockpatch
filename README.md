[work in progress...]

This is a website trying to explain the clock patch for the Atari Falcon in layman's terms. As a bonus, you can find here [history of all known schematic and PCB revisions](history.md), with details of every change (if available).

Purpose of this site is not to shock you with some new findings but gather the existing knowledge. If you google for Falcon clock patch, you'll get very fragmented information with blurry schematics and very often not even in English language but in German or French instead. Basically, all the great knowledge is burried in old magazines, FidoNet archives and ancient Usenet groups' posts.

I'd like to meet two goals with this little project, one is to encourage people to get again interested in this confusing little mod (esp. those who do not know what is it about at all) and second is to get some feedback from people who *do* know but are lazy to explain all the details to others but maybe would like to correct errors or add a bit of information.

If you find an error, please mention it in the [issues](https://github.com/mikrosk/clockpatch/issues) or fork the [repository](https://github.com/mikrosk/clockpatch) and provide a [pull request](https://github.com/mikrosk/clockpatch/pulls) (you can edit these files directly in the web editor).

## What is it?

It is a small patch (or mod if you like) for the three main Falcon clock signals (fed to the CPU, FPU+SDMA and the expansion slot), usually (but not always) utilising one or more 7404 and/or 7408 [gates](https://en.wikipedia.org/wiki/Logic_gate).

## What does it do?

The 7404 is a hex [inverter](https://en.wikipedia.org/wiki/Inverter_(logic_gate)), i.e. it can invert six independent inputs from high to low and vice versa. It has 14 pins, 6x2 are input and outputs, the remaining two are VCC (+5V) and GND (ground). 

The 7408 is, on the other hand, a quad 2-input [AND gate](https://en.wikipedia.org/wiki/AND_gate), i.e. it can do boolean AND operation on four independent pairs of inputs. It also has 14 pins, 4x(2+1) are inputs and outputs,  the remaining two are VCC (+5V) and GND (ground).

If only one IC is used, it is usually mounted on top of U63 which offers several nice features:
- it's the closest to the three clock inputs
- it's the same width as the 7404 so if you put it on U63, they will match nicely
- most importantly, it provides the needed VCC and GND pins

As if this wasn't enough, another important feature of a clock patch is which *family* (or technology) the 740x was used to manufacture given gate. There are [many families](https://en.wikipedia.org/wiki/7400_series#7400_series_derivative_families) available, I focus only on those interesting to us:
- **74F0x**: "Fast" 740x, 3.4ns gate delay
- **74LSx**: "Low-power Schottky", 10ns gate delay
- **74HCTx**: "High-speed CMOS TTL voltage", 8ns gate delay

To make things even more confusing, various manufacturers guarantee different delay times. So it does matter whether the gate is manufactured by Motorola (in the past...), Philips or Fairchild. The manufacturer can be sometimes guessed from the gate name prefix, for instance:
- **SN740x**: Texas instruments, Fairchild, ...
- **DM740x**: National semiconductor, ...
- **MC740x**: Motorola (for historical reasons)

But it's not guaranteed, it's not unusual that more than one manufacturer share the same prefix. And often there's no prefix at all and you just have to look it up in catalogue (or via Google). Seriously, WTF?

The delay means how much time the gate needs to perform given operation. As you will see, this is very important factor for different clock patches!

To make our 7404 journey complete, the "N" suffix means plastic through-hole DIP package, in other words, the usual long legs so you can solder them to U63's legs. Strangely, even this has influence on the clock patch quality, other packages (for instance those SMT-like ICs) are said to work much less reliably in certain scenarios.

## Why does it exist?

The problematic parts of Falcon's design are demonstrated here:

![Image of PCB without clock patch](BaseFalcon.png)

We can see that the main clock signal (16.1079525 on NTSC machines, 16.042494 MHz on PAL/Péritel) goes from the Combel (also known as the Combo IC :)) via **R21** (27 Ω, back side of PCB), having **C208** (10 pF, back side of PCB; not present on PCB since rev.H) as a low pass filter and finally through **R217** (0 Ω) right into three resistors: **R216** (33 Ω), **R221** (33 Ω, changed to 0 Ω in PCB rev.H) and **R222** (33 Ω).

Why there has to be a 0 Ω resistor (R217) I have no clue but it's not that what causes trouble. The problem are those three clock signals branching from it, esp. the one going to the SDMA (*Sound and SCSI Direct Memory Access*, did you know?) where the clock travels first to the FPU and then to the other end of the PCB.

Those three paths basically distribute the main clock to all important Falcon ICs so they can work synchronously. Unfortunately, those paths are very poorly shielded so one IC can very easily disturb another. Especially in the cases with high data bus load (typically displaying video in high resolutions) SDMA problems become nearly unavoidable.

Sane solution would be to make those paths as short as possible and of course make each path buffered.

Atari hadn't realised the problem until it was too late. As you can see in the [schematic / PCB history log](history.md), the first attempt to fix had appeared in August 1993, i.e. by the time when Atari would be shutting down Falcon manufacturing.

## How do I know I need it?

There are two or three typical symptoms (as mentioned, typically surfacing in higher resolutions):
- SCSI read/write errors, corrupted data
- crackles during sound playback (corrupted data between SDMA and DSP and/or DAC)
- Floppy disk read/write errors (especially in Falcons with accelerated bus)

As you can see, the worst possible scenario is recording audio, using DMA run it trough the DSP and write output to a SCSI disk in 720x512x16bit resolution. :)

## How and where the mod is done?

Not surprisingly, the heart of all changes are always those three/four resistors because they are exit points to the three clocks - A, B and C; and the SDMA itself (because that's where the errors happen).

I wish I could tell you that those gates are doing some well defined operation which Atari engineers just forgot to implement. The truth is that nobody really knows what's happening there and why the gates help (!).

There are various theories what effect the gate(s) and/or resistors and/or capacitors have on the clock paths:
- the basic idea is that the gates serve as some kind of protection against the signal going backwards (if something comes to an output pin, it wont get trough the gate)
- effect of a delay: resulting in SDMA's clock input either being phase shifted or even delayed by whole tick what leads to avoiding a conflict on data bus
- weaker signals or better filtered signals (less prone to fail due to random noise)
- different voltage levels
- different impedance

### Variant 1.1
### Variant 1.2
### Variant 1.3
### Variant 1.4
### Variant 2.1
### Variant 2.2

## How do I know it worked?

## References

Credit where credit's due! Sorted by volume of information taken from there:

[Atari Falcon030 Service Guide](http://dev-docs.atariforge.org/files/Atari_Falcon030_Service_Guide.pdf) hosted by Lonny Pursell

[Clock patch explanation in JoyAIP](http://phoenix.inf.upol.cz/~opichals/libhyp/hypview.cgi?url=http://joy.sophics.cz/joyaip.hyp&dstenc=latin2&index=93) by Petr Stehlík

[Chip'n Chips](phoenix.inf.upol.cz/~opichals/libhyp/hypview.cgi?url=http://dev-docs.atariforge.org/files/chips.hyp) by Michael Ruge and hosted by Lonny Pursell

[DoIt Falcon030](http://dev-docs.atariforge.org/files/Doit_Archives-ELiTE_2006.zip) by Robert Schaffner, published by ELiTE and hosted by Lonny Pursell

[Falcon troubleshooting](http://members.optusnet.com.au/~startreks/falccct.html) by Claes Holmerup (found on the [website](http://members.optusnet.com.au/~startreks/falccct.html) by Mark Bedingfield)

[Falcon clock signals](https://mikrosk.github.io/ct60tos/rodolphe.czuba.free.fr/Museum/F30_Clocks.jpg) by Rodolphe Czuba

[Phantom installation manual](http://www.volny.cz/boban07/PhantomS/phantom_manual.rtf) by and discussion with Ctirad Feřtr

[Falcon acceleration problems](http://www.stcarchiv.de/stc1998/06/falcon-beschleunigen) by Michael Ruge
