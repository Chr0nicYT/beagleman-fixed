# BEAGLEMAN -- Fixed Edition.
Custom Amazon Alexa commands for the RaspberryPi (AlexaPi) (BeagleAlexa)
# 
# Tutorial
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
5) TYPE: python auth_web.py
6) ON YOUR DESIRED WEB BROWSER! NAVIGATE TO YOUR RASPBERRYS IP FOLLOWED BY THE PORT 5050. EXAMPLE: http://ip:5050
7) LOGIN TO YOUR AMAZON ACCOUNT! THEN CONTINUE WITH THE STEPS?
8) REBOOT YOUR PI WHEN IT SAYS SO.
ON YOUR WEB BROWSER:
1) CREATE! AND LOGIN TO YOUR ACCOUNT on wit.ai
2) ON MyFirstApp, click settings, and copy the API KEY (long all capital string)
3) ON PI: type: nano beagleman.py AND PASTE THAT API KEY WHERE IT SAYS: <wit.ai token>
#
# FUN:
RUN THE SCRIPT AND ASK who created you TO CONFIRM IT WORKS.VOR CUSTOMIZE YOUR OWN COMMANDS.
