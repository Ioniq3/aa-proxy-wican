# aa-proxy-wican

aa-proxy-wican is a aa-proxy-rs client for the WiCAN Pro device found here: https://www.crowdsupply.com/meatpi-electronics/wican-pro  This device supports vehicle profiles and returns pre-parsed vehicle metrics such as SOC (State of Charge).  Setting up the WiCAN Pro and getting your vehicle profile working is beyond the scope of this document, please see the WiCAN documentation here: https://meatpihq.github.io/wican-fw/

# Requirements:
* WiCAN Pro (Original WiCAN is not currently supported
* WiCAN Pro firmware 4.30b4 and above
* A working WiCAN Pro vehicle profile with at least SOC (confirm on the Dashboard that your SOC is being parsed correctly, if not seek support from WiCAN)
* aa-proxy-rs with working MITM mode

# Setup instructions:

 - Identify the MAC Address of your WiCAN PRO
 - Open your aa-proxy-rs configuration, either via the web interface or by editing the config.toml
 - Add the MAC address of your phone to the 'connect' setting.  This will ensure aa-proxy-rs does not try to connect to the WiCAN Pro (note this is temporary and will be resolved with an aa-proxy-rs update)
 - Enable EV Mode
 - Configure your EV Connector types if not already done
 - Configure EV Logger, at a minimum the following is required: ```/usr/bin/aa-proxy-wican --wican-mac-address AA:BB:CC:DD:EE:FF --vehicle-battery-capacity 10000``` where 10000 is the capacity of your EV battery in watt hours.

Logs are by default written to /var/log/aa-proxy-wican.log

aa-proxy-wican supports additional arguments you may wish to modify.  It can also be run over ssh should you wish to test/debug.

# Full usage:
```
Usage: aa-proxy-wican [OPTIONS] --vehicle-battery-capacity <VEHICLE_BATTERY_CAPACITY> --wican-mac-address <WICAN_MAC_ADDRESS>

Options:
  -v, --vehicle-battery-capacity <VEHICLE_BATTERY_CAPACITY>
          Vehicle Battery Capacity in wh
  -w, --wican-mac-address <WICAN_MAC_ADDRESS>
          WiCAN MAC address
      --wican-passkey <WICAN_PASSKEY>
          WiCAN passkey [default: 123456]
      --wican-max-connect-retries <WICAN_MAX_CONNECT_RETRIES>
          WiCAN retries [default: 5]
      --wican-timeout <WICAN_TIMEOUT>
          WiCAN timeout [default: 10]
      --wican-update-frequency-minutes <WICAN_UPDATE_FREQUENCY_MINUTES>
          WiCAN update frequency in minutes [default: 1]
      --api-url <API_URL>
          aa-proxy-rs url [default: http://localhost/battery]
      --log-file <LOG_FILE>
          Log file [default: /var/log/aa-proxy-wican.log]
      --log-level <LOG_LEVEL>
          Log level [default: info] [possible values: off, error, warn, info, debug, trace]
  -h, --help
          Print help
  -V, --version
          Print version
```