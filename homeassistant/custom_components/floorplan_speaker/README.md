FLOORPLAN SPEAKER AKA LOVELACD PLAYER
###########################################

URL https://github.com/thomasloven/lovelace-player

lovelace-player

Use any browser currently viewing your lovelace interface as an audio receiver with a media_player interface.

Example use case: An iPad mounted to your wall as a home automation dashboard can now receive text-to-speech announcements from home-assistant.
Breaking changes!

Lovelace-player configuration has recently changed entirely. See below for setup instructions.
Installation instructions

This plugin requires card-tools to be installed.

For installation instructions see this guide.

The recommended type of this plugin is: js.

After installing the plugin, you also need to install the floorplan_speaker media player component.

Download floorplan_speaker.py from pkozul/ha-floorplan-kiosk and save to <ha config>/custom_components/floorplan_speaker/media_player.py.

Also create an empty file at <ha config>/custom_components/floorplan_speaker/__init__.py. (That's two underscores on each side of init)
Usage instructions

First, you need to add a media player to your home assistant configuration, which your lovelace interface will connect to.

Add the following to your configuration.yaml

media_player:
  - platform: floorplan_speaker
    name: my_floorplan_speaker

The connection is then setup in the resources section (where you imported lovelace-player.js to your lovelace configuration, by adding one or more variables on the form <entity-id>=<device-id> to the script URL:

resources:
  - url: /local/card-tools.js
    type: js
  - url: /local/lovelace-player.js?<entity-id>=<device-id>
    type: js

<entity-id> is the entity id of your media_player, e.g. media_player.my_floorplan_speaker.

<device-id> is the device ID for your device-browser combination (see below).

To add more players, you add more <entity-id>=<device-id> combinations to the url, separated by an ampersand &.
About device IDs

The Device ID is a random number that is generated the first time you view the lovelace UI in a new browser after installing card-tools. It is stored in your browsers localStorage and can not be accessed or used to identify your browser by any other website (this is not true for Fully Kiosk browser for Android).

To get your Deice ID, the easiest method is to look in your browser console (press F12 in google Chrome, most browsers have something similar). There you should be able to see a message saying "CARD-TOOLS IS INSTALLED" followed by your Device ID.

id-cardtools

If you don't have access to the console (e.g. on a mobile browser), you can add the variable getID=true to the script URL. You should then get a popup displaying your Device ID the next time you reload your lovelace interface.