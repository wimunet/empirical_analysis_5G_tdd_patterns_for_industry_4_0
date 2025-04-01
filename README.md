# Empirical Analysis of 5G TDD Patterns Configurations for Industrial Automation Traffic
We investigate the potential of configuring the 5G time division duplex pattern to minimize packet transmission delay in industrial environments. Through empirical measurements using a commercial 5G system, we evaluate different TDD configurations under varying traffic loads, packet sizes and full buffer status report activation.

This repository provides a detailed description of the network configuration used in the experiments, along with the Wireshark traces collected and the delays measured for each packet, considering the different TDD patterns configured and evaluated. These data were used in the paper: O. Adamuz-Hinojosa, F. Delgado-Ferro, N. Domènech, J. Navarro-Ortiz, P. Muñoz, S. Mahdi Darroudi, P. Ameigeiras, J. M. Lopez-Soler, 'Empirical Analysis of 5G TDD Patterns Configurations for Industrial Automation Traffic,' EuCNC, pp. 1-6, 2025.

__If you use code from these repositories, please cite our paper. Thanks!__

## Setup
The setup comprises seven devices. __5G Amarisoft__ is a general-purpose computer equipped with a PCIe SDR50 card and runs the Amarisoft software to provide a standalone 5G network. The setup also includes two UEs, each consisting of an __Intel NUC BXNUC10I7FNH2__ with a __Quectel RM500Q-GL__ card. Since the 5G system works in licensed bands, it is enclosed in an RF Shielded Test Enclosure, specifically the __Labifix LBX500__ model. And, __SecureSync 2400__ time synchronization server distributes time using the Network Time Protocol (NTP) to ensure time synchronization across devices. 

