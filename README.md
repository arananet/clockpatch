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

The delay means how much time the gate needs to perform given operation. As you will see, this is very important factor for different clock patches!

And also, the manufacturer is importat. In our case the important names are:
- **SN740x**: Texas instruments
- **DM740x**: National semiconductor

And to make our 7404 journey complete, the "N" suffix means plastic through-hole DIP package, in other words, the usual legs so you can solder it to U63's legs.

## Why does it exist?

I wish I could tell you that those gates are doing some well defined operation which Atari engineers just forgot to implement. The truth is that nobody really knows what's happening there and why the gates help (!).

The problematic part of the design is here:

![Image of PCB without clock patch](BaseFalcon.png)

Here we can see that the main clock signal (16.1079525 on NTSC machines, 16.042494 MHz on others) goes from the Combel (also known as the Combo IC :)) via **R21** (27 Ω, other side of PCB), having **C208** (10 pF, other side of PCB; not present on PCB since rev.H) as a low pass filter and finally through **R217** (0 Ω) right into three resistors: **R216** (33 Ω), **R221** (33 Ω, changed to 0 Ω in PCB rev.H) and **R222** (33 Ω).

Atari didn't realise the problem until it was too late. As you can see in the [schematic / PCB history log](history.md), the first attempt to fix had appeared in August 1993, i.e. by the time when Atari would be shutting down Falcon manufacturing.

## How do I know I need it?

## How and where the mod is done?

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
