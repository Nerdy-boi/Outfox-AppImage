#!/bin/bash

STR=$'[Desktop Entry]\nEncoding=UTF-8\nName=OutFox\nGenericName=Rhythm and dance game\nTryExec=OutFox\nExec=OutFox\nTerminal=false\nIcon=OutFox\nType=Application\nCategories=Application;Game;ArcadeGame\nComment=A cross-platform rhythm video game.'
#echo -e $STR > OutFox.desktop

#makes dirs
mkdir OutFox.AppDir
mkdir OutFox.AppDir/usr
mkdir OutFox.AppDir/usr/bin
mkdir OutFox.AppDir/usr/lib

#gets appimagetool
wget -O appimagetoolx64.AppImage https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage
chmod +x appimagetoolx64.AppImage

#extracts the outfox tar.gz in the working directory
ls OutFox*.tar.gz | xargs -I{} tar -xf {} --strip-components=1 --directory OutFox.AppDir/usr/bin

#required things for the appimage
wget https://raw.githubusercontent.com/Nerdy-boi/OutFoxAppImage/main/OutFox.desktop
wget -O OutFox.png https://github.com/Nerdy-boi/OutFoxAppImage/blob/main/OutFox.png?raw=true
mv OutFox.png OutFox.AppDir/OutFox.png
mv OutFox.desktop OutFox.AppDir/OutFox.desktop

wget https://raw.githubusercontent.com/AppImage/AppImageKit/master/resources/AppRun
chmod a+x AppRun
mv AppRun OutFox.AppDir/AppRun

#cant remember what this does.
sed -i -e 's#/usr#././#g' OutFox.AppDir/usr/bin/OutFox
#gets required libs and copies them
ldd OutFox.AppDir/usr/bin/OutFox | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -v '{}' OutFox.AppDir/usr/lib
#forgot what this does. may be important
sed -i -r 's+/usr/share/OutFox/OutFox+OutFox+g' OutFox.AppDir/OutFox.desktop
#builds the appimage
ARCH=x86_64 ./appimagetoolx64.AppImage OutFox.AppDir

#cleanup
rm -r OutFox.AppDir
rm appimagetoolx64.AppImage
ls OutFox*.tar.gz | xargs -I{} rm {}
