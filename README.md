# Wilberforce Home Assistant Dashboard


A few people have been asking for the yaml config so here goes, along with some other brief explanations.

**Theme**: [hass-kibibit-theme](https://github.com/Kibibit/hass-kibibit-theme)

**Camera/Frigate card**: [frigate-hass-card](https://github.com/dermotduffy/frigate-hass-card)



.
# SCREENSHOTS:

## Desktop Dashboard:

**Main dashboard:**
![ha1](https://user-images.githubusercontent.com/57415184/214659523-14d6e2a9-ad9c-40c9-9006-5663850775ce.png)

**Note**: The blank space there fills up with other cards throughout the day based on conditions. For example, Alexa timer countdowns)

.


**Server/Systems dashboard:**
![Screenshot 2023-01-25 at 18 25 58](https://user-images.githubusercontent.com/57415184/214653305-6b169411-3cc5-4bde-b73a-06ad47807569.png)



## Mobile Dashboard:

**Main Mobile Dashboard:**


![Mobile Main](https://user-images.githubusercontent.com/57415184/214659989-3d601fc8-4e4b-435a-9208-d0f7e4ee876a.png)
![c](https://user-images.githubusercontent.com/57415184/214658584-6af798ef-fae8-45e5-8fe1-0be861f86db8.png)

**Note**: The two indoor cameras are set to only come on when nobody is home, I've just manually switched them on for the screenshots. I like having my front door as the main focus when I first open the app as it's useful to quickly check when someone's at the door.

.

**Server/Systems dasbboard:**

![s](https://user-images.githubusercontent.com/57415184/214656065-8b82d07a-30d4-496d-9cf6-5db412e394ab.png)
![f](https://user-images.githubusercontent.com/57415184/214656073-69600ae6-a586-4296-b27d-a73c9ad09c24.png)
![w](https://user-images.githubusercontent.com/57415184/214656099-92ac5285-9e4f-45b4-8dd6-a663a388f1b7.png)

.

.


# CARD EXPLAINERS





## 1. The ['Devices' desktop card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Devices%20tab)  

**Note:** The mobile 'Devices' card is the same config but with some bits taken out as I don't need that info on mobile view.

![Screenshot 2022-05-10 at 12 08 50](https://user-images.githubusercontent.com/57415184/214660379-ece50d60-bfd6-4c00-9b29-828329a9c219.png)




 **A:** [How I control my Macbook Pro volume/mute](https://github.com/bessarabov/mac2mqtt) 
 
![Screenshot 2022-05-10 at 11 46 24](https://user-images.githubusercontent.com/57415184/214662048-1bd277e7-386c-48dc-a3bb-33575c33a9fe.png)

 
 **B:** [How I added the Denon AVR 'Dynamic EQ' and subwoofer level controls](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Denon%20AVR)
 
![Screenshot 2022-05-10 at 11 52 04](https://user-images.githubusercontent.com/57415184/214663364-c4782fb4-093d-4d9c-b73a-d736460196c1.png)





**Note:** You can control pretty much every single aspect of a Denon Receiver via its IP protocol and the Denon HA integration. 

The list of commands you can publish are [here](https://www.denon.com/-/media/files/documentmaster/denonna/avr-x3700hfy21avr_denon_protocol_v02_04062020.xlsx) on Denon's official website.






  **Required custom cards:**
  - [Stack In Card](https://github.com/custom-cards/stack-in-card)   
  - [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom)   
  - [Text Divider Row](https://github.com/iantrich/text-divider-row)   
  - [Lovelace Slider Entity Row](https://github.com/thomasloven/lovelace-slider-entity-row)   
  - [Mini Media Player](https://github.com/kalkih/mini-media-player)   



.





## 2. The ['All Rooms' (Lights and Scripts buttons) desktop card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Lights%20and%20Scripts%20tab)  

![Screenshot 2022-05-10 at 11 44 15](https://user-images.githubusercontent.com/57415184/214664750-74237b50-8043-4c86-ab01-e0a89c5ab7ca.png)


 **Note:** The buttons for 'Switch', 'Xbox', 'Plex' and 'Shield' all simply just call scripts that I've created that turn on my TV, surround sound and switch my TV & Receiver to the appropiate HDMI and turns the corresponding device on if supported. (The Nintendo Switch won't turn on this way as we cannot control it via HA). 
 
 The Script buttons are actually Template Switches, so it allows HA to report the 'on state', for example the Shield switch appears **'on'** when my Nvidia Shield is on AND my TV is currently on the correct HDMI input. 
 
 **Example extract from my config.yaml for the Template Switches:**


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






**Required custom cards:**
- [Homekit Panel Card](https://github.com/DBuit/Homekit-panel-card)   
- [Mini Graph Card](https://github.com/kalkih/mini-graph-card)   
- [Light Popup Card](https://github.com/DBuit/light-popup-card)   
- [Light Entity Card](https://github.com/ljmerza/light-entity-card)   


.











## 3. The ['Macbook Pro' card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Macbook%20Pro%20card)

![Screenshot 2022-05-10 at 11 46 24](https://user-images.githubusercontent.com/57415184/214665300-c3abcc69-5b9c-43a7-a00e-d8ca3229c1d9.png)










**Note:** The battery % simply comes from the Home Assistant MacOS app, you can expose many sensors from this.

**A:** [How I control my Macbook Pro/mute/Sleep](https://github.com/bessarabov/mac2mqtt)







**Required custom cards:**
- [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom)
- [Stack In Card](https://github.com/custom-cards/stack-in-card)
.










## 4. The [Server Stats](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Server%20Stats%20%26%20Uptime%20Card)


![Screenshot 2022-05-10 at 11 48 57](https://user-images.githubusercontent.com/57415184/214665844-7d3a083c-74df-4808-84f4-d82f12c9e31f.png)



**A:** [What I use to pull my local server stats](https://www.home-assistant.io/integrations/systemmonitor/)

**B:** [What I use to pull my remote offsite backup server stats](https://www.home-assistant.io/integrations/glances/) (My servers are connected together via Wireguard VPN so no need to open ports)

**C:** [Uptime integration](https://www.home-assistant.io/integrations/uptime/)








**Required custom cards:**
- [Bar Card](https://github.com/custom-cards/bar-card)
- [Uptime Card](https://github.com/dylandoamaral/uptime-card)
- [Stack In Card](https://github.com/custom-cards/stack-in-card)
.






## 5. The [Plex/Tautulli bandwidth card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Plex%20card)

![Screenshot 2022-05-10 at 11 51 13](https://user-images.githubusercontent.com/57415184/214666954-297d219a-3d03-4943-87e7-e573ec09d74d.png)







**Required custom cards:**
- [Mini Graph Card](https://github.com/kalkih/mini-graph-card)
- [Stack In Card](https://github.com/custom-cards/stack-in-card)








