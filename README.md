# Empirical Analysis of 5G TDD Patterns Configurations for Industrial Automation Traffic
We investigate the potential of configuring the 5G time division duplex pattern to minimize packet transmission delay in industrial environments. Through empirical measurements using a commercial 5G system, we evaluate different TDD configurations under varying traffic loads, packet sizes and full buffer status report activation.

This repository provides a detailed description of the network configuration used in the experiments, along with the Wireshark traces collected and the delays measured for each packet, considering the different TDD patterns configured and evaluated. These data were used in the paper: 

[1] O. Adamuz-Hinojosa, F. Delgado-Ferro, N. Domènech, J. Navarro-Ortiz, P. Muñoz, S. Mahdi Darroudi, P. Ameigeiras, J. M. Lopez-Soler, 'Empirical Analysis of 5G TDD Patterns Configurations for Industrial Automation Traffic,' in Joint European Conference on Networks and Communications & 6G Summit (EuCNC/6G Summit), pp. 1-6, 2025.

Post-print Available: https://arxiv.org/abs/2504.00912

__If you use data/code from this repository, please cite our paper. Thanks!__

## Testbed Description
The setup comprises seven devices. __5G Amarisoft__ is a general-purpose computer equipped with a PCIe SDR50 card and runs the Amarisoft software to provide a standalone 5G network. The setup also includes two UEs, each consisting of an __Intel NUC BXNUC10I7FNH2__ with a __Quectel RM500Q-GL__ card. Since the 5G system works in licensed bands, it is enclosed in an RF Shielded Test Enclosure, specifically the __Labifix LBX500__ model. And, __SecureSync 2400__ time synchronization server distributes time using the Network Time Protocol (NTP) to ensure time synchronization across devices. 

![Image](https://github.com/user-attachments/assets/b96903cb-0fb6-4a93-8a44-aba7b772e675)

## Experimental Setup
We considered four TDD patterns: TDD 44, TDD 36, TDD 72, and TDD 10. The numbers following TDD indicate the consecutive full slots allocated to DL and UL, respectively. All patterns have a periodicity of 10 slots between UL and DL, except for TDD 10, which has a periodicity of 2 slots. For TDD 10, although no dedicated UL slot is provided, 12 out of 14 UL OFDM symbols are used for data transmission (i.e., as nrofUplinkSymbols), with the remaining symbols acting guard band. For all TDD patterns, the slot duration is 0.5 ms, the minimum duration supported by the Quectel card i.e, $\mu$=1, allowing for the lowest possible packet transmission delay with our equipment. The base station operates with a bandwidth of 50 MHz and transmits in band n79 (4,4 GHz - 5 GHz).

We aim to measure the packet transmission delay in the 5G system for both UL and DL directions, using the outlined TDD patterns. The measurement points within the 5G system are illustrated in the bottom image of the previous figure. Specifically, these points are the NIC of the 5G system, via the UPF, and the NIC of the UE. To measure the delay, we used tcpdump to capture traces from the NIC, identifying packets via the IP header's ID field. Timestamps were extracted and subtracted to calculate the delay. To emulate periodic industrial traffic, we used the Linux tool iperf in UDP mode, with the server and client configured based on traffic direction. Additionally, our work includes measurements of throughput, which refers to the data rate generated by the transmitter, and effective throughput, which represents the rate of data successfully received by the receiver. 

For each TDD pattern, we considered all possible combinations of the following parameters: (a) four traffic load levels, where the same load was applied simultaneously to both UL and DL directions at 10 Mbps, 20 Mbps, 30 Mbps, and 40 Mbps; (b) two packet sizes, using either 100 bytes or 1000 bytes; and (c) two configurations for the \gls{BSR}, one where the full \gls{BSR} is active and another where the full \gls{BSR} is not active. A total of 100,000 packets was generated in each direction for all possible scenarios to provide a sufficient number of samples to derive the distribution of the packet transmission delay.

## Performance Results
The following figures show: (a)  the CDF of packet transmission delay for 100-byte packets with full BSR disabled, under varying traffic loads; (b) the CDF of packet transmission delay for 100-byte packets with the full BSR mechanism enabled; and (c) the CDF of the packet transmission delay considering different packet sizes under low (i.e., 10 Mbps) and high (i.e., 40 Mbps) traffic load scenarios. 

![Image](https://github.com/user-attachments/assets/967ecb96-3d81-47f0-bd0c-df3b3ff24109)

## Measured Data
- Traces captured with tcpdump in .csv files are saved on ```Traces``` folder
- Measured timestamps for each individual packet (at the base station, and the ue) are saved on ```Delays``` folder
- CDFs from these packet transmission delays are saved on ```CDFs``` folder

Both the individual delays of each transmitted packet and the CDFs have been saved in NumPy format. The CDFs for both the uplink and downlink are extracted for a specific scenario, which is stored in file.npz. Additionally, you can also obtain the raw delays. To read them with Python, you can use the following code:

data = np.load(file.npz, allow_pickle=True)

ecdf_dl_x, ecdf_dl_y = data['ecdf_dl_x'], data['ecdf_dl_y'] 

ecdf_ul_x, ecdf_ul_y = data['ecdf_ul_x'], data['ecdf_ul_y']  

time_downlink = data['tiempos_downlink'] 

time_uplink = data['tiempos_uplink']

For the individual delays of each packet, the following code should be used:

data = np.load(file.npz, allow_pickle=True)

timestamps_bs_dl, timestamps_bs_ul = data['timestamps_downlink_bs'], data['timestamps_uplink_bs']

sequences_bs_dl, sequences_bs_ul = data['sequences_downlink_bs'], data['sequences_uplink_bs']

timestamps_ue_dl, timestamps_ue_ul = data['timestamps_downlink_ue'], data['timestamps_uplink_ue']

sequences_ue_dl, sequences_ue_ul = data['sequences_downlink_ue'], data['sequences_uplink_ue']


## Acknowledgment
This work has been financially supported by the Ministry for Digital Transformation and of Civil Service of the Spanish Government through TSI-063000-2021-28 (6G-CHRONOS) project, and by the European Union through the Recovery, Transformation and Resilience Plan - NextGenerationEU. Additionally, this publication is part of grant PID2022-137329OB-C43 funded by MICIU/AEI/10.13039/501100011033 and part of grant FPU20/02621 funded by the Spanish Ministry of Universities.
