# ESP32-on-Osx-and-Big-Sur
https://github.com/espressif/arduino-esp32/issues/4408
by https://github.com/igor17400

I have decided to write a summary for all those reading the post at a later time.

Open your arduino IDE and press command + , to open preferences window.

Click the preferences path at the bottom. This should open finder with the path being used by arduino IDE. If for some reason this doesn't work, make use of a manual step. Open the terminal and run open /Users/<user>/Library/Arduino15/

Dive into /Users/<user>/Library/Arduino15/packages/Heltec-esp32/hardware/esp32/0.0.5/tools/esptool.py and copy esptool.py file.

4.1) Paste the copied file into /Users/<user>/Library/Arduino15/packages/Heltec-esp32/tools/esptool_py/2.6.1/

4.2) Open /Users/<user>/Library/Arduino15/platform.txt file and change tools.esptool_py.cmd=esptool to tools.esptool_py.cmd=esptool.py

Run ls /Users/<user>/Library/Arduino15/packages/Heltec-esp32/tools/esptool_py/2.6.1/ to check if the file was indeed copied. You should see two files, esptool and esptool.py. However, esptool - without py extension - isn't nedded.

Quit and reopen arduino IDE. Try to run the script on the IDE.

If the script does not work, after all those steps, due to the following error ImportError: No module named serial read the next steps.

Open your terminal and make sure you aren't in any virtual environment, unless you're running your arduino IDE in some virtual environment. If you aren't, which was my case, I tried several times to run python -m pip install pyserial, however I kept receiving the same error ImportError: No module named serial. The problem was that pyserial library was being installed on python3 environment and my Arduino IDE was running at python2.

Install pip for python2 via curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py afterwards run python2 get-pip.py

Run python2 -m pip install pyserial and try to run the script again in arduino IDE.

Those steps worked for me, I hope it helps

:)
