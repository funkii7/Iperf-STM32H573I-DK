# Iperf for STMH573I-DK

Ported existing example[0] of STM for the Nucleo H563ZI Board to the H573 Board.

For more information about the setup refer to the documentation linked in [0].

In order to work on the H573 board, we mostly changed the clock configuration and the pin layout. 

For the differences, see `./diff`

Also we apply a patch of the STM32 community forum[1] for a increased TCP TX performance.

Note that we only ported the relevant stuff for Iperf, so UART and LEDs are not working.

## How to run
- Right click in the project explorer > Import > Import STM32Cube Example
- Search for `Nx_Iperf` and select the one for the `NUCLEO-H563ZI` Board > Press Next and Finish
- Run `git apply ./diff` in the folder
- Run `patch Middlewares/ST/netxduo/common/drivers/ethernet/nx_stm32_eth_driver.c driverpatch`
- Compile and flash as usual

## Results
Host: Ubuntu 22.04, iperf version 2.1.5 (3 December 2021) pthreads

Executed commands
- TCP TX: `iperf -s`
- TCP RX: `iperf -c 192.168.1.101`
- UDP TX: `iperf -s -u -V` 
- UDP RX: `iperf -c 192.168.1.101 -u -b 200M`

Average of 10 test runs:
- TCP TX: 94.9 Mbits/Sec
- TCP RX. 93.0 Mbits/Sec
- UDP TX: 91.2 Mbits/Sec
- UDP RX: 95.0 Mbits/Sec

## Resources

[0] https://github.com/STMicroelectronics/STM32CubeH5/tree/main/Projects/NUCLEO-H563ZI/Applications/NetXDuo/Nx_Iperf
[1] https://community.st.com/t5/stm32-mcus-embedded-software/stm32h573i-dk-poor-tcp-tx-performance-iperf/td-p/642402
