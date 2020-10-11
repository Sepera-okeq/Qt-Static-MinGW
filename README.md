# Статическая сборка QT 5.15.1 MinGWx64

Для начала нужно поставить именно Online установку для дополнительных инструментов. [Online Installer](http://download.qt.io/official_releases/online_installers/qt-unified-windows-x86-online.exe "Онлайн Инсталлятор") 


**Дальше нужно установить:**
1. [Python последней версии x64 bit](https://www.python.org/ftp/python/3.8.3/python-3.8.3-amd64.exe "Python последней версии x64 bit")
2. [Perl последней версии x64 bit](http://strawberryperl.com/download/5.30.2.1/strawberry-perl-5.30.2.1-64bit.msi "Perl последней версии x64 bit")
3. [Ruby последней версии x64 bit](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.7.1-1/rubyinstaller-2.7.1-1-x64.exe "Ruby последней версии x64 bit")

Заходим в **Система/Дополнительные параметры системы/Переменные среды/Системные переменные -> выбираем Path и нажать изменить**

Вводим:

Ruby: // может быть новее
- C:\Ruby27-x64\bin 

Perl: // может быть новее
- C:\Strawberry\c\bin
- C:\Strawberry\perl\site\bin
- C:\Strawberry\perl\bin

Python: // может быть новее
- C:\Python\Python38
- C:\Python\Python38\Scripts

MinGW : // может быть новее
- C:\Qt\Tools\mingw810_64\bin
- C:\Qt\Tools\mingw810_64\include 

OpenSSL: 
- C:\Qt\Tools\OpenssL\Win_x64\bin

CMake:
- C:\Qt\Tools\CMake_64\bin

Сохраняем данные системные переменные в Path и закрываем окно Система.

[Далее скачиваем исходники QT 5.15.1](http://download.qt.io/official_releases/qt/5.15/5.15.1/single/qt-everywhere-src-5.15.1.zip "Исходники QT") (может быть новее, поэтому ссылка на все версии - [тык](http://download.qt.io/official_releases/qt/)) и распаковываем архив в любую папку - 

Переходим в нее и начинаем писать в cmd.exe/powershell.exe или создайте рядом с configure батник с названием - install.bat и запустите его через cmd.exe:

`configure -static -debug-and-release -platform win32-g++ -qt-zlib -qt-pcre -qt-libpng -qt-libjpeg -qt-freetype -qt-tiff -qt-webp -opengl desktop -no-angle -sql-sqlite -openssl -I "C:\Qt\Tools\OpenSSL\Win_x64\include" -L "C:\Qt\Tools\OpenSSL\Win_x64" -opensource -confirm-license -make libs -make tools -nomake examples -nomake tests -prefix C:\Qt\5.15.1\mingw81_64_static`

`mingw32-make -k -j4`

`mingw32-make -k install`

И чтоб отлучить об зависимостей MinGW в проект добавляем

`QMAKE_LFLAGS_RELEASE += -static -static-libgcc`
