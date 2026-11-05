# Appliance Compliance

Home Assistant automation blueprints, written for and running on a real
house.

## Blueprints

### Daylight-Aware Presence Light

[![Open your Home Assistant instance and show the blueprint import dialog with this blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FIsoceth%2FAppliance-Compliance%2Fblob%2Fmain%2Fblueprints%2Fautomation%2Fpresence%2Fpresence_daylight_light.yaml)

`blueprints/automation/presence/presence_daylight_light.yaml`

Keeps a light on while a presence sensor reports someone there and the
daylight is too poor. The sensor can be a motion sensor, with a hold time
after the last movement, or a computer reporting that it is in use.

- **Daylight** comes from an illuminance sensor in the room when you have
  one. The sensor sees the light it controls, so its reading only decides
  when to switch on. Otherwise daylight is estimated from the sun's
  elevation and the weather entity's cloud cover, rain, snow and fog, and
  two thresholds in outdoor lux switch the light on and off.
- **Colour and brightness** follow the clock, not the sunset. On a winter
  afternoon the light comes on at its day settings, and evening warmth
  waits for the evening.
- **Manual changes** made through Home Assistant or a voice assistant are
  left alone until presence ends. Once presence ends and the hold time has
  passed, the light always switches off.

### Circadian Lighting Room Controller

[![Open your Home Assistant instance and show the blueprint import dialog with this blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FIsoceth%2FAppliance-Compliance%2Fblob%2Fmain%2Fblueprints%2Fautomation%2Fcircadian%2Fcircadian_room.yaml)

`blueprints/automation/circadian/circadian_room.yaml`

Adjusts a room's lights through the day while they are on: a cool morning
boost, day settings, and a warm, dimming evening that begins at sunset or a
fallback time, whichever is later. Optional helpers can pause it, on request
or automatically after a manual adjustment.

## Installing

Use the import button above. You can also paste the file's GitHub URL into
**Settings → Automations & Scenes → Blueprints → Import Blueprint**. Then
create an automation from the blueprint and fill in its inputs.
