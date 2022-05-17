<img src="img/browser_auswaehlen.png" width="800" />

# Browser auswählen
Es können mehrere Browser (Firefox, Chrome, Edge, Opera, Safari usw.) installiert werden. Es kann sein, dass man einen Link zu einer Webseite, anstelle des Standard-Browsers, in einem anderen Browser öffnen möchte.  
Zu diesem Zweck gibt es verschieden Tools (Dienstprogramme). Hier eine kleine Auswahl:

## Apple macOS

### Browserosaurus
* Quelle: [https://browserosaurus.com/](https://github.com/will-stone/browserosaurus)
* Bemerkungen: Es handelt sich hier um eine Open Source Lösung.

### Choosy
* Quelle: [https://www.choosyosx.com/](https://www.choosyosx.com/)
* Bemerkungen: Hier handelt es sich um eine kostenpflichtige Anwendung.

## Microsoft Windows

### BrowserSelector
* Quelle: [https://apps.microsoft.com/store/detail/browserselector/9P7FSLDKDXH3?hl=de-de&gl=DE](https://apps.microsoft.com/store/detail/browserselector/9P7FSLDKDXH3?hl=de-de&gl=DE)
* Bemerkungen: Kostenlos

## Linux (Debian usw.)

### Select-Browser
* Quelle: [https://unix.stackexchange.com/questions/487203/choose-which-browser-to-open-link-in](https://unix.stackexchange.com/questions/487203/choose-which-browser-to-open-link-in)
* Bemerkungen: Hier handelt es sich um eine Kombination von einem Shell-Script, einer Desktop-Verknüpfung und Shell-Befehlen.

Im ersten Schritt wird das Shell-Script erstellt:
```
sudo nano /usr/bin/selcect-browser.sh **(chmod nicht vergessen)**

#!/bin/sh

BROWSER=$(zenity --list --radiolist --text '' --column='check' --column=browser --width=320 --height=284 --title='Browserwahl' --text='Bitte Deinen gewünschten Browser wählen...' TRUE "firefox" FALSE "google-chrome" FALSE "chromium" FALSE "microsoft-edge" FALSE "opera")

$BROWSER $\* &
```

Nun muss noch eine Desktop-Verknüpfung erstellt werden damit das »Programm« vom aus Desktop gestartet werden kann:
```
sudo nano /usr/share/applications/selcect-browser.desktop

[Desktop Entry]
Version=1.1
Type=Application
Name=Select Browser
GenericName=Browser wählen
Comment=Browser wählen
Exec=/usr/bin/select-browser.sh %U
Icon=/usr/share/icons/users/Netscape.png **(irgendein Logo)**
Actions=new-window;new-private-window;NewShortcut;NewShortcut1;
Categories=Application;Utility;
StartupNotify=true
StartupWMClass=select-browser
MimeType=x-scheme-handler/unknown;x-scheme-handler/about;text/html;text/xml;application/xhtml\_xml;image/webp;x-scheme-handler/http;x-scheme-handler/https;x-scheme-handler/ftp;
```

Zum Schluss muss noch die Desktop-Verknüpfung als »Standard-Browser« eingestellt werden:
```
xdg-mime default select-browser.desktop x-scheme-handler/http
xdg-mime default select-browser.desktop x-scheme-handler/https
```

#### Tipp
* Mit ```xdg-settings set default-web-browser firefox.desktop``` kann z.B. Firefox wieder als Standard-Browser eingestellt werden.
* Mit ```xdg-mime query default x-scheme-handler/http``` und ```xdg-mime query default x-scheme-handler/https``` kann der Standard-Browser überprüft werden.
