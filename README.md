📘 SPI Module Description

This Verilog module implements a simple SPI Master Transmitter that sends a 12-bit data frame (din) over the MOSI line using a generated serial clock (sclk). The module operates as a synchronous state-machine and includes automatic chip-select control and a done flag indicating the completion of transmission.

🔧 Key Features
1. SPI Clock Generation

The internal sclkt signal is created by dividing the input clock.

This generated clock drives the bit-shifting process during transmission.

Output sclk is directly mapped to sclkt.

2. 12-bit Serial Data Transmission

Data is loaded into a temporary register (temp) when start is asserted.

Bits are shifted out on MOSI one at a time on each rising edge of sclkt.

Total transmitted frame size: 12 bits (no start/stop bits like UART).

3. Chip Select Handling

CS remains high in idle.

When start = 1, CS is pulled low, indicating the start of the SPI transaction.

After all 12 bits are transmitted, CS returns high.

4. Done Signal

done = 1 for one clock cycle after transmission completes.

Useful for synchronization with external logic or a testbench.

🧠 Internal State Machine

The module uses a 4-state FSM:

State	Meaning
idle	Waits for start signal. CS high, MOSI low.
start_tx	Loads 12-bit data and pulls CS low.
send	Shifts out bits 0–11 of the data on MOSI.
end_tx	Finishes transmission, sets done = 1, raises CS.
🧵 Signal Overview
Signal	Direction	Description
clk	input	System clock
start	input	Begins SPI transmission
din[11:0]	input	12-bit data to transmit
cs	output	Chip Select (active low)
mosi	output	Serial data output
done	output	Asserted when all 12 bits are transmitted
sclk	output	SPI clock
📡 Operation Summary

start = 1 → CS goes low

Module loads din into temp

On every sclkt rising edge, one bit is transmitted via MOSI

After all 12 bits, CS goes high and done = 1

Module returns to idle
