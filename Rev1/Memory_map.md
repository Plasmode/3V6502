# Memory Map of Rev1 3V6502
RAM $0-$EFFF. $0-$3FFF are common RAM; there are two banks of RAM from $4000 to $EFFF controlled by bank register. D[0] of bank register selects the banks. Bank register is cleared on reset.


Bank reg = $FB12, D[0] selects the banks; Bank register is cleared on reset. D[1]-D[7] are don't care bits.

PS2CLK control register = $FB14. D[0] controls the PS2CLK output. Writing '1' to PS2CLK reg causes PS2CLK output to float allowing an external pull up resistor to pull it high. Writing '0' to PS2CLK reg causes PS2CLK output to go low. PS2CLK register is preset to 1 at reset thus its output is floating. Writing to D[1]-D[7] have no effects

PS2Data line is clocked in with the falling edge of PS2CLK. Reading PS2CLK control register at $FB14 display the value of PS2Data at D[7] and the value of PS2CLK at D[6].

Hsync Status register = $FB40. D[0] displays state of last Hsync line. D[0] is high wheh 525th line is reached. Next Hsync will be the first line at top of the screen. Interrupt is generated when Hsync is low, which last 100 clocks (25.175MHz)

Pixel shifter snoops data in addresses $4000-$EFFF; another word, accessing addresses in the range of $4000-$EFFF will load the data bus value into pixel shifter. This is the mechanism to load graphic data located in $4000-$EFFF and shift them out to video display.

SerData $fbc1
SerStat $fbc0

SPI register at $FB68 or $FB69.

RTC register is at $FB10 or $FB11

Flash disable register is at $FBFF, this is a write-only register. Writing '0' to D[0] of $FBFF disable the CPLD internal flash memory at $F000-$FFFF and replace it with RAM. D[0] is preset to '1' at reset. D[1] to D[7] are don't-care bits.
