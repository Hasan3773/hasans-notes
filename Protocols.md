**CAN (Controller Area Network):

Shared bus, so that there is no master device
The bus is just two differential pair of wires, a can signal is the difference between the two wires
Terminating (120 ohm) resistors at both ends of the bus, prevents signal reflections
Each CAN Node has an ID, each node tries to transmit its ID, if it gets overpowered, it stops and waits its turn, so the lower IDs overpower higher IDs (0000000 > 0000001)
The way a Node knows if it won the arbitration is if it reads back its node ID from the CAN bus

**UART (Universal Asynchronous Receiver / Transmitter):

Ex: Serial COM ports, modems, Arduino
It's a very simple protocol for sending serial data between two devices
Only uses two wires (TX & RX)
It can be simplex, half-duplex or full-duplex
Data is transmitted in frames
Is asynchronous - the two devices don't share a clock, which mean they both have to operate at a known speed (baud rate)
UART frames consists of:
- Start / Stop bits
- Data bits (5-9 bits) (LSB First - reverse the data of what you're sending)
- Parity bit (even - number of 1 is even, odd - opposite) checks before and after data is sent to make sure no errors have occurred. ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd0sfwLIdk8ncEhXj7xhxj63YTam3l7szAsOd2RRd6Zw9Mset9Bp-lP5eIPAd1npkvTz4D88qi1xMOgyVpRxB8_mVVGzZid-AUDiQC759axjyAQY-8EAc-d6tZOeY9cVl_MWplIIcYKM6VuDgyTydf7NnDT?key=96Zz1iNouwiYhGNilCw3Ng)**

**SPI (Serial Peripheral Interface):

Four wire serial interface, faster than UART and I2C, full-duplex
Generally used to transfer data between a smart controller and a less smart peripheral device Ex: Sensors, ADCs, RTC’s.
One master and one or more slaves connected with 4 wires.
Chip select line - chooses which slave
SCLK line - provides timing / synchronizes devices (MHz range) - Only master generates clock signal
MOSI - Master Out Slave in, data sent by master (LSB or MSB)
MISO - Master In Slave Out, data received by master - Sent as a response to data on MOSI, the master queries the slave for how many bits it's going to send, then generates the corresponding clock cycles
Steps: The master sets the CS line low to indicate data is incoming, then starts the clock, then the master can send / receive bits
Clock polarity (CPOL): Can be active high - Idle low or Idle high - Active low,  Forcen’s ADC was Idle high - Active low (CPOL = 1). 
Leading edge is the first edge of a clock pulse and the Trailing edge is the second. So for CPOL = 0, the leading edge is rising and for CPOL = 1 the leading edge is falling.
Clock phase (CPHA): Which edge of the clock is the data sampled on, CPHA = 0 is when it's on the leading edge, CPHA = 1 is when it's sent on the trailing edge. 
For the 4 different combinations of CPOL and CPHA, there is a corresponding SPI mode, 0-3, all SPI devices in a system have to be the same mode.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe4KAeROhkjgrOUtEBlg7wFVg-ZxkP9Hiz-3cvRtuJmTckEb5akIQgQtQaOe8-9CCCooeqo_al2lIrQfPPeFIoS2EfRJ4OGu1c6ki6VsHc5uVwIT5CUQZvE5-WTpuVKrQwB4GJyF8Jyi9tHvrSc9qO3FfQ?key=96Zz1iNouwiYhGNilCw3Ng)  
  
  
**I2C (Inter Integrated Circuit): 

Used for communication inside of ICs
Only two lines, SCL( Serial Clock Line) & SDA (Serial Data Line)
Two pull up resistors connected to both lines, pulling up the voltage
One bus connects to all slaves
Built in addressing
Half- duplex, cannot send and receive at the same time (400 kbps)

The way it works is that because the pull up resistor has the lines constantly pulled up to its voltage because both the master and the slave have their gates open (usually just a MOSFET transistor), the voltage is high across the circuit. So to send a 0 you just close the gate, completing the circuit and making the voltage across the bus 0V. 

The reason that I2C needs the pull up resistors rather than just letting all the devices pull up the lines themselves, is to solve the issue where multiple devices try to pull the line up at the same time which would create a short, so rather if multiple lines try to use the line at the same time, they would just pull the line to low, not creating a short. (if multiple devices try to use pull down the line, the slower device wins)

The start condition: 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdtq4jgvxUedl0w6UQVyJ44Im__8b0-KOUR2nZQbERoxTLidlfgC2OKsrsnyO2b-Oe7Q66KtOxu6wmBoH32ZOiAS02VZdh6ADhSWdgOiL_aPIkJMyhcn2i-oSLz06aneA_uI5IP0jvGHCXpMzW6j9yRg-6j?key=96Zz1iNouwiYhGNilCw3Ng)