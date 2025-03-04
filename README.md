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

![Screenshot 2024-12-30 at 10 54 57 AM](https://github.com/user-attachments/assets/60eb60b1-2ce3-4e32-a32c-67e73c51a863)

[SN74AXC4T774 Evaluation Module User Guide](https://www.ti.com/lit/ug/sceu015/sceu015.pdf)

![Screenshot 2025-01-20 at 12 08 34 PM](https://github.com/user-attachments/assets/848fdd0d-9e4f-47ec-8b7a-3a13d67b152f)

[Tag-Connect TC2050-IDC-430-FP](https://www.tag-connect.com/wp-content/uploads/bsk-pdf-manager/TC2050-IDC-430-NL_Datasheet_9.pdf)

## Debugging

![DS0014](https://github.com/user-attachments/assets/1d28b278-2cbf-44ab-912e-0563195944aa)

TCLK & TDO MSP-FET 3.3V

![tdi](https://github.com/user-attachments/assets/241c0b57-2091-4e27-85a2-7853151470a7)

TCLK & TDI MSP-FET 3.3V

## EnergyTrace

Power consumption measured with energy trace when the RF430FRL152H is in LPM0 was roughly 0.69mW. At 2.9V this is 229.7 uA. The MSP-FET FET_VCC supply is powering a TPS72215 1.5V LDO that supplies the RF430FRL152H. Two SN74AXC4T774 chips are also supplied to perform voltage level translation for JTAG between the RF430FRL152H and MSP-FET. The baseline power measurement includes all of these loads and must be accounted for when measuring application specific power consumption. For the RF430FRL152H 190uA in LPM0 at room temperature is typical. 

![power](https://github.com/user-attachments/assets/9c3e63be-e39e-4d79-b6ec-7177775aacb1)

## Modes

### Passive Operation
When no JTAG debug probe is attached, the device is passively powered by the RF field. VDDSW will provide power harvested and regulated from the RF field to the RF430FRL152H and TCAL9539. VDDB is connected to VDDSW but is just an open circuit as no debug probe is present.

### Debug / Programming
When the MSP-FET debug probe is attached (after level translation), the device is powered by FET_VCC 3.3V stepped down to 1.5V provided by the probe and off board voltage regulator. FET_VCC is connected to VDDB and VDDSW providing power to the RF430FRL152H and TCAL9539. It should be possible to measure power consummption using EnergyTrace, it will just have some additional quiescent current from the voltage regulator and level translators that will not be present when powered passively as those components are offboard and only in circuit when the debug probe is attached.

