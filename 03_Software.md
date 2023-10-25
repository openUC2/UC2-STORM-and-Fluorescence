
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
