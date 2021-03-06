the-bike-shed
================================================================================

`@TODO` what are the high level goals of this project?


Development
--------------------------------------------------

For best results, listen to this on repeat: https://www.youtube.com/watch?v=T1CowKULMx8

### [VSCode](https://code.visualstudio.com/)

0. Install and setup docker:
    - Windows & MAC install docker desktop
    - Ubuntu:
        0. `sudo apt install docker.io; sudo usermod -aG docker $USER`
        1. re-login
    - Linux follow directions for your distro...
1. Install the "Remote - Containers"
   (`ms-vscode-remote.remote-containers`) exension
2. Clone this code locally.
3. Open the project folder in VSCode
4. It should prompt to "Reopen in Container", do that. else do
   `Command Pallette -> "Reopen in Container"`
    - Note: You can ignore the message about git missing, it will get
      installed in the next step
5. Once it's loaded in the new container run the "setup dev
   environment" task. Command Pallette -> "Run Task"
6. Re-open window (so that vscode will realize git is now installed)
7. Run the default build task to build...
    - To clean and rebuild: uncomment line 44 and then comment out
      lines 45 & 47 of build.bash. Save and run build task again. Then
      undo and run build task again

Hardware List
--------------------------------------------------

This list is a work in progress.

 - [Raspberry PI Zero W][pi0w]
 - PI0 GPIO keypad (`@TODO` what type? link?)
 - PI0 GPIO LCD 2x16 Char display (`@TODO` what type? link?)
 - SD Card (`@TODO` what type? link?)
 - Communication (See `TODO -> Hardware Research`)
 - Mains Power supply (See `TODO -> Hardware Research`)
 - Solenoid / electric strike (See `TODO -> Hardware Research`)
 - Internal 5v regulator (See `TODO -> Hardware Research`)

[pi0w]: https://www.raspberrypi.org/products/raspberry-pi-zero-w/

TODO
--------------------------------------------------

Items below are either incomplete (☐) or complete (☑). Skipped items
are <strike>striked out</strike>.


### Code

- ☐ Create skeleton code for shed
  - ☐ async curl
  - ☐ p2p UDP packets...
  - ☐ Periodic autosave
- ☐ Testing framework

- ☐ non vscode directions for building

- ☐ prototype code for PI0 GPIO keypad

- ☐ prototype code for PI0 GPIO LCD 2x16 Char display
  - ☐ memfd device file...

- ☐ LIBCURL grab master-config from server

- ☐ Parse master config

- ☐ Trade config with peers

- ☐ Synchonize time?
  - Do it with the time http headers when we get master-config?

- ☐ Crypto all the things
  - ☐ sign p2p configs? have peer keys in master-config?
  - ☐ [argon2d][a2d] for RFID serials
  - ☐ Encrypt the list of IPs in the master-config

- ☐ Make buildroot config

[a2d]: https://en.wikipedia.org/wiki/Argon2


### Hardware

- ☐ Make schematics for exterior board.
- ☐ SDCARD leveling torture test, need to make sure that the SDcard
  will last for the lifetime, 30 new accesses per day * 365 days * 5
  years should be plenty.

### Hardware Research

- ☐ Research into ATMEL - RPI long distance/cheap/reliable
  communication...
    - TTL? [MAX232][max232]? MAX485?
    - Research reliabiliy options like parity? or CRC?
- ☐ Research into solenoid/electric strike, need to pin down voltage
  - Candidate: [(DC12V) Failure Secure ANSI Standard Heavy Duty Electric Strike Lock][lock]
- ☐ Power mosfet
  - Article: [Byte and Switch (Part 1)][bas]
- ☐ Mains Power supply:
  - Canidate: [RS-25-12][rs25] (Probably is overkill?)
- ☐ Internal 5v regulator:
  - StackExchange: [Powering a PI from 12v][se12v]

[max232]: https://en.wikipedia.org/wiki/MAX232
[lock]: https://www.amazon.com/dp/B01MXZ0EKQ
[bas]: https://www.embeddedrelated.com/showarticle/77.php
[rs25]: https://www.digikey.com/product-detail/en/mean-well-usa-inc/RS-25-12/1866-4140-ND/7706175
[se12v]: https://raspberrypi.stackexchange.com/a/19964


Streatch Goals (TODOs for after MVP)
--------------------------------------------------

- ☐ Research alternate auth mechanisms:
  - Just using serials from NFC has a few security issues:
    - Easily skimmed
    - Small address space, trivially brute-forced, especially on clippercards
  - Possible Solutions:
    - Use bigger (1k) payloads
    - Use Challenge response NFC
    - Use BLE (phone?)
