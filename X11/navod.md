
# NÁVOD NA INŠTALÁCIU A POUŽITIE #

## Inštalácia na Ubuntu ##

Platí pre Ubuntu s Gnome, KDE a väčšinu ďalších distribúcií nezaložených na Ubuntu.

Nakopíruj súbor sk-imega2 do /usr/share/X11/xkb/symbols:

    sudo cp sk-imega2 /usr/share/X11/xkb/symbols


## Aktivácia ##

Nové rozloženie klávesnice sa dá aktivovať príkazom sexkbmap:

    setxkbmap -layout "sk-imega2"
    
Ak nemáš rád klávesu Caps Lock a otravuje ťa, keď ju náhodne zmačkneš, môžeš týmto zmeniť jej význam na AltGr:

    setxkbmap -layout "sk-imega2" -option "lv3:caps_switch"
    
Ak chceš prepínať medzi dvomi rozloženiami/jazykmi klávesnice, stačí pridať ďalší kód rozloženia do hodnoty parametra `-layout`. Potom funguje obvyklá klávesová skratka na prepínanie klávesnice nastavená v Gnome/KDE (napr. Alt+Shift). Napríklad:

    setxkbmap -layout "sk-imega2,ru"

Ak chceš mať rozloženie nastavené hneď po štarte OS, vrátane prihlasovacej obrazovky a textového režimu (Ctrl+Alt+F1), vyplň rozloženie v `/etc/default/keyboard`, napríklad takto:
    
    XKBMODEL="pc105"
    XKBLAYOUT="sk-imega2"
    XKBVARIANT=""
    XKBOPTIONS="lv3:caps_switch,terminate:ctrl_alt_bksp"
    BACKSPACE="guess"

V Ubuntu 16.04 to takto stačí, ale v Ubuntu 18.04 je treba ešte ďalšie kroky:
    
    sudo dpkg-reconfigure keyboard-configuration       # v sprievodcovi vyber Slovenčinu/QWERTY
    service keyboard-setup restart
    
Pokiaľ chceš používať klávesnicu v Gnome spolu s iným rozložením, je nutné nahradiť súbor `sk` so štandardným slovenským rozložením:

    cd /usr/share/X11/xkb/symbols
    sudo mv sk sk_orig
    cd -
    sudo cp sk /usr/share/X11/xkb/symbols

    
## Editovanie rozloženia ##

Po editácii súboru sk-imega2 sa zmeny neprejavia okamžite, pretože rozloženie sa kešuje. Je nutné spustiť tento príkaz (Ubuntu 16.04 a novšie):

    sudo dpkg-reconfigure xkb-data


## Autori a licencia ##

Autori: Igor Mega, Andrej Repiský, 2017
Licencia: Freeware bez akejkoľvek záruky.
