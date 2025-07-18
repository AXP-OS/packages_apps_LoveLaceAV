LoveLaceAV
=======

![IMAGE](app/src/main/res/mipmap-xxhdpi/ic_launcher.png)

Overview
--------
LoveLaceAV is a FOSS malware scanner for Android. It is powered by ClamAV style signature databases and forked from [Hypatia](https://codeberg.org/divested-mobile/hypatia) made by the Divested Computing Group.

See all the details at the [LoveLaceAV website](https://axpos.org/lovelace)


[<img src="https://hosted.weblate.org/widget/divestos/hypatia/287x66-grey.png"
     alt="Translation status"
     height="66">](https://hosted.weblate.org/projects/maintainteam/hypatia/)

Features
--------
- Near zero battery impact: you'll never notice any impact on battery at all
- Extremely fast: it can scan small files (1MB) in <20ms, and even large files (40MB) in 1000ms.
- Memory efficient: with the default databases enabled it uses under 120MB.
- Regular scan: allowing selection of /system, internal storage, external storage, and installed apps
- Realtime scanner: can detect malware in realtime on write/rename in internal storage
- Completely offline: Internet is only used to download signature databases, files will never ever leave your device
- Persistence: will automatically restart on boot/update
- Tiny codebase: coming in at under 1000 sloc, it can be audited by even someone with basic programming experience
- Minimal dependencies: the app only uses libraries when necessary
- Signature databases can be enabled/disabled at the users demand

Download
--------
While it is possible to download LoveLaceAV directly it is strongly recommended using the public **AXP.OS F-Droid repo**.

- Direct download: [here](https://codeberg.org/AXP-OS/packages_apps_LoveLaceAV/releases), [mirror](https://github.com/AXP-OS/packages_apps_LoveLaceAV/releases)
- F-Droid repo: [here](https://axpos.org/F-Droid)

Troubleshooting
------------------
- **The app crashes and is very buggy:**
The first thing to check is if you have extended databases enabled. Extended databases require more RAM (8 GB), and can occasionally cause the app to be very buggy.
- **Unable to download databases:**
If this occurs, try tapping the ellipsis in the top right of the main screen and tap `Database server override`. This uses a mirror database in case the main database is down.
- **There are false positives:**
This occasionally occurs due to the nature of bloom filters. If you believe there is a false positive, first, rescan. This will sometimes fix the false positive. And if this still returns a false positive, scan the file to [VirusTotal](https://www.virustotal.com/gui/home/upload), and this will tell you if you truly have a false positive or rather some malware.

Signature Databases
-------------------

- Default database:
	- Signing key: `14C17E7F99EABF3F`
	- Database: https://lav.axpos.org/db
- Hypatia-Fork @codeberg:
	- Signing key:`5298C0C0C3E73288`
	- Database: https://codeberg.org/MaintainTeam/HypatiaDatabases/
- Hypatia-Fork @github:
	- Signing key: `5298C0C0C3E73288`
	- Database: https://github.com/MaintainTeam/HypatiaDatabases/

Technical Details
------------------
- Signature databases are serialized Guava BloomFilter object format
- Signature databases will not be redownloaded if the file hasn't changed on the server (304 not modified)
- Signatures are stored using BloomFilters for O(k) lookup
- Files have their MD5/SHA-1/SHA-256 hashes calculated in one pass
- Realtime scanner is multithreaded and will use half of the device's core count for scanning multiple files asynchronously
- Realtime scanning powered by a recursive FileObserver
- Network connections will be made to the following: https://lav.axpos.org/db/hypatia-*-bloom.bin{,.sig}
- Statistics & generation output of the current database is available via  https://lav.axpos.org/db

Permissions
-----------------
- `ACCESS_NETWORK_STATE`
- `FOREGROUND_SERVICE` and `FOREGROUND_SERVICE_SPECIAL_USE`: Used for realtime scanning.
- `INTERNET`: Download and update databases.
- `MANAGE_EXTERNAL_STORAGE`: Used for reading malicous files for scanning, and deleting infected files.
- `QUERY_ALL_PACKAGES`: Used for scanning malicous apps.
- `READ_EXTERNAL_STORAGE`: Scanning external storage.
- `RECIEVE_BOOT_COMPLETED`: Restart the app on reboot.
- `REQUEST_DELETE_PACKAGES`: Used for removing infected apps.
- `POST_NOTIFICATIONS`: Notifications.
- `WAKE_LOCK`
- `WRITE_EXTERNAL_STORAGE`: Used for removing infected files.
- `ACCESIBILITY_SERVICE`: Used to allow the link scanner to read the screen and check for malicious domains.
- `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`

Planned Updates
----------------
- Option to scan on access
- Scan newly installed/updated apps
- Option to let 3rd-party apps invoke scans
- Automatic database updates
- Database sanity checks
- Testing
- Better GUI
- Translations
- Scanning entire system using root (low priority)

Goals
-----
- Be fast
- Don't eat batteries
- Use minimal permissions
- Use libraries only when necessary

Credits
-------
- Divested Computing Group for [Hypatia](https://divestos.org/pages/our_apps#hypatia)
- MaintainTeam-Hypatia: https://github.com/MaintainTeam/Hypatia
- ClamAV for the databases (GPLv2)
- ESET for extra databases (BSD 2-Clause)
- Nex (@botherder) for extra databases (CC BY-SA 4.0)
- Amnesty International for extra databases (CC BY 2.0)
- Echap for extra databases (CC BY 4.0)
- MalwareBazaar for extra databases (CC0)
- RecursiveFileObserver.java (GPL-3.0-or-later): Daniel Gultsch, ownCloud Inc., Bartek Przybylski
- GPGDetachedSignatureVerifier.java (GPL-2.0-or-later): Federico Fissore, Arduino LLC
- Petra Mirelli for the app banner/feature graphic and various tweaks.
- @eloitor: Translations work
- Various for signatures which can be found at [https://lav.axpos.org/db](https://lav.axpos.org/db)

Translations
------------
- Afrikaans: Oswald van Ginkel
- Arabic: abdelbasset jabrane, ABDO GM
- Chinese (Simplified): Sdarfeesh, Crit, 大王叫我来巡山
- Chinese (Traditional Han script): 張可揚
- Croatian: lukapiplica
- Czech: Fjuro
- Estonian: Priit Jõerüüt
- Finnish: huuhaa, Ricky Tigg
- French: cardpuncher, Jean-Luc Tibaux, Petra Mirelli, thraex
- Hebrew: elid34
- Galician: ghose, josé m
- German: thereisnoanderson, Balthazar1234, Petra Mirelli, Ettore Atalan
- Greek: Dimitris Vagiakakos
- Indonesian: Adrien N
- Italian: Tommaso Fonda, srccrow, Petra Mirelli, Dark Space
- Japanese: honyaku
- Polish: Marcin Mikołajczak
- Portuguese (Brazil): lucasmz
- Portuguese: jontaix, inkhorn, ssantos
- Romanian: Renko
- Russian: yurtpage, q1011, Andrey
- Slovak: Pa Di
- Spanish: gallegonovato, Manuel-Senpai, Petra Mirelli
- Turkish: cardpuncher
- Ukrainian: Fqwe1

Notices
-------
- Divested Computing Group is not affiliated with Cisco or ESET
- LoveLaceAV is not sponsored or endorsed by Cisco or ESET
- MaintainTeam is not affiliated with Cisco or ESET


