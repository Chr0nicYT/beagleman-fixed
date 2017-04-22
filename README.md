# BEAGLEMAN -- Fixed Edition.
Custom Amazon Alexa commands for the RaspberryPi (AlexaPi) (BeagleAlexa)
# 
# Tutorial

PREP:
sudo apt-get install swig python-alsaaudio sox espeak libcurl4-openssl-dev libsox-fmt-mp3 bison autoconf 
YOU WILL REMOVE PYTHON-ALSAAUDIO LATER ON. THIS JUST WORRKED FOR ME.
sudo pip install pycurl cherrypy
sudo -i
nano /root/.bashrc
ADD THE BELOW LINES TO THE BOTTOM OF .bashrc:
export LD_LIBRARY_PATH=/usr/local/lib
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
export PYTHONPATH=/usr/local/lib/python2.7/site-packages/        

NEVER DELETE THE FOLDERS WE ARE CLONING. NEVER.
cd /root/
git clone http://github.com/cmusphinx/pocketsphinx.git
git clone http://github.com/cmusphinx/sphinxbase.git

BELOW, LOOK FOR SOMETHING LIKE: the package (WHATEVER) doesn't seemed to be jnstalled, or something like that. just do sudo apt-get install (that whatever thing)

cd /root/sphinxbase/
./autogen.sh
make
make install

cd /root/pocketsphinx/
./autogen.sh
make
make install

sudo apt-get remove python-alsaaudio

YOU NEED TO RUN THIS:
cd /root/
git clone https://github.com/alexa-pi/AlexaPi
(AT THE FIRST MESSAGE WHERE IT SAYS ABORT, TYPE N FOR NO, THEN PRESS ENTER.)
DON'T ENABLE AT BOOT AND ONLY CLONE IT IN /root/ NOT /opt/
sudo -i
cd /root/AlexaPi/src/scripts/
./setup.sh
1) Go to developers.amazon.com, sign up, then click alexa, then alexa voice service, and create a new profile for a device.
2) Customize the profile id and description to your liking.
3) On the security profile tab, select web, then on the first box put: http://localhost:5050 THEN ADD ANOTHER WITH YOUR PI IP: http://ip:5050
4) On the second box do step number 4, but put "/code" at the end of it.
5) SAVE!
ON YOUR PI:
1) CLONE THIS
ADD AS SUDO!
2) Type: mv ex_creds.py creds.py THEN nano creds.py
3) FILL IN BETWEEN THE QUOTATION MARKS WITH THE STRINGS ON DEVELOPER.AMAZON.COM THAT CORRESPOND TO THE STRINGS BEFORE THE EQUAL SIGN.
4) THEN! CTRL+X, Y, ENTER.  
5) TYPE: python auth_web.py &
6) ON YOUR DESIRED WEB BROWSER! NAVIGATE TO YOUR RASPBERRYS IP FOLLOWED BY THE PORT 5050. EXAMPLE: http://ip:5050
7) LOGIN TO YOUR AMAZON ACCOUNT! THEN CONTINUE WITH THE STEPS?
8) REBOOT YOUR PI WHEN IT SAYS SO.
ON YOUR WEB BROWSER:
1) CREATE! AND LOGIN TO YOUR ACCOUNT on wit.ai
2) ON MyFirstApp, click settings, and copy the API KEY (long all capital string)
3) ON PI: type: nano beagleman.py AND PASTE THAT API KEY WHERE IT SAYS: <wit.ai token>
#
#OPTIONAL TUTORIAL:
THIS WILL SET YOUR SOUNDCARD AS DEFAULT PLAYBACK AND CAPTURE? WORKS WITH SHAIRPORT TOO ;)
sudo nano /usr/share/alsa/alsa.conf
look for defaults.ctl or pcm (something like that)
replace the 0 after that defaults.* with 1
CTRL+X, Y, [Enter]
sudo nano /etc/asound.conf
PASTE THE FOLLOWING:

pcm.!default {
        type plug
        slave {
                pcm "hw:1,0"
        }
}
ctl.!default {
       type hw
        card 1
}

THEN:
CTRK+X, Y, [ENTER]

sudo reboot

TEST ON NEXT STARTUP WITH:
speaker-test


THIS WILL RUN BEAGLEMAN ON BOOT:
sudo -i
cd /etc/init.d/
nano beagleman.sh
PASTE THE BELOW LINES INTO beagleman.sh:

#!/bin/bash
python /root/beagleman/beagleman.py

THEN (You know the drill):
CTRL+X, Y, [Enter]

FINALLY:

update-rc.d /etc/init.d/beagleman.py defaults

TEST BY REBOOTING IT, YOU SHOULD HEAR: "Hello [name], ask me anything"

# FUN:
CHANGE THE GREETING MY OPENING THE PYTHON SCRIPT beagleman.sh AND SEARCH FOR THE FIRST WORD OF THE GREETING UNTIL YOU FIND JT, AND THEN REPLACE WHAT IS IN THE QUOTATION MARKS. 

CHANGE YOUR NAME BY SEARCHING FOR THE WORD NAME, AND CHANGING IT MAKING SURE IT STAYS IN BETWEEN THE TWO QUITATION MARKS.

RUN THE SCRIPT AND ASK who created you TO CONFIRM IT WORKS. OR CUSTOMIZE YOUR OWN COMMANDS.



