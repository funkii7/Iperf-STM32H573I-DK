# Iperf for STMH573I-DK

Ported existing example[0] of STM for the Nucleo H563ZI Board to the H573 Board.

For more information about the setup refer to the documentation linked in [0].

In order to work on the H573 board, we mostly changed the clock configuration and the pin layout. 

For the differences, see `./diff`

Note that we only ported the relevant stuff for Iperf, so UART and LEDs are not working.

## How to run
- Right click in the project explorer > Import > Import STM32Cube Example
- Search for `Nx_Iperf` and select the one for the `NUCLEO-H563ZI` Board > Press Next and Finish
- Run `git apply ./diff` in the folder
- Compile and flash as usual

## Results
Host: Ubuntu 22.04, iperf version 2.1.5 (3 December 2021) pthreads

Executed commands
- TCP TX: `iperf -s
- TCP RX: `iperf -c 192.168.1.101`
- UDP TX: `iperf -s -u` 
- UDP RX: `iperf -c 192.168.1.101 -u -b 200M`

Average of 10 test runs:
- TCP TX: 85.00 Mbits/sec 
- TCP RX: 93.41 Mbits/sec
- UDP TX: 95.20 Mbits/sec
- UDP RX: 99    Mbits/sec


## Resources

[0] https://github.com/STMicroelectronics/STM32CubeH5/tree/main/Projects/NUCLEO-H563ZI/Applications/NetXDuo/Nx_Iperf
