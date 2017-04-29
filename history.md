## Schematic / PCB history

### PCB flavours

The main PCB has following production numbers:

- **CA401332-001** ASSY PCB FALCON030 NTSC (US/CAN; Atari last revision: J)
- **CA401332-002** ASSY PCB FALCON030 PAL-I (GERMANY, generally most of Western Europe, Australia, and New Zealand; last Atari revision: H)
- **CA401332-003** ASSY PCB FALCON030 PAL-B (UK, generally UK, Ireland, Hong Kong, South Africa, and Macau; last Atari revision: H)
- **CA401332-004** ASSY PCB FALCON030 PERITEL (FRANCE; last Atari revision: A)

### Manufacturers

There had been two large Falcon manufacturers: ATMC and EFA. ATMC had used two sub-contractors, "Golden Horse" (B3) and "ECS Tamsui" (B5), EFA just one, "Ta Yuan" (Y4). EFA had been developing all Falcons since PCB rev. B. List of all Atari manufacturers [here](500277ra.pdf).

### Serial numbers

This is one big mess. According to this diagram in the Falcon030 service manual:

![falcon_serial.png]

it should be pretty straightforward but it is not. There are several discrepancies:

1. **Number of digits**: [ECO statistics document](ECOSTATX.[pdf] uses serial numbers with the control code having "0" prefix, few Falcons developed by B3/B5 and all of the Y4 Falcons follow this scheme, too
2. **Colour encoding**: Early falcons from B3 and B5 follow the rules and include the number indicating colour encoding in their serial number. All of the Y4 Falcons however skip this number (or insert zero there, hard to say with such low sequential numbers) and rely solely on the PCB production number.
3. **Sequential numbering**: It's more or less clear that every factory used its own numbers. However from the numbers I have it seems that the sequence number was reset only once in Y4, in 1994, and it's still not clear whether it was because of new year or because C-Lab had already ordered new machines for their MK I models.

### Manufacturing years

From all the serial numbers I've seen so far one can conclude:

1. First batch happened in 10/1992 in B5, this was also the only batch producing Peritel models
2. Second batch happend during 02-04/1993 in B3
3. Third batch happend during 03-09/1993 in Y4
4. Fourth batch happend in 01-??/1994 in Y4 (for C-Lab MK I models?)
5. Fifth and the last batch happened in 09/1994 in Y4 for C-Lab MK II and MK X models

If we can trust the ECO statistics document, it's really hard to believe that if the last approval activity for Falcon stuff had happend around 06-07/1993 that Atari Corp. would produce new batch of Falcons in January 1994.

Sometime in 09/1994 (judging from MK II serial numbers) C-Lab had ordered by EFA another batch for the MK II/X models which were delivered around 08/1995 according to [this article](http://www.stcarchiv.de/stc1995/05_sylvie.php) in ST-Computer.

Another rather confusing fact is that revisions are not always related to manufacturing years. So it's totally OK to see rev. D/C from 01/1994 and rev. J from 07/1993.

### Number of Atari Falcons manufactured

In [this intereview](http://stcarchiv.de/stc1993/10/interview-atari-bob-gleadow) in ST-Computer, Bob Gleadow, Managing Director at Atari Deutschland GmbH, claimed that in 10/1993 Atari had sold around 13,000 - 14,000 units and had 4164 units in stock.

Taking into account the fact that Falcons by Bx factories are counted in hundreds, Y43x Falcons seems to have the same sequential ordering (at least I haven't seen yet a newer Y43x Falcon with s/n lower than an older Y43x Falcon) with highest number being 11903 so far and that C-Lab had ordered only a couple of thousands, it's safe to assume the number isn't higher than 20,000.

### PCB revisions

Schematic C303007-001 rev. | Schematic rev. date | PCB rev. | PCB approval date | Description | PCB rev. changes | Notes
-------------------------- | ------------------- | -------- | ----------------- | ----------- | ---------------- | -----
A	| 23/07/1992 ||| Initial release
B	|	25/08/1992 ||| Revised per ECO #1488 [![Image of ECO #1488](Eco1488_preview.png)](Eco1488.png)
C	|	25/08/1992 ||| Revised per ECO #1492
D	|	25/08/1992 ||| Revised per ECO #1497
E	|	|||			Revised per ECO #1498 [![Image of ECO #1498](Eco1498_preview.png)](Eco1498.png)
F	|	10/09/1992 | A || Revised per ECO #1505	| NTSC A, PAL-I/B A, PERITEL A | Production release, manufactured in 10/1992 by ATMC's "Golden Horse" and "ECS Tamsui"; PERITEL models had socketed CODEC and no RF modulator
G	|	06/01/1993 | B | 26/01/1993 |	Revised per ECO #1600 [![Image of ECO #1600](Eco1600_preview.png)](Eco1600.png) || Manufactured by EFA's "Ta Yuan" ever since; there's no PERITEL version manufactured anymore
H	|	20/01/1993 | C | 16/03/1993 |	Revised per ECO #1604 [![Image of ECO #1604 1/2](Eco1604_1_preview.png)](Eco1604_1.png) [![Image of ECO #1604 2/2](Eco1604_2_preview.png)](Eco1604_2.png)
|| D | 16/03/1993 | Revised per ECO #1613 || Common D/C release, manufactured for Atari between 03/1993 - 09/1993, later sold by C-Lab as MKI models
|| E |	02/03/1993 | Revised per ECO #1621
|| F | 30/04/1993 | Revised per [ECO #1625](Eco1625.pdf) || Corrected error made on ECO #1604
J	|	11/06/1993 | G | 04/08/1993 | Revised per [ECO #1642](Eco1642.pdf) | NTSC G | Improved video quality for NTSC machines
K	|	06/08/1993 | H | 04/08/1993 | Revised per [ECO #1643](Eco1643.pdf) [![Image of ECO #1643](Eco1643_preview.png)](Eco1643.png) |	NTSC H, PAL-I/B G	| Attempt to fix sound crackle during DMA playback
L	|	06/08/1993 | J | 04/08/1993 | Revised per ECO #1641 [![Image of ECO #1641](Eco1641_preview.png)](Eco1641.png) | NTSC J, PAL-I/B H
||||| PAL J | Strangely, there are records of Falcons from 07/1993 with this revision. Maybe done by an Atari dealer in post production to D/C PCBs?
||||| PAL K |	C-Lab Falcon MKII, manufactured in 09/1994

Schematic 500047-001 rev. | Schematic rev. date	| Description | Notes
------------------------- | -------------------	| ----------- | -----
1	|	06/01/1993 ||Initial release (spin-off from rev.G?)
A	|	01/03/1993 || Engineering release
B	|	13/05/1993 | Revised per ECO #1644 | Production release
