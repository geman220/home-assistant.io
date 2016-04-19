---
layout: page
title: "Hibernate your Windows PC"
description: "Hibernate / Wake up your Windows PC with a Switch"
date: 2016-04-19 15:30
sidebar: true
comments: false
sharing: true
footer: true
ha_category: Automation Examples
---

Hibernate a remote Windows PC from HASS or automate!

Add a the PC you want to hibernate

```yaml
- platform: wake_on_lan
  mac_address: "00:00:00:00:00:00"
  name: "Main PC"
  host: "192.168.x.x"
```

This requires psexec.exe to be in your system environment path

```yaml
- platform: command_switch
  switches:
    Main_PC_Power:
      offcmd: psexec -s -i \\PCNAME shutdown.exe /h
      initial: 'on'
```

Using the template switch the toggle will show if the PC is hibernating or not

```yaml
- platform: template
  switches:
    copy:
      value_template: '{{ states.switch.main_pc.state }}'
      turn_on:
        service: switch.turn_on
        entity_id: switch.main_pc
      turn_off:
        service: switch.turn_off
        entity_id: switch.main_pc_power
```
