# WeeWX_to_Domoticz
Get weather data from WeeWX to present in Domoticz.

Sending weather data from WeeWX to Domoticz via Weather Underground stopped to work for me 2019-03-05. 
The reason was that Weather Underground now charges for data! 
(But I still send weather station data to Weather Underground for free.)

First a new skin was created on the machine running WeeWX.
Customization of WeeWX is described in: http://www.weewx.com/docs/customizing.htm

Create template "/etc/weewx/skins/Standard/current.json.tmpl"
Include this json template in "/etc/weewx/skins/Standard/skin.conf" after the RSS template:

        [[[json]]]
            template = current.json.tmpl


The DzVents event script "weewx" is created on the machine running Domoticz.
This script gets weather data from WeeWX by fetching the file "weewx/current.json" from the machine running WeeWX.
The usage of DzVents is described in: https://www.domoticz.com/wiki/DzVents:_next_generation_LUA_scripting

Virtual sensors must also be created in Domotics
*  Setup > Hardware, Add: "Dummy (Does nothing, use for virtual switches only)", 
*    name the virtual hardware is here "WeeWX". Created once for WeeWX weather station.
*  Setup > Hardware > for created virtual hardware > Create Virtual Sensors, 
*    three sensors should be created, this dzVents script assumes that are named:
*    name: "Väderstation", Sensor Type: "Temp+Hum+Baro"
*    name: "Vind", Sensor Type: "Wind"
*    name: "Regn", Sensor Type: "Rain"
