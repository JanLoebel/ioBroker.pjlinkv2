![Logo](admin/pjlink.png)
# ioBroker.PJLinkV2

[![NPM version](http://img.shields.io/npm/v/iobroker.template.svg)](https://www.npmjs.com/package/iobroker.template)
[![Downloads](https://img.shields.io/npm/dm/iobroker.template.svg)](https://www.npmjs.com/package/iobroker.template)
![Number of Installations (latest)](http://iobroker.live/badges/template-installed.svg)
![Number of Installations (stable)](http://iobroker.live/badges/template-stable.svg)
[![Dependency Status](https://img.shields.io/david/Author/iobroker.template.svg)](https://david-dm.org/Author/iobroker.template)
[![Known Vulnerabilities](https://snyk.io/test/github/Author/ioBroker.template/badge.svg)](https://snyk.io/test/github/Author/ioBroker.template)

[![NPM](https://nodei.co/npm/iobroker.template.png?downloads=true)](https://nodei.co/npm/iobroker.template/)

**Tests:**: [![Travis-CI](http://img.shields.io/travis/Author/ioBroker.template/master.svg)](https://travis-ci.org/Author/ioBroker.template)

This adapter controls any PJLink compatible projector or display with ioBroker.

PJLink is a unified standard for operating and controlling data projectors and displays. The protocol enables central control of certain devices, manufactured by different vendors. The protocol is used by NEC, Casio, Seiko, Sony, Panasonic, Hitachi, Mitsubishi, Ricoh, Vivitek and even more. Please consult the device manual to check compatibility.

## Current shortcomings
- Error Handling is not implemented right now. If an unknown parameter is entered or if the device is not accessible using TCP/IP, an error will be shown in the ioBroker Log. In one of the future versions, the device errorcodes will be analyzed and translated.
- Lighting hours are given for one (the first) lamp, even if PJLink supports several lamps. If somebody have a proper device, please contact me for testing.
- The device is not pushing information using the PJLink protocol. Therefore, the adapter will pull certain information frequently (see
polling interval). Do not reduce the polling interval <10 sec. because the device needs up to 2 sec. to answer and the script will query several paramters.
- All dialogs are in English as for now, DE and RU are in progress. Further translations on demand.

## ToDo
- Implementing a table to translate input ID to name of the port (like 31 = HDMI1)
- Supporting PJLink Class 2 protocol

## How the adapter works
The adapter consists by three elements:
-	Admin interface to define device specific parameters (admin/index.html)
-	JavaScript module for device communication, based on PJLink protocol (utils/pjlink.js)
-	Main script (main.js)

The Main script works in four steps:
1)	Doing some initial configuration like creating ioBroker objects
2)	Starring the first communication with the device and asking for the current parameters
3)	Waiting for a state change like switching the input source or turning power off
4)	Executing the change with the device
Please be aware, that the communication with the projector is not possible if the projector is in standby with power saving feature enabled. Therefore, it will not be possible to turn the project on using this adapter. To do so, disable the power saving feature using the projector configuration (Menu > Settings...).

## Changelog
### 2.0.0 (2020/09/22)
- new development, based on ioBroker adapter template 

### 0.2.0 (2019/11/15)
- fixed an error where adapter instances started multiple times
- fixed an issue when encrypted communicating ist used
- changed datapoint "power" to be boolean, to start/stop the devices
- added datapoint "status" to report the current status of the device (on, off, warm up, cool down, not connected)

### 0.1.1 (2018/02/11)
- errorhandling implemented (somekind of...)

### 0.1.0 (2017/12/31)
- first public flight (beta)

### 0.0.5 (2017/12/26)
- bugfixing

### 0.0.3 (2017/12/23)
- build admin interface
- build translate table

### 0.0.2 (2017/12/18)
- redesign some timings (what / when)

### 0.0.1
- Inital version

## License
MIT License

Copyright (c) 2020 Author <author@mail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.