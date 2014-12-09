DualOptiboot6
=============

Custom Optiboot to add wireless programming capability to Moteino and Anarduino
Copyright Felix Rusu (2013-2014), felix@lowpowerlab.com
More at: http://lowpowerlab.com/Moteino

Anarduino's MiniWireless support Copyright Alexandre Bouillot (2014), alexandre@bouillot.org


This Optiboot is derivated from OptiBoot v6 - latest to date - and integrate 
the code changes make by LowPowerLab to support reflashing from an 
external SPI flash memory chip. It remain, by defaut configured to support
Moteino, but integrate changes to support Anarduino's MiniWireless as well.

This Optiboot version is modified to add the capability of reflashing 
from an external SPI flash memory chip. As configured this will work 
with Moteino (www.lowpowerlab.com/Moteino) provided a SPI flash chip
is present on the dedicated onboard footprint.
Summary of how this Optiboot version works:
- it looks for an external flash chip
- if one is found (SPI returns valid data) it will further look
  for a new sketch flash image signature and size
  starting at address 0:   FLXIMG:9999:XXXXXXXXXXX
  where: - 'FLXIMG' is fixed signature indicating FLASH chip
           contains a valid new flash image to be burned
         - '9999' are 4 size bytes indicating how long the
           new flash image is (how many bytes to read)
         - 'XXXXXX' are the de-hexified bytes of the flash 
           pages to be burned
         - ':' colons have fixed positions (delimiters)
- if no valid signature/size are found, it will skip and
  function as it normally would (listen to STK500 protocol on serial port)

-------------------------------------------------------------------------------------------------------------

Add the content of boards.txt to the board.txt located in <arduino_install_dir>/hardware/arduino
It will create an MiniWireless board in the selection menu and allows the bootloader's burning

To compile, go in DualOptiboot folder and compile with command line as
omake miniwirelss
to complete with flashing after compilation,
omake miniwireless_isp

##License
GPL 3.0. See License.txt file.