# HA_Simple_Lock_Manager
This is a simple simple Zwave Lock Manager for Home Assistant.

When I first migrated from Smartthings to Home Assistant, one of the very first things I needed to do was to figure out how to manage the lock codes on my Zwave (kwikset) locks and have them auto lock.

I discovered the KeyMaster integration and went with it.  However, it was more complex than I needed and most of all it made my install messy with the hundreds of helpers it created that HA would report as broken and were unfixable. 

There had to be a simpler way, and this is what I developed using a handful of helpers and a few automations.

The automations support up to 8 distinct codes that can be selectively enabled/disabled and be set to provide a notification if the lock code is used.

![image](https://user-images.githubusercontent.com/25288127/208971061-797fa4b9-3915-4080-887a-2de3f22d9b04.png)

# Instructions
1) Add the sensors in the configuration.yaml file in this repo to your configuration.yaml file (hint use File Editor add-in if possible)
2) Reload the input_boolean and input_text helpers via Developer Tools/YAML
3) Create new automations for each of the set codes and notify yaml files (create new automation and edit in YAML, and then paste the code)
4) Create the front end YAML by creating a new dashboard in Settings/Dashboards, and editing the page in YAML (it is multiple cards)
