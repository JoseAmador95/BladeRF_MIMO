# BladeRF_MIMO

MATLAB and Simulink Interface for the BladeRF MIMO layout. These scripts are a modifyied version of the 
[original scripts](https://github.com/Nuand/bladeRF/tree/master/host/libraries/libbladeRF_bindings/matlab) 
provided by Nuand. The modifications were done as described in the [libbladeRF API documentation](http://www.nuand.com/libbladeRF-doc/v2.2.1/).

* Created as part of research on 

```User Equipment Tracking Beamforming Using a MIMO Software-Defined Radio```


## You are here

* https://github.com/JoseAmador95/BladeRF_MIMO


### Return to UoS Beamforming By JoseAmador95

* https://github.com/JoseAmador95/UoS_Beamforming

#### 

* Model setup script
* Simulations
  * Modulatior and Receiver simulation test model
  * TX Beamformer simulation test model
  * RX Beamformer simulation test model
  * Theoretical Radiation pattern generator
  * User Equipment tracking simulation
* Real Implementation
  * [MIMO Interface for the BladeRF](https://github.com/JoseAmador95/BladeRF_MIMO) <---------- You are Here
  * MIMO SDR layout test model
  * User Equipment tracking model
* CAD
  * Fusion 360
  * STEP
* [Report](https://github.com/JoseAmador95/UoS_Beamforming/blob/master/Report.pdf) <----- Great Reference

## Requirements
The MIMO objects require an older version of the BladeRF release. The recommended version is [2019.07](https://github.com/Nuand/bladeRF/releases/tag/2019.07). Particularly, 2021.02 is incompatible. Please let me know if a workaround is found for the newer version.

## How to Use
These scripts require the official tools from [Nuand](https://www.nuand.com/support/); include the root directory into
MATLAB's path. To use within Simulink, copy the scripts in this repo into the working directory and introduce a _MATLAB System_
block (From Simulink/User-Defined Functions) into the Simulink model and select _bladeRF_MIMO_Simulink.m_. Make sure to test the 
BladeRF using Nuand's BladeRF CLI and to close all of its instances before running the Simulink model.

## How was this done
The [original scripts](https://github.com/Nuand/bladeRF/tree/master/host/libraries/libbladeRF_bindings/matlab) allow to transmit 
and receive signals from a single channel of the BladeRF; leaving the other channel unused. The scripts in this repo enables every 
channel in the SDR, executes the synchronous TX/RX functions considering the 2x2 layout and interleaves/de-interleaves the samples 
according to the [streaming format](http://www.nuand.com/libbladeRF-doc/v2.2.1/group___s_t_r_e_a_m_i_n_g___f_o_r_m_a_t.html#ga4c61587834fd4de51a8e2d34e14a73b2).

## Known Issues
Altough these scripts do transmit and receive samples as expected, some stability issues exist when opening and closing the device.
Some of these issues are not causes by the modifications to support the MIMO layout, as they are also present in Nuand's scripts.

These issues cause the SDR to become unreachable for any application until the PC is rebooted or the user logs-in again (Windows).

* Stoping the Simulink model execution may cause an issue, but not every time.
* Modifying the gain of either the TX and RX front-ends at runtime causes an issue every time.


