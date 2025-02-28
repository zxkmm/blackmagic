# Firmware BMP for STM32F401/STM32F411 MiniF4 aka BlackPill v2 boards

Allows the use of a [BlackPill v2](https://github.com/WeActStudio/WeActStudio.MiniSTM32F4x1) as a Black Magic Probe.

## Pinout

| Function        | Pinout | Alternative pinout 1 | Cluster   |
| --------------- | ------ | -------------------- | --------- |
| TDI             | PB6    | PB5                  | JTAG/SWD  |
| TDO/TRACESWO    | PB7    | PB6                  | JTAG/SWD  |
| TCK/SWCLK       | PB8    | PB7                  | JTAG/SWD  |
| TMS/SWDIO       | PB9    | PB8                  | JTAG/SWD  |
| nRST            | PA5    | PB4                  | JTAG/SWD  |
| TRST (optional) | PA6    | PB3                  | JTAG/SWD  |
| UART TX         | PA2    | PA2                  | USB USART |
| UART RX         | PA3    | PA3                  | USB USART |
| Power pin       | PA1    | PB9                  | Power     |
| LED idle run    | PC13   | PC13                 | LED       |
| LED error       | PC14   | PC14                 | LED       |
| LED bootloader  | PC15   | PC15                 | LED       |
| LED UART        | PA4    | PA1                  | LED       |
| User button KEY | PA0    | PA0                  |           |

## How to Build

```sh
cd blackmagic
make clean
make PROBE_HOST=blackpillv2
```

or

```sh
cd blackmagic
make clean
make PROBE_HOST=blackpillv2 ALTERNATIVE_PINOUT=1
```

## How to Flash with dfu

After building the firmware as above:

* 1) `apt install dfu-util`
* 2) Force the F4 into system bootloader mode by keeping BOOT0 button pressed while pressing and releasing nRST
      button. The board should re-enumerate as the bootloader.
* 3) `dfu-util -a 0 --dfuse-address 0x08000000 -D blackmagic.bin`

To exit from dfu mode just press and release nRST. The newly Flashed BMP firmware should boot and enumerate.

## SWD/JTAG frequency setting

https://github.com/blackmagic-debug/blackmagic/pull/783#issue-529197718

`mon freq 900k` helps at most
