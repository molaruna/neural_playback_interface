# UCSF_benchtop_testing
Benchtop testing setup that allows "playback" of RC+S data into device 

![hardware demo](images/hardware_demo.jpg)

Preprocessing neural data:
-------------

In MATLAB, process the raw recorded neural data into a matlab formatted table and add the file (RawDataTD.mat) to your workspace. Then, transform the data into an audio-compatible format using this MATLAB function: [audioOut.m](code/audioOut.m)


Overview of the DAC setup:
-------------
The audio DAC has four output aux cables that feed into the copper Faraday cage and are then used as inputs for the circuit.
Each aux cable contains two signal (white) and one ground (black) wire, which you can see inside of the Faraday cage.
The signal from the black wire travels directly to the RCS body by conducting electricity through the copper RCS holder. The signals from the white wires travel through the circuit on the perfect and to the leads of the RCS via the 3D printed lead holder.

**The RCS must be inside the holder for the setup to be properly grounded.**

On the output end of the circuit, the rainbow colored wires send signal to the contacts of each lead.
I've hooked the wires up so that aux cable 1 records from contacts 0-2, aux cable 2 records from contacts 1-3, and so on.

Using the DAC setup:
-------------
* Setup and/or check the wiring: 
  - The cables from audio DAC outputs 1-4 should travel to corresponding Faraday Cage aux jack inputs 1-4. 
  - The black and white wires inside the Faraday Cage should travel from Faraday Cage outputs 1-4 to the circuit perfboard inputs 1-4. The black wires (ground) of each cable block should all be on the outermost side of the perfboard. 
  - Default setup -- The rainbow wires from the circuit perfboard output should be connected to every other contact input so that aux cable 1 records from contacts 0-2, etc.
* Placing the RCS components in the Faraday Cage:
  - Place the RCS body inside the copper holder.
  - Place the lead(s) inside the white lead holder. Make sure the contacts of the lead are making direct contact with the metal springs inside the holder. 
  - Place the CTM inside the smaller compartment of the Faraday cage and shut the lid. You'll need to rotate the battery out for the CTM to fit. There is a cardboard holder to rest the battery.
* Connect the audio DAC to either a macOS or windows machine with a USB-C cord.
* Minimize all unnecessary wiring on the computer connected to the audio DAC.
* Recommended baseline -- record noise while the lid is shut without playing data for 5 minutes to make sure the setup is working properly.

Your baseline noise level should look something like this: 
![baseline noise level](images/baseline_check_closed.jpg)

To create a graph like the one above, use MATLAB's `pspectrum` function.

Lastly, before playing back real neural data, you may also want to test an active baseline signal by playing simple test data, such as a sine wave.

Summary checklist before collecting data:
-------------
* Add all RCS & DAC components to Faraday Cage setup
* Check that all wires are correctly and securely connected
* Avoid ground loops by minimizing any additional wires (don't charge your laptop while recording)
* Test multiple baseline states before playing back neural data
