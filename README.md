Fork of the DS1054Z_BodePlotter adapted to use Feeltech FY6900 or similar signal generators


# DS1054Z_BodePlotter
A Python program that plots Bode plots of a component using a Rigol DS1054Z Oscilloscope and a JDS6600 DDS Generator.

A [Bode plot](https://en.wikipedia.org/wiki/Bode_plot) shows the  frequency response of a system plotted in a phase and a amplitude graph.

# Requirements
DS1054Z_BodePlotter needs a numpy/scipy/matplotlib environment. Under Linux Distros you can install these via package manager ([See here](https://www.scipy.org/install.html) for more informations).
Under Windows you can use [Anaconda](https://www.anaconda.com/).

Further you will need to install pyserial, DS1054Z, and (optional) zeroconf. You can do this via pip:
``` pip install pyserial ds1054z zeroconf ```

# Hardware setup
Connect your Feeltech FY6900 AWG via USB with you computer and connect the DS1054Z to network (via Ethernet port).

Connect the Channel 1 output of the FY6900 to CH1 of the DS1054Z and to the input of the component you want to test (DUT = Device under test). Connect CH2 of the DS1054Z to the output of the DUT.

![Schematic](https://github.com/jbtronics/DS1054_BodePlotter/raw/master/examples/BodePlotter_schematic.svg?sanitize=true)

# Usage
The basic syntax is `python bode.py MIN_FREQ MAX_FREQ [FREQ_COUNT]`, so if you, for example, want to test your DUT between 1kHz and 2.2Mhz, with 100 steps (default is 50),
you can do it like this: `python bode.py 1e3 2.2e6 100`.

If you have installed zeroconf, the program will try to find your Oscilloscope automatically, if not you will have to specify the IP via the `--ds_ip` option. Mostl likely you will also have to specify the serial port of the JDS6600, you can do this with `--awg-port`.

By default only the Amplitude diagram is measured and plotted. If you also want to get the Phase diagram, you will have to specify the `--phase` flag.

If you want to use the measured data in another software like OriginLab or Matlab, you can export it to a semicolon-seperated CSV file with the `--output` option.

So a typical command line would like this: ```python bode.py 1e3 2.2e6 100 --ds_ip 192.168.1.108 --awg_port /dev/ttyUSB0 --phase --output out.csv```

By default the amplitude plots are shown with linear voltage scale. If you want to get logarithmic axis you can switch this in the plot windows under Figure options.

To see the full list of possible options call `python bode.py --help`.

# Output examples
Here are some example measurements:
## LC Parallel Resonance Circuit
![LC Amplitude Diagram](https://github.com/jbtronics/DS1054_BodePlotter/raw/master/examples/LC_Amplitude.png)
![LC Phase Diagram](https://github.com/jbtronics/DS1054_BodePlotter/raw/master/examples/LC_PHASE.png)

## RL high pass
![RL Amplitude](https://github.com/jbtronics/DS1054_BodePlotter/raw/master/examples/RL_Amplitude.png)
![RL Phase](https://github.com/jbtronics/DS1054_BodePlotter/raw/master/examples/RL_Phase.png)

## RC low pass
![RC Amplitude](https://github.com/jbtronics/DS1054_BodePlotter/raw/master/examples/RC_Amplitude.png)
![RL Phase](https://github.com/jbtronics/DS1054_BodePlotter/raw/master/examples/RC_Phase.png)

# License
This program is licensed under the MIT License. See [LICENSE](https://github.com/jbtronics/DS1054_BodePlotter/blob/master/LICENSE) file for more info.

The FyGen.py library was taken from https://github.com/mattwach/fygen
