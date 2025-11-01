# === Memory map

<table style="text-align: center">
<tr style="background-color: #9ccc65"><td><b>Address start <td><b>Address end <td> <b>M7 <td> <b>M4 <td> <b>Notes </td>
<tr style="background-color: #Dcedc8"><td>0x0000 0000 <td> 0x0000 FFFF <td> ITCM <td> VTOR REMAP <td>
<tr style="background-color: #c5e1a5"><td>0x0001 0000 <td>0x07FF FFFF <td colspan=2> Reserved <td>
<tr style="background-color: #Dcedc8"><td>0x0800 0000 <td>0x080F FFFF <td colspan=2> User Flash Bank 1 <td> Default bank for CM7
<tr style="background-color: #c5e1a5"><td>0x0810 0000 <td>0x081F FFFF <td colspan=2> User Flash Bank 2 <td> Default bank for CM4
<tr style="background-color: #Dcedc8"><td>0x0820 0000 <td>0x0FFF FFFF <td colspan=2> Reserved <td>
<tr style="background-color: #c5e1a5"><td>0x1000 0000 <td> 0x1001 FFFF <td colspan=2> SRAM1 (Alias) <td> Alias to preserve the<br>harvard architecture for CM4;<br>References further SRAM1 section
<tr style="background-color: #Dcedc8"><td>0x1002 0000 <td> 0x1003 FFFF <td colspan=2> SRAM2 (Alias) <td>Alias to preserve the<br>harvard architecture for CM4;<br>References further SRAM2 section
<tr style="background-color: #c5e1a5"><td>0x1004 0000 <td> 0x1004 7FFF <td colspan=2> SRAM3 (Alias) <td>Alias to preserve the<br>harvard architecture for CM4;<br>References further SRAM2 section
</table>

> ***TODO*** - dokończyć

# === Option bytes
Option bytes allow you to configure:
- R/W memory protection;
- BOR level;
- watchdog SW/HW;
- reset when the device is in Standby or Stop mode;

> The bytes are coded in little-Endian format.

# === Configuring boot address
Boot address are configured using registers `BOOT_CM7_ADD0` and `BOOT_CM7_ADD1` for the CM7 core and by using registers `BOOT_CM4_ADD0` and `BOOT_CM4_ADD1` for the CM4 core, depending on the value of the input pin `BOOT0`. Changing the state of the pin from logical `0` to logical `1` changes selected boot addresses for **both cores**.

> **CM7** core uses the user FLASH memory **bank 1** and the **CM4** core uses the user FLASH memory **bank 2** as the **default** setting, and by default boot from the **starting addresses** of these banks.

> ***TODO*** - dokończyć

# === RAM sections

The AHB masters can perform Read/Write-access the SRAM sections in parallel with the Ethernet MAC or the USB OTG HS peripherals when accessing separate SRAM sections.

## -- D1 Domain
### ::: AXI SRAM (@ 0x2400 0000)
- Accessible by all system masters except BDMA through D1 domain AXI bus matrix;
- Can be used for application data which is not allocated in DTCM RAM or reserved in graphic objects;

## -- D2 Domain
### ::: AHB SRAM1 (@ 0x3000 0000)
- Accessible by all system masters except BDMA through D2 domain AHB matrix;
- AHB SRAM1 can be used as DMA buffers to store peripheral I/O data in D2 domain;
- AHB SRAM1 can be used as code location for M4, accessible when D1 domain is powered off;

### ::: AHB SRAM2 (@ 0x3002 0000)
- Accessible by all system masters except BDMA through D2 domain AHB matrix;
- AHB SRAM2 can be used as DMA buffers to store peripheral I/O data in D2 domain;
- AHB SRAM2 can be used as Read/Write segment for M4;

### ::: AHB SRAM3 (@ 0x3004 0000)
- Accessible by all system masters except BDMA through D2 domain AHB matrix;
- AHB SRAM3 can be used as buffers for Ethernet or USB I/O;
- AHB SRAM3 can be used as shared memory between M7 and M4 cores;

## - D3 Domain
### ::: AHB SRAM4 (@ 0x3800 0000)
- Accessible by most of the system masters through D3 domain AHB matrix;
- AHB SRAM4 can be used as BDMA buffers for peripheral I/O data in D3 domain;
- AHB SRAM4 can be used to retain some application code/data when D1 and D2 domains enter DStandby mode;
- AHB SRAM4 can be used as shared memory between M7 and M4 cores;

## --- Exclusive RAM

M7 core possesses exclusive access to two more sectors:

### ::: DTCM RAM (@ 0x2000 0000)
- Accessible by M7 core and MDMA through AHBS slave bus of the M7 core;
- DTCM RAM can be used as Read/Write segment to host critical real-time data (eg. stack and heap) for M7 application;

### ::: ITCM RAM (@ 0x0000 0000)
- Accessible by M7 core and MDMA through AHBS slave bus of the M7 core;
- ITCM RAM can be used to host code for time-critical routines (eg. ISRs) that require deterministic execution;

## --- Aliasing
For the M4 core, the D2 SRAMs are aliased in order to preserve the Harvard architecture, and use addresses:
- AHB SRAM1: 0x1000 0000;
- AHB SRAM2: 0x1002 0000;
- AHB SRAM3: 0x1004 0000;

These addresses are accessible through AHB D2 domain matrix.

# === Operations on FLASH memory

TODO

## --- Reading from FLASH memory

TODO

## --- Writing to FLASH memory

**1**. Unlock FLASH control registers using *HAL_FLASH_Unlock()*;
> This unlocks both banks

**2**. Set *PB* bit in the *CR1* / *CR2* flash register for enabling write operation to FLASH bank 1 or FLASH bank 2 respectively. They are set independently and can be set simultaneously;
**3**. Write to FLASH memory using *HAL_FLASH_Program()*.
**3.1**. *ProgramType* is *FLASH_TYPEPROGRAM_FLASHWORD*, and it configures the flash process to write a full *FLASH word* which in case of STM32H75x/74x is *256* bits;
**3.2**. FLASH memory address must be in the range of either *user FLASH bank 1* or *user FLASH bank 2*, but must be aligned to *256 bits*;
**3.3**. Data address is a pointer to the data that has to be cast to *uint32_t*. It must be aligned to *32 bits*. If the data to be flashed is not contiguously *256-bit-long*, FLASH space after the data length will be filled with whatever was placed after the data in the source memory;

> __IMPORTANT__ : The last part constitutes a **buffer overflow vulnerability** and **vulnerability to code injection**, and any function that performs write to FLASH memory must guard against it, typically by adding padding after the data to fill the full FLASH word.

**3.4(\*)**. If you try to program into FLASH memory the contents of a buffer that holds more than one FLASH word bits, you need to do it iteratively repeating step **3**.

**4**. Clear bit *PB* from the corresponding *CR1* / *CR2* register;

**5**. Lock the flash control registers using *HAL_FLASH_Lock()*.

## --- Erasing FLASH memory

TODO

# === Operations on SRAM shared memory

TODO

## --- Reading from shared SRAM memory

TODO

## --- Writing to shared SRAM memory

TODO