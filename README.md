# moshi
Reverse Engineering Moshiboard

Mosh2-works is the first file where the moshi connected correctly.

Moshi-movement around raster rect. The commands were 0.2mm right many times, then a couple odd commands. Then move around in a rectangle movement. Then I drew a rectangle and sent that to the board. It rastered the rectangle rather drew it as a vector.

The status reads are also different than the M2:

MOSHI
ff cd 6f 08 00 00 -- IDLE
ff cf 6f 08 00 00 -- Machine Busy.
