# Home Assistant Simple Lock Manager
This is a simple simple Zwave Lock Manager for Home Assistant.

When I first migrated from Smartthings to Home Assistant, one of the very first things I needed to do was to figure out how to manage the lock codes on my Zwave (kwikset) locks and have them auto lock.

I discovered the KeyMaster integration and went with it.  However, it was more complex than I needed and most of all it made my install messy with the hundreds of helpers it created that HA would report as broken and were unfixable. 

There had to be a simpler way, and this is what I developed using a handful of helpers and a few automations with very little customization needed.  The key difference is that it doesn't support scheduling (although you could easily write a distinct automation to enable disable the appropriate booleans at certain times) and most importantly it doesn't make a distinction between various locks you might have.  Basically, if you can get in the house via one lock, you can get in the house via all the locks.  

The automations support up to 8 distinct codes that can be selectively enabled/disabled and be set to provide a notification if the lock code is used.

I've also included an example auto-lock automation which uses various custom sensors.

I suspect that all of this could be converted to blueprints, but I don't have time for that right now.  Volunteers welcome! :-)

![image](https://user-images.githubusercontent.com/25288127/208971061-797fa4b9-3915-4080-887a-2de3f22d9b04.png)

# Instructions
1) Add the sensors from the configuration.yaml file in this repo to your configuration.yaml file (hint use File Editor add-in if possible)
2) Reload the input_boolean and input_text helpers via Developer Tools/YAML
3) Create new automations for each of the 'set codes' and 'notify' yaml files (create new automation and edit in YAML, and then paste the code).  Note there are some modifications you will need to make to use your door lock entities and notification service, but that's it
4) Create the front end YAML by creating a new dashboard in Settings/Dashboards, and editing the page in YAML via raw configuration editor (it is multiple cards) and pasting the code from the lovelace yaml file.
5) For auto-lock, you can use the auto-lock yaml, but note that it has some custom logic around sensors that prevent the door from auto-locking if it detects activity outside.  You can either replace this with your own sensors or remove these conditions.

## Important Notes
1) The code is set up to support 8 distinct lock codes.  The current code could support 9.  However, it can't support more than that due to the janky ninja template code which assumes that the code slots are only single digits.  If you want more than 9 slots, you will need to fix the template code with something more durable and clever than I am.  By all means feel free to share your code or do Pull Request if you do come up with something better!
