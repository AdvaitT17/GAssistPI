# Personal Assistant based on Artificial Intelligence
Artificial intelligence (AI, also machine intelligence, MI) is intelligence exhibited by machines, rather than humans or other animals (natural intelligence, NI). In computer science, the field of AI research defines itself as the study of "intelligent agents": any device that perceives its environment and takes actions that maximise its chance of success at some goal.
# Prerequisites 
**Works with Pi3 as well as Pi Zero W

# Features:  
**1. Headless auto start on boot with multiple wakeword activation trigger.**   
**2. Startup audio and audio feedback for wakeword detection.**   


******************************************************************************************************************************* 
**This is implemented in Python2 so your existing Google Assistant may not work. So please start by making a fresh copy of latest Raspbian**  
*************************************************  
# Note
After extartcting the project rename it to **Personal-AssistPi** in /home/pi/ directory
*************************************************  
**INSTALL AUDIO CONFIG FILES**
*************************************************  
1. Choose the audio configuration according to your setup.    
   (Run the commands till you get .bak notification in the terminal)

  1.1. USB DAC users,  
  ```
  sudo chmod +x /home/pi/Personal-AssistPi/audio-drivers/USB-DAC/scripts/install-usb-dac.sh  
  sudo /home/pi/Personal-AssistPi/audio-drivers/USB-DAC/scripts/install-usb-dac.sh 
  ``` 

  1.2. USB MIC AND HDMI users,  
  ```
  sudo chmod +x /home/pi/Personal-AssistPi/audio-drivers/USB-MIC-HDMI/scripts/install-usb-mic-hdmi.sh  
  sudo /home/pi/Personal-AssistPi/audio-drivers/USB-MIC-HDMI/scripts/install-usb-mic-hdmi.sh  
  ```
  
  1.3. USB MIC AND AUDIO JACK users,  
  ```
  sudo chmod +x /home/pi/Personal-AssistPi/audio-drivers/USB-MIC-JACK/scripts/usb-mic-onboard-jack.sh  
  sudo /home/pi/Personal-AssistPi/audio-drivers/USB-MIC-JACK/scripts/usb-mic-onboard-jack.sh 
  ``` 

**Those Using HDMI/Onboard Jack, make sure to force the audio**  
```
sudo raspi-config  
```
Select advanced options, then audio and choose to force audio

**Those using any other DACs or HATs install the cards as per the manufacturer's guide
 and then you can try using the USB-DAC config file after changing the hardware ids**        

2. Restart Pi

3. Check the speaker using the following command    

```
speaker-test -t wav  
```  

**********************************************************************  
**CONTINUE AFTER SETTING UP AUDIO**
**********************************************************************   

1. Download credentials--->.json file (refer to this doc for creating credentials https://developers.google.com/assistant/sdk/develop/python/config-dev-project-and-account)   

2. Place the .json file in/home/pi directory  

3. Rename it to assistant--->assistant.json  

4. Using the one-line installer for installing Google Assistant and Snowboy dependencies    
**Pi3 and Armv7 users use the "gassist-installer-pi3.sh" installer and Pi Zero users use the "gassist-installer-pi-zero.sh" installer. Snowboy installer is common for both**  
	4.1 Make the installers Executable  
	```
	sudo chmod +x /home/pi/Personal-AssistPi/scripts/gassist-installer-pi3.sh
	sudo chmod +x /home/pi/Personal-AssistPi/scripts/gassist-installer-pi-zero.sh
	sudo chmod +x /home/pi/Personal-AssistPi/scripts/snowboy-deps-installer.sh  
  
	```
	4.2 Execute the installers (Run the snowboy installer first. **Don't be in a hurry and Don't run them parallely, Run them one after the other**
	```
	sudo  /home/pi/Personal-AssistPi/scripts/snowboy-deps-installer.sh
	sudo  /home/pi/Personal-AssistPi/scripts/gassist-installer-pi-zero.sh
	sudo  /home/pi/Personal-AssistPi/scripts/gassist-installer-pi3.sh  
	
	```

5. Copy the google assistant authentication link from terminal and authorize using your google account  

6. Copy the authorization code from browser onto the terminal and press enter    

7. Move into the environment and test the google assistant according to your board  

```
source env/bin/activate  
google-assistant-demo 
googlesamples-assistant-pushtotalk   
```  

8. After verifying the working of assistant, close and exit the terminal    


*************************************************  
**HEADLESS AUTOSTART ON BOOT SERVICE SETUP**  
*************************************************  
1. Make the service installer executable  

```
sudo chmod +x /home/pi/Personal-AssistPi/scripts/service-installer.sh 
```  

2. Run the service installer  

```
sudo /home/pi/Personal-AssistPi/scripts/service-installer.sh    
```  

3. Enable the services - **Pi3 and Armv7 users, if you need custom wakeword functionality, then enable both the services, else enable just the "gassistpi-ok-ggogle.service" - Pi Zero users, enable snowboy services alone**        

```
sudo systemctl enable gassistpi-ok-google.service  
sudo systemctl enable snowboy.service
```  

4. Start the service - **Pi3 and Armv7 users, if you need custom wakeword functionality, then start both the services, else start just the "gassistpi-ok-ggogle.service" - Pi Zero users, start snowboy services alone**    

```
sudo systemctl start gassistpi-ok-google.service  
sudo systemctl start snowboy.service   
```  

**RESTART and ENJOY**  

**Thanks to**

Pi Zero - forked and modified from warchildmd's repo (https://github.com/warchildmd/google-assistant-hotword-raspi).   
Pi 3 Installer has been forked and modified from Shivasiddharth     


