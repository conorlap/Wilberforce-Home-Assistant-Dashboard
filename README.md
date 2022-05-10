# Wilberforce Home Assistant Dashboard


A few people have been asking for the yaml config so here goes, along with some other brief explanations:


## 1. The ['Devices' desktop card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Devices%20tab)  

Note: The mobile 'Devices' card is the same config but with some bits taken out as I don't need that info on mobile view.

**Required custom cards:**
- [Stack In Card](https://github.com/custom-cards/stack-in-card)   
- [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom)   
- [Text Divider Row](https://github.com/iantrich/text-divider-row)   
- [Lovelace Slider Entity Row](https://github.com/thomasloven/lovelace-slider-entity-row)   
- [Mini Media Player](https://github.com/kalkih/mini-media-player)   

 **A:** [How I control my Macbook Pro volume/mute](https://github.com/bessarabov/mac2mqtt) 
 
 **B:** [How I added the Denon AVR 'Dynamic EQ' and subwoofer level controls](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Denon%20AVR)




/

/





## 2. The ['All Rooms' (Lights and Scripts buttons) desktop card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Lights%20and%20Scripts%20tab)  


**Required custom cards:**
- [Homekit Panel Card](https://github.com/DBuit/Homekit-panel-card)   
- [Mini Graph Card](https://github.com/kalkih/mini-graph-card)   
- [Light Popup Card](https://github.com/DBuit/light-popup-card)   
- [Light Entity Card](https://github.com/ljmerza/light-entity-card)   


 **Note:** The buttons for 'Switch', 'Xbox', 'Plex' and 'Shield' all simply just call scripts that I've created that turn on my TV, surround sound and switch my TV & Receiver to the appropiate HDMI and turns the corresponding device on if supported. (The Nintendo Switch won't turn on this way as we cannot control it via HA). 
 
 The Script buttons are actually Template Switches, so it allows HA to report the 'on state', for example the Shield switch appears on when I'm on my Nvidia Shield. [Example extract from my config.yaml for this.](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Template%20Switch%20config.yaml)






/

/











## 3. The ['Macbook Pro' card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Macbook%20Pro%20card)

**Required custom cards:**
- [Lovelace Slider Entity Row](https://github.com/thomasloven/lovelace-slider-entity-row)
- [Custom Bar-Card](https://github.com/custom-cards/bar-card)



**Note:** The battery % simply comes from the Home Assistant MacOS app, you can expose many sensors from this.

**A:** [How I control my Macbook Pro volume/mute](https://github.com/bessarabov/mac2mqtt)

**B:** [How I pull my Macbook Pro stats](https://www.home-assistant.io/integrations/glances/) & then install and configure glances on your Mac! Note that this only works when my Macbook is on my local network.







/

/








## 4. The [Server Stats/Uptime card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Server%20Stats%20%26%20Uptime%20Card)

**Required custom cards:**
- [Bar Card](https://github.com/custom-cards/bar-card)
- [Uptime Card](https://github.com/dylandoamaral/uptime-card)


**A:** How I pull my local server stats: https://www.home-assistant.io/integrations/systemmonitor/

**B:** [How I pull my remote offsite backup server stats](https://www.home-assistant.io/integrations/glances/) (You must open ports on router at remote site for this to work, **be careful!)**

**C:** [Uptime integration](https://www.home-assistant.io/integrations/uptime/)

**D:** [SMART integration](https://community.home-assistant.io/t/monitor-your-hdd-smart-status/194132), this is quite awkward to setup!






/

/







## 5. The [Plex/Tautulli bandwidth card](https://github.com/conorlap/Wilberforce-Home-Assistant-Dashboard/blob/main/Plex%20card)

**Required custom cards:**
- [Mini Graph Card](https://github.com/kalkih/mini-graph-card)






/

/













# SCREENSHOTS

## Mobile Dashboard:
![1(1)](https://user-images.githubusercontent.com/57415184/167597138-9232043c-8ef1-4024-aeb9-a6f498553a93.jpg)
![2(1)](https://user-images.githubusercontent.com/57415184/167597150-1deec21e-e1a2-4efe-be5d-7f167c5f7092.jpg)
![3](https://user-images.githubusercontent.com/57415184/167597155-a5fd96b7-0082-465d-a7e5-a7ab2f6f8333.png)
![4(1)](https://user-images.githubusercontent.com/57415184/167597160-de68f0e5-47c9-4995-89fc-d6db556f9153.jpg)



## Desktop Dashboard:

![1](https://user-images.githubusercontent.com/57415184/167597383-0dbfb352-4905-405b-8a5a-700638a78d69.jpg)
![2](https://user-images.githubusercontent.com/57415184/167597404-33cbde7f-0331-4b96-9279-4b070365ae44.jpg)
