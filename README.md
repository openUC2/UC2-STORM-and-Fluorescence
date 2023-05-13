
<p align="left">
<a href="#logo" name="logo"><img src="https://raw.githubusercontent.com/bionanoimaging/UC2-GIT/master/IMAGES/UC2_logo_text.png" width="400"></a>
</p>

# U.C.*STORM*
---

This repository will help you to build *a widefield fluorescence microscope and show you how to upgrade it to perform advanced microscopy methods, such as (d)STORM*.


## How does it look like?

### Top View

<p align="center">
<a href="#logo" name="logo"><img width=400 src="./IMAGES/Application_Fluorescence_Microscope_Infinity_Inverted_STORM_v3_1.png"></a>
</p>

### Side View

<p align="center">
<a href="#logo" name="logo"><img width=400 src="./IMAGES/Application_Fluorescence_Microscope_Infinity_Inverted_STORM_v3.png"></a>
</p>


***Features:***
* Single-channel fluorescence imaging
* XYZ motorized automated microscopy
* LED Matrix for quantitative imaging
* Fully integrated into ImSwitch


# Software

For the control and acquisition software, we use ImSwitch. This is an open-source software centered around Napari as a multi-layer viewer and a rich framework for QT-based widgets. We make use of the open-source localization framework "microEye" ()


## Installation

For the installation we advise you to have a look at the ImSwitch repository here https://github.com/kasasxav/ImSwitch/

After setting up ImSwitch, you can enable STORM reconstruction in real time using the MicroEye Plugin by adding the following configuration to the ImSwitch config file that is located in `~/Documents/ImSwitchConfig/config/imcontrol_options.json`

```json
{
    "setupFileName": "example_uc2_storm_alliedvision.json",
    "recording": {
        "outputFolder": "./ImSwitch/ImSwitch/recordings",
        "includeDateInOutputFolder": true
    },
    "watcher": {
        "outputFolder": "/Users/bene/ImSwitchConfig/scripts"
    }
}
```

The setup file with the actual hardware configuration can be placed here:

`~/Documents/ImSwitchConfig/imcontrol_setups/example_uc2_storm_alliedvision.json`

```json
{
  "positioners": {
    "ESP32Stage": {
      "managerName": "ESP32StageManager",
      "managerProperties": {
        "rs232device": "ESP32"
      },
      "axes": [
        "X",
        "Y",
        "Z"
      ],
      "forScanning": true,
      "forPositioning": true
    }
  },
  "rs232devices": {
    "ESP32": {
      "managerName": "ESP32Manager",
      "managerProperties": {
        "host_": "192.168.43.129",
        "serialport_windows": "COM5",
        "serialport": "/dev/cu./dev/cu.SLAB_USBtoUART"
      }
    }
  },
  "lasers": {
    "488 Laser": {
      "analogChannel": null,
      "digitalLine": null,
      "managerName": "ESP32LEDLaserManager",
      "managerProperties": {
        "rs232device": "ESP32",
        "channel_index": 1,
        "filter_change": false,
        "laser_despeckle_period": 10,
        "laser_despeckle_amplitude": 0
      },
      "wavelength": 488,
      "valueRangeMin": 0,
      "valueRangeMax": 1024
    },
    "635 Laser": {
      "analogChannel": null,
      "digitalLine": null,
      "managerName": "ESP32LEDLaserManager",
      "managerProperties": {
        "rs232device": "ESP32",
        "channel_index": 2,
        "filter_change": false,
        "laser_despeckle_period": 10,
        "laser_despeckle_amplitude": 0
      },
      "wavelength": 635,
      "valueRangeMin": 0,
      "valueRangeMax": 1024
    },
    "LED": {
      "analogChannel": null,
      "digitalLine": null,
      "managerName": "ESP32LEDLaserManager",
      "managerProperties": {
        "rs232device": "ESP32",
        "channel_index": "LED",
        "filter_change": false,
        "filter_axis": 3,
        "filter_position": 32000,
        "filter_position_init": -0
      },
      "wavelength": 635,
      "valueRangeMin": 0,
      "valueRangeMax": 255
    }
  },
  "detectors": {
    "WidefieldCamera": {
        "analogChannel": null,
        "digitalLine": null,
        "managerName": "AVManager",
        "managerProperties": {
            "cameraListIndex": 1,
            "mocktype": "STORM",  
            "mockstackpath": "/Users/bene/Downloads/New_SMLM_datasets/ROI_cos7MT_AF647fluopaint.tif",            
            "avcam": {
                "exposure": 0,
                "gain": 0,
                "blacklevel": 100,
                "image_width": 1000,
                "image_height": 1000,
                "pixel_format": "Mono12"
            }
        },
        "forAcquisition": true,
        "forFocusLock": false
    }
},
"rois": {
    "Full chip": {
      "x": 600,
      "y": 600,
      "w": 1200,
      "h": 1200
    }
  },
  "LEDMatrixs": {
    "ESP32 LEDMatrix": {
      "analogChannel": null,
      "digitalLine": null,
      "managerName": "ESP32LEDMatrixManager",
      "managerProperties": {
        "rs232device": "ESP32",
        "Nx": 4,
        "Ny": 4
      },
      "wavelength": 488,
      "valueRangeMin": 0,
      "valueRangeMax": 32768
    }
  },
  "autofocus": {
    "camera": "WidefieldCamera",
    "positioner": "ESP32Stage",
    "updateFreq": 10,
    "frameCropx": 780,
    "frameCropy": 400,
    "frameCropw": 500,
    "frameCroph": 100
  },
  "availableWidgets": [
    "Settings",
    "View",
    "Recording",
    "Image",
    "Laser",
    "Positioner",
    "Autofocus",
    "STORMRecon"
  ]
}
```

## ImSwitch in Action

Here you can find a tour on Youtube how to set up everything and what it can do.

<p align="center">
<a href="https://www.youtube.com/watch?v=r8f-wmeq5i0" name="logo"><img src="https://i3.ytimg.com/vi/r8f-wmeq5i0/maxresdefault.jpg"></a>
</p>


## Bill of material

Below you will find all components necessary to build this device

### 3D printing files

All these files need to be printed. We used a Prusa i3 MK3 using PLA Prusament (Galaxy Black) at layer height x.x mm and infill xx%.

An in-depth tutorial on how to build the XY-stage can be found here https://github.com/openUC2/

An in-depth tutorial on how to build the Z-stage can be found here https://github.com/openUC2/


| Printed  | UC2             | Linear Stage mount                                                                                                             | 00_Linear_Stage_NEMA11_Mount.ipt                               | 1  | $5.00   | 5   |
|----------|-----------------|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|----|---------|-----|
| Printed  | UC2             | Linear Stage spacer                                                                                                            | 00_Linear_Stage_NEMA11_Mount_Lid.ipt                           | 1  | $1.00   | 1   |
| IM       | openUC2         | UC2 Puzzle piece                                                                                                               | 10_Base_puzzle_v3.ipt                                          | 26 | $5.00   | 130 |
| Printed  | UC2             | UC2 objective Mount linear stage                                                                                               | 20_Cube_Insert_Cube_Z-Stage_NEMA11_china_objectivemount_v3.ipt | 1  | $1.00   | 1   |
| IM       | openUC2         | openUC2 IM Cube                                                                                                                | 10_Cube_1x1_IM.ipt                                             | 42 | $5.00   | 210 |
| External |                 | 5 mm Neodym Magnets                                                                                                            | 00_BallMagnets_5mm_single.ipt                                  | 9  |         | 0   |
| Printed  | UC2             | UC2 Insert for Kinematic Mirror Part1                                                                                          | 20_Cube_Insert_Kinematic_Mirrormount_45_base_part1.ipt         | 3  | $5.00   | 15  |
| Printed  | UC2             | UC2 Insert for Kinematic Mirror Part2                                                                                          | 20_Cube_Insert_Kinematic_Mirrormount_45_base_part2.ipt         | 3  | $1.00   | 3   |
| Printed  | UC2             | Adapter for Nut                                                                                                                | 30_Adapter_M3_nut.ipt                                          | 9  | $1.00   | 9   |
| External | Würth           | DIN 912 - M3 x 0.5 x 12 x 10.75.ipt                                                                                            | DIN 912 - M3 x 0.5 x 12 x 10.75.ipt                            | 15 | $1.00   | 15  |
| Printed  | UC2             | UC2 Insert for 1 inch Mirror, 45°                                                                                              | 20_Cube_Insert_Kinematic_Mirrormount_45_Thorlabsadapter.ipt    | 3  | $5.00   | 15  |
| External | Thorlabs        | Thorlabs PF 10-03-P01                                                                                                          | 00_Thorlabs_PF10-03-P01-Step.ipt                               | 3  | $25.00  | 75  |
| External |                 | Allied Vision Alvium USB 3.1 Kamera 1800 U-158m, 1/2,9", 1,58 MP, C-Mount, monochrom                                           | *Varies*                                                       | 2  | $445.00 | 890 |
| External |                 | C:\cad\PSP2011Client\Work\139705407318IP01941702.stp                                                                           | 00_Basler_ace_USB3_C-Mount.ipt                                 | 1  |         | 0   |
|          | UC2             |                                                                                                                                | 20_Cube_Insert_Cmount_v3.ipt                                   | 1  | $5.00   | 5   |
| External | Thorlabs        | Thorlabs CP33                                                                                                                  | 00_Thorlabs_Cage_CP33_M.ipt                                    | 2  | $20.00  | 40  |
| Printed  | UC2             | UC2 Insert for Thorlabs Cage                                                                                                   | 20_Cube_Insert_Thorlabs_Pins.ipt                               | 2  | $5.00   | 10  |
| Printed  | UC2             | UC2 Insert for Thorlabs 1inch lens                                                                                             | 20_Cube_Insert_Thorlabs_SM1Tube.ipt                            | 2  | $5.00   | 10  |
|          | Thorlabs        | Thorlabs AC254-050-A-ML                                                                                                        | 00_THORLABS_AC254-050-A-ML-Step.ipt                            | 2  | $100.00 | 200 |
| Printed  | UC2             | Filtermount                                                                                                                    | 30_Cube_Insert_Filter_Revolver_Filter_base_single_v3.ipt       | 1  | $5.00   | 5   |
| External | Euromex         | Euromex Mechanischer 180 x 155 mm Objekttisch mit integriertem 75 x 55 mm X-Y-Kreuztisch und transparenter Glasplatte, NZ.9505 | 00_XYTable_china_75_55mm.ipt                                   | 1  | $200.00 | 200 |
| Printed  |                 | Uc2 Insert for Allied Vision Camera                                                                                            | 30_XYTabel_Aliexpress_basplateadapter.ipt                      | 1  | $7.00   | 7   |
| Printed  |                 | Motormount for XY stge                                                                                                         | 30_XYTable_Aliexpress_motormount.ipt                           | 1  | $7.00   | 7   |
| Printed  |                 | Sample Inset for XY Stage                                                                                                      | 30_XYTable_Aliexpress_sampleinsert_round.ipt                   | 1  | $7.00   | 7   |
| External | Roboter Bausatz | GT2 Riemenscheibe 16 Zähne 4mm Bohrung für 6mm Zahnriemen                                                                      | 00_XYTable_pulley.ipt                                          | 2  | $2.00   | 4   |
| Printed  | UC2             | Timing Gear Small                                                                                                              | 00_XYTable_medium_gear.ipt                                     | 1  | $2.00   | 2   |
|          | UC2             | Timing Gear Large                                                                                                              | 00_XYTable_large_gear.ipt                                      | 1  | $2.00   | 2   |
| Printed  | UC2             | Printed Timing Belt Long                                                                                                       | 00_GT2_TimingBelt_flexible_Modular_xytable_large_89tooth.ipt   | 1  | $5.00   | 5   |
| Printed  | UC2             | Printed Timing Belt Short                                                                                                      | 00_GT2_TimingBelt_flexible_Modular_xytable_large_65tooth.ipt   | 1  | $5.00   | 5   |
| External | Laserlands.net  | 638nm Red Laser Module 500mW Round Dot Focusable TTL 3050                                                                      | 00_LASER_640nm.ipt                                             | 1  | $40.00  | 40  |
| Printed  | UC2             | holder for LED Array                                                                                                           | 40_Cube_XY_Table_Illumination_Arm.ipt                          | 1  | $5.00   | 5   |
| External | Adafruit        | Adafruit 64 LED array (8x8)                                                                                                    | 00_LED-ARRAY.ipt                                               | 1  | $20.00  | 20  |
| External | Chroma          | Chroma ET655                                                                                                                   | 00_Chroma_ET655lp long-pass.ipt                                | 1  | $250.00 | 250 |
| External | Chroma          | Chroma ZET 636                                                                                                                 | 00_Chroma ZET635_Excitationfilter.ipt                          | 1  | $250.00 | 250 |
| External | Chroma          | Chroma ZT640                                                                                                                   | 00_Chroma_ZT640rdc.ipt                                         | 1  | $250.00 | 250 |
| External | -               | Linear Stage 50mm , Nema 12, MGN9h                                                                                             |                                                                | 1  | 50      | 50  |

### Design files

The original design files are in the [INVENTOR](./INVENTOR) folder.

### Electronics

Here we make use of the ESP32 Wemos D1 R32 microcontroller board in combination with the CNC Shield v3. The wiring of the different components is straight forward as the Stepper Motors are attached to the stepper drivers and the Laser is triggered by the `SpinEn` pin. The NeoPixel LED mounts to the  `Hold` pin.

<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/UC2_STORM.png"></a>
</p>

#### Flashing the firmware

Go to the website https://youseetoo.github.io/ and choose the CNC board as the hardware configuration to flash the latest version of the Firmware. The PS3 controller's MAC address has to be setup with the PS Pairing tool. The actual MAC Address is printed out on the Serial monitor while the Board is booting up.


## Showcase

Here you can see the device in action:

<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/microscope_1.jpeg"></a>
</p>gith


<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/microscope_2.jpeg"></a>
</p>

<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/microscope_3.jpeg"></a>
</p>

<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/microscope_4.jpeg"></a>
</p>

<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/microscope_5.jpeg"></a>
</p>

<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/microscope_6.jpeg"></a>
</p>


## Get Involved

This project is open so that anyone can get involved. You don't even have to learn CAD designing or programming. Find ways you can contribute in  [CONTRIBUTING](https://github.com/openUC2/UC2-GIT/blob/master/CONTRIBUTING.md)


## License and Collaboration

This project is open-source and is released under the CERN open hardware license. Our aim is to make the kits commercially available.
We encourage everyone who is using our Toolbox to share their results and ideas, so that the Toolbox keeps improving. It should serve as a easy-to-use and easy-to-access general purpose building block solution for the area of STEAM education. All the design files are generally for free, but we would like to hear from you how is it going.

You're free to fork the project and enhance it. If you have any suggestions to improve it or add any additional functions make a pull-request or file an issue.

Please find the type of licenses [here](https://github.com/openUC2/UC2-GIT/blob/master/License.md)

REMARK: All files have been designed using Autodesk Inventor 2019 (EDUCATION)


## Collaborating
If you find this project useful, please like this repository, follow us on Twitter and cite the webpage! :-)
