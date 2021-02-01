# Current State

The project is a success.

This project was used to write Moshiboard drivers for MeerK40t. This was added in 0.7.0-beta-3 and shown to be effective at controlling the moshiboard.

# Project Future

Archiving. Documentation will be made for the Moshiboard and left properly running in MeerK40t.


# moshi

Reverse Engineering Moshiboard

Moshiboards were a popular laser control board circa 2013. They ran with Moshidraw and came with a dongle. Also, the view of the chip looked highly similar to the M2 Nano board setup, the use of CH341 chips for both. For these reasons it was theorized that they were an early version of this same sort of format. And a goal was set among meerk40t designers to do a secondary project including reverse engineering of the moshiboard's control structure.

A Moshiboard was donated to the cause early in April of 2020. This was hooked up and with the use of Wireshark initial attempts were made to do the reverse engineering of the command structures, in hopes, in part of quickly running a secondary method of making a compatable device.

There was every reason to think this project may be a success and the format can be mapped out to sufficiently run the moshiboard with alternative software. However for reasons this project was tabled until late January 2021 when it was written and tested. Properly mimicked the laser responded to the commands. The swizzling was unneeded as any form of  any command works for that command.

# Known Knowns.

* The internal format uses a cache on the board that stores much of the program as the board is running.
* Unplugging the board doesn't change this operation.
* The formating is not relative but absolute in that the exact x and y positions are sent in int_16le values.
* The communications are not sent via A0 packets like in the M2 but rather in A6 and A7 writes.
* A7 writes convey a small amount of command information setting the mode for the moshiboard.
* Reads are also performed with an AC command.
* The speed is sent within the command header and is sent purely as a single byte which can set speeds from 1 to 256.
* Stop commands and Unlock Rail commands are done through A7xx sends.
* There are 6 major commands. Cut x,y. Move x,y. Cut-horiz x. Move-horiz x, Cut-vert y, Move-vert y. There are additionally commands for speed info and some z, x, y location data.

See the wiki page on the project for some examples of this. 
https://github.com/meerk40t/moshi/wiki

