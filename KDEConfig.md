# KDE Config

Download and set walpaper
https://unsplash.com/photos/v7daTKlZzaw
Photo by <a href="https://unsplash.com/@danielleone?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Daniel Leone</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
## Appearance

Download Themes
```sh
sudo pacman -S kvantum-qt5 make latte-dock
git clone https://github.com/vinceliuice/Qogir-theme.git
git clone https://github.com/vinceliuice/Tela-circle-icon-theme.git
Qogir-theme/install.sh
Tela-circle-icon-theme/install.sh
rm -fr Qogir-theme Tela-circle-icon-theme
```

Download Font
https://fonts.google.com/specimen/Roboto
Download family
Extract, install one (this creates ~/.fonts/r/)
Copy the rest of the font family to above directory

System Settings -> Appearance
### Global Theme
Get New Global Themes...
* Edna By jomada
### Application Style
kvantum-dark
Configure GNOME/GTK Application Style...
Qogir-dark

### Window Decorations
Titlebar Buttons
Arrange Close, minimize, maximize on left. Throw away everything else.

### Fonts
Adjust All Fonts
Roboto 10 pt

### Icons
Tela circle dark

### Cursors
Get New Cursors
McMojave Curors

### Set KVantum theme
Download theme
https://store.kde.org/p/1367055/

Install/Set Theme

## Set Workspace Behaviors
System Settings -> Workspace Behavior ->

### Desktop Effects
[x] Blur
* Light = 9
* Noise = 0
[x] Sheet
[x] Wobbly Windows
[x] Magic Lamp
* Focus
[x] Dialog Parent
[x] Slide Back
* Virtual Desktop Switching Animation
[x] Slide
* Window Open/Close Animation
[x] Scale

### Set Screen Edges
Keep only upper left

### Virtual Desktops
1 Row
4 Desktops

## Window Management
System Settings -> Window Management -> 
### Set Window Placement Center
Window Behavior -> Advanced
Window Placement = Centered

### KWin Scripts
KWin Scripts -> Get New Scripts
* Force Blur By esjeon
* Latte Window Colors By Psifidotos

## Dock
Right Click Desktop -> Add New Widgets -> Get New Widgets -> Download New Plasma Widgets
* Latte SideBar Button By Psifidotos
* Latte Separator By Psifidotos
* Latte Spacer By Psifidotos
* Active Window Control By clearmartin
* Better inline clock By marianarlt
* Simple Menu By Sho

Install virtual-desktop-bar from github
```sh
git clone https://github.com/wsdfhjxc/virtual-desktop-bar.git
virtual-desktop-bar/scripts/install-dependencies-arch.sh
virtual-desktop-bar/scripts/install-applet.sh
```

Download Edna Latte layout
https://store.kde.org/p/1417204/

Replace org.kde.plasma.chiliclock with org.kde.plasma.betterinlineclock

Copy to ~/.config/latte

Start Latte Dock with Edna theme
```sh
latte-dock --layout Edna
```

Remove default panel

Latte dock edit panel

remove virtual desktop bar from bottom dock. Put on top.

Arrange top dock 
1. Application Launcher (do show alternatives -> Simple Menu)
2. Show Desktop
3. Active Window Control
4. Global Menu
5. Justify Splitter
6. Better Inline Clock
7. Justify Splitter
8. Virtual Desktop Bar
9. System Tray

Configure Widgets
Configure Simple Menu
* General -> Icon -> (All) Start Here
Configure Active Window Control
* Appearance ->
  * Hide titlebar for maximized windows
  * Text Type = Application Name
* Buttons
  * Show minimize button
  * Show maximize button
  * Button order = Close, Minimize, Maximize
  * Buttons next to icon and text
  * Position Upper Left, Vertical Center
  * Button Size 4
  * Path to aurorae theme (Edna theme path)
Configure Better Inline Clock
(However you like)
Configure Virtual Desktop Bar
* Appearance -> Style = Number





