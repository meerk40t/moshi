# moshi

Reverse Engineering Moshiboard

Moshiboards were a popular laser control board circa 2013. They ran with Moshidraw and came with a dongle. Also, the view of the chip looked highly similar to the M2 Nano board setup, the use of CH341 chips for both. For these reasons it was theorized that they were an early version of this same sort of format. And a goal was set among meerk40t designers to do a secondary project including reverse engineering of the moshiboard's control structure.

A Moshiboard was donated to the cause early in April of 2020. This was hooked up and with the use of Wireshark initial attempts were made to do the reverse engineering of the command structures, in hopes, in part of quickly running a secondary method of making a compatable device.

The early results are in.

# Known Knowns.

* The internal format uses a cache on the board that stores much of the program as the board is running.
* Unplugging the board doesn't change this operation.
* The formating is not relative but absolute in that the exact x and y positions are sent in 2 int_16le values.
* The communications are not sent via A0 packets like in the M2 but rather in A6 and A7 writes.
* Reads are also performed with an AC command. 
* The speed is sent within the command header and is sent purely as a single byte which can set speeds from 1 to 256.
* Stop commands and Unlock Rail commands are done through A7xx sends.

See the wiki page on the project for some examples of this. 
https://github.com/meerk40t/moshi/wiki

# Known Unknowns

* How the format turns the laser on and off. It appears to be part of the hash/formating byte. This is however unknown. In some example code this turn on code causes the byte to always be high. In that it's never less than 128.
* How the format triggers between X and Y values. The rasters do not contain x and y. They usually contain x values, except when they only contain a y value. The standard size of these commands goes for 5 for outlines to being 3 for rasters.
* How the commands end. The jumps seem to have 6 blocks of randomly hashed varying values. These are flagged in a different way and often seem like they are may be repeated commands of neither x or y positions.
* What does the second line indicate. The value is often like `00 xx xx yy yy` but, it's unclear whether this goes there or sets a position or something. The 00 command is unseen elsewhere in such files.
* Why does the system send A7xx before jumps, or other commands? Is there some reason for this value? Does it relate to the command/hash?
* Does this format change a bunch for other versions of the Moshiboard before or after version 4.2?

# Unknown Unknowns
* (shrug)

# Project Future

There's every reason to think this project may be a success and the format can be mapped out to sufficiently run the moshiboard with alternative software. It is however, unknown whether this work would be worthwhile. How many people still have this kind of board or how many people would actually care if open source software could control such a thing? Also, much of the early hope was based around the belief that this board would be substancially similar to the M2 Nano. It's actually substancially smarter and less usable.
