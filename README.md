Inkscape MockupMachine
=====================

Export Inkscape layer constellations as images in batch.

Installation
============
Copy `MockupMachine.inx` and `MockupMachine.py` to your Inkscape extension directory.
Windows: `C:\Program Files (x86)\Inkscape\share\extensions`

Usage
=====
* Create a config file for SVG file (see below)
* Start inkscape with your SVG file
* Select Extensions -> MockupMachine -> Setup
* Enter the full path to your desired output directory
* Enter the full path to your SVG file
* Hit execute and wait.

Usecase
=======

When creating mockup walkthroughs for websites or applications, one would probably use layers he 
activates and deactivates per screen to show.

Exporting all screens (layer constellations) to images is a pretty boring and time consuming job.

MockupMachine automates this as a Inkscape extension. You only have to write a simple configuration file.

Example included
================

The project includes an example Inkscape-SVG file and a config-file that outputs screen variations from that layers.

The configuration
=================

    Filename ends with a colon:
    + Layer to activate
    - Layer to deactivate
      blank line to end one file (incemental)
    -- line of minus signs to disable all layers again (full reset).

A config file may look like this:

    myfile-1.0:
    + layer1
    + layer2
    
    myfile-1.1:
    - layer2
    + layer3
    + layer4
    -----------------
    myfile-2.0:
    + layer10
    + layer11
    
    myfile-2.1:
    - layer10
    + layer12

This will create the files myfile-1.0.png, myfile-1.1.png, myfile-2.0.png and myfile-2.1.png

Development notes
=================

Inkscape does not provide the file origin path to an extension, only a temp file. 
That's why you have to set it explicitly.

If you want to modify the script, don't use `print` to debug, use `inkex.debug` instead. 
Using print() will crash inkscape because it currupts the output SVG file.

I suffered a lot with paths including german umlauts and whitespaces. Keep that in mind.

I tested it on my computer only, which is a Windows 8 machine using Inkscape 0.48.

It will leave the last layer constellation active within the active inkscape instance.

TODOs
=====
* Do not change layer configuration in the active file after export.
* Append the current configuration to the config file (as a setup help for the user)
* Activate a constellation using the config file
