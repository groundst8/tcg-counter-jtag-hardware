# tcg-counter-jtag-hardware
Off board JTAG level translation to support MSP-FET programming

## Overview

Want to be able to program tcg-counter with MSP-FET but want level translation JTAG specific hardware to be off the main board to keep costs as low as possible since it is mainly for development purposes or in case a device is bricked via over the air updates. Looking at tag connect for a headerless connector option that will not add cost but provide easy access to the JTAG signals required when needed.

## Reference Designs

![Screenshot 2024-11-25 at 8 42 28 PM](https://github.com/user-attachments/assets/1dbe9e8d-86f4-4606-b524-62f4ce33974a)
[RF430FRL152HEVM User's Guide](https://www.ti.com/lit/ug/slau607c/slau607c.pdf)

![Screenshot 2024-11-25 at 8 47 31 PM](https://github.com/user-attachments/assets/aa277a38-1f16-40d6-a896-e80834d5c7cf)
[Low Voltage Translation For SPI, UART, RGMII, JTAG
Interfaces](https://www.ti.com/lit/an/scea065b/scea065b.pdf)

![Screenshot 2024-11-26 at 3 01 13 PM](https://github.com/user-attachments/assets/3ce24a4f-4d93-4d40-9882-c1ec327c1f64)

[MSP Debuggers User's Guide](https://www.ti.com/lit/ug/slau647o/slau647o.pdf)

