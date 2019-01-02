![Logo](admin/nuki.png)
# ioBroker.nuki
=================

This ioBroker adapter allows to control and monitor the [Nuki Smart Lock](https://nuki.io/de/) by using the [API of the Nuki Bridge](https://developer.nuki.io/page/nuki-bridge-http-api-170/4/#heading--introduction).

[![NPM version](http://img.shields.io/npm/v/iobroker.nuki.svg)](https://www.npmjs.com/package/iobroker.nuki)
[![Travis CI](https://travis-ci.org/smaragdschlange/ioBroker.nuki.svg?branch=master)](https://travis-ci.org/smaragdschlange/ioBroker.nuki)
[![Downloads](https://img.shields.io/npm/dm/iobroker.nuki.svg)](https://www.npmjs.com/package/iobroker.nuki)

[![NPM](https://nodei.co/npm/iobroker.nuki.png?downloads=true)](https://nodei.co/npm/iobroker.nuki/)


## Requirements
* A Nuki Smart Lock (obviously) and a Nuki (hardware or software) Bridge.
* A running instance of ioBroker.


## Usage
Each instance of the Nuki adapter represents a Nuki bridge. When creating an instance, simply enter IP address, port and token of your Nuki bridge. The name is optional and will be generated automatically if left empty. The checkbox "use callback" and the value "callback port in ioBroker" are optional and can be set in order to make use of the callback function of the Nuki. After saving an instance there will be created a bridge device with a channel for each Nuki lock that is connected to the specified Nuki bridge. The channels provide the current state of the Nuki lock as output parameters:

* batteryCritical: Indicator for low battery
* lockState: Indicator whether Nuki is locked
* state: Current (numeric) lock state (Nuki native)
* timestamp: Last updated

Additionally, the channels provide input parameters which enable basic control of the Nuki lock:

* action: Numeric action code for setting the Nuki state (Nuki native)

Valid input values are:

    0 (no action)
    1 (unlock)
    2 (lock)
    3 (unlatch)
    4 (lock ‘n’ go)
    5 (lock ‘n’ go with unlatch)

* lockAction: Switch for locking / unlocking the Nuki (true = unlock; false = lock)
* openAction: Button for unlatching the Nuki
* openLocknGoAction: Button for unlatching and after some seconds locking the Nuki
* unlockLocknGoAction: Button for unlocking and after some seconds locking the Nuki


## Additional information
How to get your bridges token:

* Call http://< bridge_ip >:< bridge_port >/auth from any browser in your LAN -> bridge turns on its LED
* Press the button of the bridge within 30 seconds
* Result of the browser call should be something like this:
    {
    "token": “token123”,
    "success": true
    }
Callback function:

If the callback function is being used, the adapter will try to automatically set the callback on the Nuki bridge when the instance is being saved. When the instance is unloaded the callback will be deleted again. All Nuki states will be kept up-to-date by the Nuki bridge while callback is activated.
Callbacks can be set and removed from any browser with following urls:

Set:
* http://< bridge_ip >:< bridge_port >/callback/add?url=http%3A%2F%2F< host_ip >%3A< host_port >%2Fapi%2Fnuki&token=< bridgeToken >

Remove:
* http://< bridge_ip >:< bridge_port >/callback/remove?id=< callback_id >&token=< bridgeToken >

## Update
When updating from 0.1.x to 0.2.0 or higher it is recommended to delete all instances of the old version before installing the new version. Please be aware that version changes bigger than on patch level (-> change of only the last digit) could always contain changes to data points e.g. 0.1.3 to 0.2.0

## Changelog

### 1.0.3
* (smaragdschlange) bug fix: action buttons were not working properly

### 1.0.1
* (smaragdschlange) version synch

### 1.0.0
* (smaragdschlange) initial release on npm

### 0.2.0
* (smaragdschlange) periodic state updates added
* (smaragdschlange) restructure objects

### 0.1.3
* (smaragdschlange) timestamp bug fixed

### 0.1.2
* (smaragdschlange) minor bugfixes
* (smaragdschlange) added delay before each Nuki request to avoid null responses

### 0.1.1
* (smaragdschlange) callback will be removed when instance is unloading

### 0.1.0
* (smaragdschlange) callback finally working
* (smaragdschlange) added another State

### 0.0.6
* (smaragdschlange) additional states/actions and improved compatibility (callback still not completely working)

### 0.0.5
* (smaragdschlange) added support for nuki bridge callback (web server still to be added)

### 0.0.4
* (smaragdschlange) added input parameter for lock actions

### 0.0.3
* (smaragdschlange) bug fixes and restructure

### 0.0.2
* (smaragdschlange) added input parameters

### 0.0.1
* (smaragdschlange) initial release

## License
The MIT License (MIT)

Copyright (c) 2018 smaragdschlange <smaragdschlange@gmx.de>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
