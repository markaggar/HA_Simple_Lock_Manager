# Home Assistant Simple Lock and Door Manager

This is a simple Zwave Lock and Door Manager for Home Assistant.

When I first migrated from Smartthings to Home Assistant, one of the very first things I needed to do was to figure out how to manage the lock codes on my Zwave (Kwikset) locks and have them auto lock after a period of time based on various door/motion sensors.

I discovered the KeyMaster integration and went with it. However, it was more complex than I needed and most of all it made my install messy with the hundreds of helpers it created that HA would report as restored entities every time I restarted HA. I wanted something simpler.

There had to be a simpler way, and this is what I developed using a handful of helpers and a few automations with very little customization needed. The key difference is that it doesn't support scheduling. There's one big automation that handles all 8 codes. Everything is simpler. The user experience is essentially the same as KeyMaster but far simpler to set up and maintain.

The automations support up to 9 distinct codes that can be selectively enabled/disabled and be set to provide a notification if the lock code is used.

I've also included example automations for auto-lock functionality and door open notifications.

![image](https://user-images.githubusercontent.com/25288127/208971061-797fa4b9-3915-4080-887a-2de3f22d9b04.png)

## Installation

1. **Download the package file**: Download `Simple_Lock_Manager_Package.yaml` from this repository
2. **Create packages directory**: If you don't already have one, create a `packages` directory in your Home Assistant configuration directory
3. **Copy the package**: Place `Simple_Lock_Manager_Package.yaml` in your `packages` directory
4. **Enable packages in configuration.yaml**: Add the following to your `configuration.yaml` if not already present:
   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```
5. **Customize lock entities**: Edit the `Simple_Lock_Manager_Package.yaml` file and replace the example lock entities with your actual lock entity IDs:
   - `lock.lock_deck_north_door`
   - `lock.lock_front_door` 
   - `lock.garage_side_door_lock`
6. **Customize notification service**: In the lock notification automation, update the notification service and targets as needed
7. **Reload YAML**: Go to Developer Tools/YAML and Reload all YAML to create the entities/automations
8. **Create dashboard**: Create a new dashboard using the Lovelace configuration from `lockcodes_lovelace.yaml`

### Additional Optional Automations

The repository also includes example automations that you can customize for your setup:

- **Auto-lock**: `auto_lock_example.yaml` - Automatically locks doors based on door sensors and motion detection
- **Door open notifications**: `doors_open_notify_automation.yaml` - Alerts when doors are left open too long

## Configuration Requirements

### Required Customizations

1. **Lock Entities**: Update all lock entity references to match your actual lock entities
2. **Notification Services**: Configure notification services in the lock notify automation
3. **Sensor Entities**: For optional automations, update sensor entity references to match your setup

### Entity Structure

The package creates the following entities for each of the 9 lock code slots:

- `input_text.lock_code_slot_X_pin` - The PIN code (5-10 digits)
- `input_text.lock_code_slot_X_name` - Name/description for the code
- `input_boolean.lock_code_slot_X_state` - Enable/disable the code
- `input_boolean.lock_code_slot_X_notify` - Enable/disable notifications for this code

## Dashboard Configuration

Create a new dashboard and use the raw configuration editor to add the cards from `lockcodes_lovelace.yaml`. You'll need to update the user visibility settings to match your Home Assistant users.

## Important Notes

1. The code supports up to 9 distinct lock codes
2. The system uses Z-Wave JS for lock code management  
3. PIN codes must be 5-10 digits and numeric only
4. The notification system can be customized to use any Home Assistant notification service
5. For production use, customize all entity references, sensor names, and notification services (i.e. any hardcoded entity and notification service names to match your setup).

## Troubleshooting

- Ensure your locks are properly integrated with Z-Wave JS
- Verify entity IDs match your actual lock entities
- Check that the packages directory is properly configured in configuration.yaml
- Use Developer Tools to test automation triggers and actions

## Contributing

Feel free to submit issues, feature requests, or pull requests.
