# Wilberforce Home Assistant Dashboard


A few people have been asking for the yaml config so here goes, along with some other brief explanations.

**Theme**: [hass-kibibit-theme](https://github.com/Kibibit/hass-kibibit-theme)

**Screenshots:** [Here](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard#screenshots)

/

/


## 1. The ['Devices' desktop card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Devices%20tab)  

**Note:** The mobile 'Devices' card is the same config but with some bits taken out as I don't need that info on mobile view.

![Screenshot 2022-05-10 at 12 08 50](https://user-images.githubusercontent.com/57415184/167615391-84246a91-1961-4329-91c4-713185a6b73e.png)



 **A:** [How I control my Macbook Pro volume/mute](https://github.com/bessarabov/mac2mqtt) 
 
 ![Screenshot 2022-05-10 at 11 52 57](https://user-images.githubusercontent.com/57415184/167612725-e09e2902-6d01-4148-821e-b35e40d48672.png)


 
 **B:** [How I added the Denon AVR 'Dynamic EQ' and subwoofer level controls](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Denon%20AVR)
 
![Screenshot 2022-05-10 at 11 52 04](https://user-images.githubusercontent.com/57415184/167612587-61df8346-e615-4607-9937-bc21f004f486.png)

**Note:** You can control pretty much every single aspect of a Denon Receiver via its IP protocol and the Denon HA integration. 

The list of commands you can publish are [here](https://www.denon.com/-/media/files/documentmaster/denonna/avr-x3700hfy21avr_denon_protocol_v02_04062020.xlsx) on Denon's official website.




/


  **Required custom cards:**
  - [Stack In Card](https://github.com/custom-cards/stack-in-card)   
  - [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom)   
  - [Text Divider Row](https://github.com/iantrich/text-divider-row)   
  - [Lovelace Slider Entity Row](https://github.com/thomasloven/lovelace-slider-entity-row)   
  - [Mini Media Player](https://github.com/kalkih/mini-media-player)   



/

/

/



## 2. The ['All Rooms' (Lights and Scripts buttons) desktop card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Lights%20and%20Scripts%20tab)  

![Screenshot 2022-05-10 at 11 44 15](https://user-images.githubusercontent.com/57415184/167611308-3dce6069-6b20-40d8-a9dc-6572c34ed657.png)




 **Note:** The buttons for 'Switch', 'Xbox', 'Plex' and 'Shield' all simply just call scripts that I've created that turn on my TV, surround sound and switch my TV & Receiver to the appropiate HDMI and turns the corresponding device on if supported. (The Nintendo Switch won't turn on this way as we cannot control it via HA). 
 
 The Script buttons are actually Template Switches, so it allows HA to report the 'on state', for example the Shield switch appears **'on'** when my Nvidia Shield is on AND my TV is currently on the correct HDMI input. 
 
 **Example extract from my config.yaml for this:**


```
switch:
  - platform: template
    switches:
      nvidiashield:
        value_template: "{{ is_state('media_player.nvidia_shield', 'idle') or is_state('media_player.nvidia_shield', 'paused') or is_state('media_player.nvidia_shield', 'playing') and is_state_attr('media_player.living_room_tv_2', 'source', 'Home Theatre')}}"
        turn_on:
          service: script.turn_on
          target:
            entity_id: script.1587548231616
        turn_off:
          service: media_player.turn_off
          target:
            entity_id: media_player.nvidia_shield
        icon_template: >-
          {% if is_state_attr('media_player.denon_avr', 'source', 'SHIELD') %}
            phu:nvidia-shield
          {% else %}
            phu:nvidia-shield
          {% endif %}
  - platform: template
    switches:
      plex_shield:
        value_template: "{{ is_state_attr('media_player.nvidia_shield', 'source', 'Plex') and is_state_attr('media_player.living_room_tv_2', 'source', 'Home Theatre') }}"
        turn_on:
          service: script.turn_on
          target:
            entity_id: script.1579992709710
        turn_off:
          service: script.turn_on
          target:
            entity_id: script.1587548231616
        icon_template: >-
          {% if is_state_attr('media_player.denon_avr', 'source', 'SHIELD') %}
            mdi:plex
          {% else %}
            mdi:plex
          {% endif %}


```




/


**Required custom cards:**
- [Homekit Panel Card](https://github.com/DBuit/Homekit-panel-card)   
- [Mini Graph Card](https://github.com/kalkih/mini-graph-card)   
- [Light Popup Card](https://github.com/DBuit/light-popup-card)   
- [Light Entity Card](https://github.com/ljmerza/light-entity-card)   


/

/

/









## 3. The ['Macbook Pro' card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Macbook%20Pro%20card)

![Screenshot 2022-05-10 at 11 46 24](https://user-images.githubusercontent.com/57415184/167611659-83c473e7-9954-44ee-ac4b-2fe0652df354.png)







**Note:** The battery % simply comes from the Home Assistant MacOS app, you can expose many sensors from this.

**A:** [How I control my Macbook Pro volume/mute](https://github.com/bessarabov/mac2mqtt)

**B:** [How I pull my Macbook Pro stats](https://www.home-assistant.io/integrations/glances/) and then once that is done,  install and configure glances on your Mac! 

Note that this only works when my Macbook is on my local network.





/

**Required custom cards:**
- [Lovelace Slider Entity Row](https://github.com/thomasloven/lovelace-slider-entity-row)
- [Custom Bar-Card](https://github.com/custom-cards/bar-card)

/

/

/








## 4. The [Server Stats/Uptime card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Server%20Stats%20%26%20Uptime%20Card)


![Screenshot 2022-05-10 at 11 48 57](https://user-images.githubusercontent.com/57415184/167612081-42c8f696-fc83-42a7-afab-f164dede083f.png)





**A:** [What I use to pull my local server stats](https://www.home-assistant.io/integrations/systemmonitor/)

**B:** [What I use to pull my remote offsite backup server stats](https://www.home-assistant.io/integrations/glances/) (You must open ports on router at remote site for this to work, **be careful!)**

**C:** [Uptime integration](https://www.home-assistant.io/integrations/uptime/)

**D:** [SMART integration](https://community.home-assistant.io/t/monitor-your-hdd-smart-status/194132)-  **Note**: this is quite awkward to setup!

![Screenshot 2022-05-10 at 11 49 48](https://user-images.githubusercontent.com/57415184/167612206-f1d6b9c4-a6ab-4303-b3fb-92f10a3190db.png)






/


**Required custom cards:**
- [Bar Card](https://github.com/custom-cards/bar-card)
- [Uptime Card](https://github.com/dylandoamaral/uptime-card)

/

/

/





## 5. The [Plex/Tautulli bandwidth card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Plex%20card)

![Screenshot 2022-05-10 at 11 51 13](https://user-images.githubusercontent.com/57415184/167612447-dee87a5a-3f79-4993-8b05-d8f170e1b7ab.png)








/

**Required custom cards:**
- [Mini Graph Card](https://github.com/kalkih/mini-graph-card)


/

/

/










# SCREENSHOTS

## Mobile Dashboard:
![1(1)](https://user-images.githubusercontent.com/57415184/167597138-9232043c-8ef1-4024-aeb9-a6f498553a93.jpg)
![2(1)](https://user-images.githubusercontent.com/57415184/167597150-1deec21e-e1a2-4efe-be5d-7f167c5f7092.jpg)
![3](https://user-images.githubusercontent.com/57415184/167597155-a5fd96b7-0082-465d-a7e5-a7ab2f6f8333.png)
![4(1)](https://user-images.githubusercontent.com/57415184/167597160-de68f0e5-47c9-4995-89fc-d6db556f9153.jpg)

/

/

/

/

## Desktop Dashboard:

![1](https://user-images.githubusercontent.com/57415184/167597383-0dbfb352-4905-405b-8a5a-700638a78d69.jpg)
![2](https://user-images.githubusercontent.com/57415184/167597404-33cbde7f-0331-4b96-9279-4b070365ae44.jpg)
