---
layout: page
title: "Leviton Decora"
description: "Instructions on how to setup Leviton Decora Bluetooth dimmers within Home Assistant."
date: 2017-01-18 22:45
sidebar: true
comments: false
sharing: true
footer: true
ha_category: Light
ha_iot_class: Local Polling
logo: leviton.png
ha_release: 0.37
redirect_from:
 - /components/light.decora/
---

Support for the Decora Bluetooth dimmer switch [Leviton](https://www.leviton.com/en/products/residential/dimmers/automation-smart-home/decora-digital-with-bluetooth-dimmers#t=Products&sort=%40wcs_site_tree_rank%20ascending&layout=card).

The API key can be obtained by downloading [this git repository](https://github.com/mjg59/python-decora) and running the `read_key.py` script with the Bluetooth address of the switch as the first argument. Hold the switch in the off position until the green status LED starts flashing before running the script. The output is the API key.

To enable these lights, add the following lines to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
light:
  - platform: decora
    devices:
      00:21:4D:00:00:01:
        api_key: YOUR_API_KEY
```

{% configuration %}
devices:
  description: A list of lights to use.
  required: true
  type: map
  keys:
    mac_address:
      required: true
      description: The bluetooth address of the switch.
      type: string
      name:
        description: The name to use in the frontend.
        required: false
        type: string
      api_key:
        description: The API key to access the device.
        required: true
        type: string
{% endconfiguration %}

<p class='note'>
If you get an error looking like this:

```bash
Jun 20 19:41:18 androlapin hass[29588]: ERROR:homeassistant.components.light:Error while setting up platform decora
[...]
Jun 20 19:41:18 androlapin hass[29588]:   File "/usr/lib/python3.6/concurrent/futures/thread.py", line 55, in run
Jun 20 19:41:18 androlapin hass[29588]:     result = self.fn(*self.args, **self.kwargs)
Jun 20 19:41:18 androlapin hass[29588]:   File "/opt/homeassistant/custom_components/light/decora.py", line 68, in setup_platform
Jun 20 19:41:18 androlapin hass[29588]:     light = DecoraLight(device)
[...]
Jun 20 19:41:18 androlapin hass[29588]: OSError: [Errno 8] Exec format error
```

1. Go to your `.homeassistant` folder
2. Then go to `deps/bluepy` subfolder.
3. Then run `make all`
4. Restart Home Assistant
</p>
