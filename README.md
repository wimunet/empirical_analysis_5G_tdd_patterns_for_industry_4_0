# Empirical Analysis of 5G TDD Patterns Configurations for Industrial Automation Traffic
We investigate the potential of configuring the 5G time division duplex pattern to minimize packet transmission delay in industrial environments. Through empirical measurements using a commercial 5G system, we evaluate different TDD configurations under varying traffic loads, packet sizes and full buffer status report activation.

This repository provides a detailed description of the network configuration used in the experiments, along with the Wireshark traces collected and the delays measured for each packet, considering the different TDD patterns configured and evaluated. These data were used in the paper: [1] O. Adamuz-Hinojosa, F. Delgado-Ferro, N. Domènech, J. Navarro-Ortiz, P. Muñoz, S. Mahdi Darroudi, P. Ameigeiras, J. M. Lopez-Soler, 'Empirical Analysis of 5G TDD Patterns Configurations for Industrial Automation Traffic,' in EuCNC, pp. 1-6, 2025.

__If you use data/code from this repository, please cite our paper. Thanks!__

## Testbed Description
The setup comprises seven devices. __5G Amarisoft__ is a general-purpose computer equipped with a PCIe SDR50 card and runs the Amarisoft software to provide a standalone 5G network. The setup also includes two UEs, each consisting of an __Intel NUC BXNUC10I7FNH2__ with a __Quectel RM500Q-GL__ card. Since the 5G system works in licensed bands, it is enclosed in an RF Shielded Test Enclosure, specifically the __Labifix LBX500__ model. And, __SecureSync 2400__ time synchronization server distributes time using the Network Time Protocol (NTP) to ensure time synchronization across devices. 

![Image](https://github.com/user-attachments/assets/b96903cb-0fb6-4a93-8a44-aba7b772e675)

## Experimental Setup
We considered four TDD patterns: TDD 44, TDD 36, TDD 72, and TDD 10. The numbers following TDD indicate the consecutive full slots allocated to DL and UL, respectively. All patterns have a periodicity of 10 slots between UL and DL, except for TDD 10, which has a periodicity of 2 slots. For TDD 10, although no dedicated UL slot is provided, 12 out of 14 UL OFDM symbols are used for data transmission (i.e., as nrofUplinkSymbols), with the remaining symbols acting guard band. For all TDD patterns, the slot duration is 0.5 ms, the minimum duration supported by the Quectel card i.e, $\mu$=1, allowing for the lowest possible packet transmission delay with our equipment. The base station operates with a bandwidth of 50 MHz and transmits in band n79 (4,4 GHz - 5 GHz).
