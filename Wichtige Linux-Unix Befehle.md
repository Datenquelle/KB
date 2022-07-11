## zeigt die aktuelle Shell an.
```bash
echo $0
```

## entspricht %1 in DOS.
```bash
$*
```

## zeigt die Belegung eines Verzeichnisses an
```bash
du –sch /***%PATH%***/
```

## findet alle Dateien die mit STRING beginnen und leitet das Ergebnis in die Datei ergebnis.txt um. Der ganze Befehl wird im Hintergrund (&) ausgeführt.
```bash
find /%PATH%/ -name '%STRING%*' > ergebnis.txt &
```

## sucht und ersetzt Text innerhalb aller Dateien im angegebenen Verzeichnis.
```bash
find /%PATH%/ -type f -exec sed -i 's/%SEARCH TERM%/%NEW STRING%/' {} \;
```

## sucht alle Verzeichnisse inkl. Unterverzeichnisse vom Benutzer und löscht sie. Anstelle des Parameters ›d‹ für Directory kann ›f‹ für File angegeben werden.
```bash
find /%PATH%/ -type d -user ${USER} -exec rm -Rf {} \;
```

## sucht String in Dateien mit einer Erweiterung.
```bash
grep -r -l '%STRING%' /%PATH%/*.%EXTENSTION%
```

## löscht aus dem angegeben Verzeichnis und dessen Unterverzeichnisse die entsprechen Dateien
```bash
find /%PATH%/ -name %FILE% -exec rm -rf {} \;
```

## Zeigt die gesamte Anzahl Dateien in einem Verzeichnis samt Inhalt an.
```bash
find /%PATH%/ -type f -print | wc -l
```

## Verkettung von zwei Befehlen. Zuerst wird find /path/file* ausgeführt und erst am Schluss der Befehl cp.
```bash
cp `find /%PATH%/%FILE%*` /%PATH%
```

## Bilder-Konvertierung mit sips. [Quelle des Tipps]([http://osxdaily.com/2013/01/11/converting-image-file-formats-with-the-command-line-sips/)
```bash
for i in *.png;do sips -s format jpeg $i --out $i.jpg;done
```

## Bilder-Konvertierung mit convert. [Quelle des Tipps](https://superuser.com/questions/71028/batch-converting-png-to-jpg-in-linux)
```bash
for i in *.png ; do convert "$i" "${i%.*}.jpg" ; done
```

## Batch-Renaming von Dateien mit Leerschlägen in Unterstrich. [Quelle des Tipps](https://bbs.archlinux.org/viewtopic.php?id=36305)
```bash
ls | while read -r FILE; do mv -v "$FILE" `echo $FILE | tr ' ' '_' | tr -d '[{}(),\!]' | tr -d "\'" | tr '[A-Z]' '[a-z]' | sed 's/_-_/_/g'`; done
```

## Batch-Renaming von Dateien mit Leerschlägen in Unterstrich: Wichtig! Ins gewünschte Verzeichnis wechseln! [Quelle des Tipps](https://stackoverflow.com/questions/1806868/linux-replacing-spaces-in-the-file-names)
```bash
for i in *' '*; do   mv "$i" `echo $i | sed -e 's/ /-/g'`; done
```

## Ändert das Änderungsdatum auf das Original Änderungsdatum. [Quelle des Tipps](https://unix.stackexchange.com/questions/89264/change-file-created-date-from-jpeg-exif-metadata/153447)
```bash
exiftool "-DateTimeOriginal>FileModifyDate" file*.jpg
```

## Clamav: Virenscan mit exclude-Dirs
```bash
sudo clamscan -i -r --exclude-dir="^/sys" --exclude-dir="^/%DIRECTORY%" --exclude-dir="^/%DIRECTORY%" --exclude-dir="^/%DIRECTORY%" /
```

## Checksum einer Datei überprüfen.
```bash
echo "%256-CHECKSUM% %FILE%.%EXTENSTION%" | shasum -a 256 --check
```

## löscht einen eine ganze Zeile mit einem bestimmten String.
```bash
grep -rl '\[%STRING%\]' %FILE% | xargs sed -i '/\[%STRING%\]/d'
```

## löscht das Zeilenende einer Textdatei
```bash
truncate -s -1 %FILE%
```
