# tedee_lock
Homeassistant Custom Component

This component gives access to a Tedee doorlock. It needs also the Tedee Bridge present and connected to the doorlock.
In my other repository you will find the Python module, that also needs to be installed.

[pytedee](https://github.com/joerg65/pytedee)

To install this component, the files in this repository must be copied to `<config/custom_components/tedee_lock>`.

Put this lines int the configuration:
```yaml
lock:
  - platform: tedee
    username: tedee-username
    password: tedee-password
```

After restart of Homeassistant you should see the lock:

![Image of Tede Lock Entity](https://github.com/joerg65/tedee_lock/images/Lock_Entity.png)

Here is how I made a horizontal-stack with two custom button-cards:

```yaml
type: horizontal-stack
title: Haustür
cards:
  - entity: lock.lock_326b
    type: 'custom:button-card'
    state:
      - value: locked
        color: gray
        icon: 'mdi:lock'
        name: verriegelt
      - value: unlocked
        color: orange
        icon: 'mdi:lock'
        name: verriegeln
    tap_action:
      action: call-service
      service: lock.lock
      service_data:
        entity_id: lock.lock_326b
  - entity: lock.lock_326b
    type: 'custom:button-card'
    state:
      - value: unlocked
        color: gray
        icon: 'mdi:lock-open'
        name: entriegelt
      - value: locked
        color: green
        icon: 'mdi:lock-open'
        name: entriegeln
    tap_action:
      action: call-service
      service: lock.unlock
      service_data:
        entity_id: lock.lock_326b
```
![Image of Tede Lock with button-cards](https://github.com/joerg65/tedee_lock/images/Lock_Entity.png)
