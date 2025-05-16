Dépendances: Pour compiler le projet, vous aurez besoin d'un compilateur
croisé vers i686-elf.
(Pour que les scripts fonctionnent tels quels nous conseillons d'utiliser
gcc, dont le compilateur croisé peut s'installer en suivant les instructions
sur cette page: https://wiki.osdev.org/GCC_Cross-Compiler ).
Vous aurez besoin pour tester le projet d'une version de qemu simulant 
du i386 ainsi que la carte réseau rtl8139.

Versions téstées avec le projet:
- i686-elf-gcc version 14.2.0
- qemu-system-i368 version 6.2.0

Lien vers le git du projet:
https://github.com/MariusBerth/OS
(À noter que si vous avez récupéré ce projet via ce lien, il faudra peut-être
aussi cloner le sous module git meaty-skeleton pour le voir apparaitre.
Il peut aussi être récupéré indépendamment à l'adresse
https://github.com/MariusBerth/meaty_skeleton-copy-)

**Compilation** 
Il faut se placer dans le sous répertoire meaty-skeleton
(qui est le répertoire qui contient le système d'exploitation à
proprement parler).
Si vous souhaitez utiliser un autre compilateur que gcc, il faudra
modifier la définition de $CC qui se situe dans
./config.sh (non tésté).

On peut ensuite utiliser certains scripts pour compiler et lancer le projet
(À noter que chacun de ces scripts appelle lui-même les autre scripts si
nécéssaire, il n'est donc pas nécéssaire de lancer le script 
build.sh pour lancer le script qemu.sh).

build.sh : se place dans le sous répertoire kernel, compile et linke le
noyau

iso.sh : crée une image bootable de l'os

qemu.sh : lance deux instances de qemu simulant chacune une instance de l'os.
Certaines options sont passées à qemu pour simuler dans chaque instance une
carte réseau ainsi que pour simuler une connecion ethernet entre les deux.


**Utilisation**
Après le boot, l'os rentre dans un shell qui permet de lancer des commandes 
pour accéder aux différentes fonctionnalités de celui ci. La commande help 
permet de les lister directement depuis l'intérieur de l'os.


**Organisation et origine du code**
Ce projet construit sur la base du projet meaty-skeleton de 
https://wiki.osdev.org.
Le projet meaty-skeleton d'origine peut être récupéré via git.
Les adresses de clonages sont trouvables à l'adresse suivante:
https://gitlab.com/sortie/meaty-skeleton.

Le sous répertoire meaty-skeleton/libc/ contient la librairie c standard de
l'os. Celle-ci ne peut pas ètre utilisée pour programmer depuis l'os
et est en majorité inchangée du projet d'origine.
Les seules différences étant string_to_int, volatile_memcpy qui ont été 
ajoutées et la fonction putchar qui à été modifiée pour utiliser notre 
affichage.

La majorité du projet se situe dans le répertoire meaty-skeleton/kernel.
Dans le dossier meaty-skeleton/kernel/arch/i368 on trouve 
la gestion de l'affichage que nous avons écrite ainsi que l'assembleur 
de boot que nous avons modifié pour passer de l'utilisation de 
la spécification multiboot 0.6.96 à la spécification multiboot 2 et
pour avoir un framebuffer. 
Ensuite dans le dossier meaty-skeleton/kernel/drivers nous trouvons
les drivers claviers, pci et rtl8139 (carte réseau).
Ils ont été écrits en utilisants diverses ressources:
driver pci: https://wiki.osdev.org/PCI 

driver rtl8139: https://github.com/arduino/uboot-yun/blob/master/drivers/rtl8139.c,
  https://github.com/TritonDataCenter/syslinux/blob/master/gpxe/src/drivers/net/rtl8139.c
  https://wiki.osdev.org/RTL8139
  https://www.qemu.org/docs/master/system/devices/net.html (Pour l'invoation de Qemu)  

driver clavier 
##TODO: A remplir


Dans le répertoire meaty-skeleton/kernel/shell se situe le code principal
du shell ainsi que celui de ses fonctions:
##TODO: A remplir 


Finalement, le dossier meaty-skeleton/kernel/games comporte un seul
sous-dossier pertinent, le sous dossier morpion,
qui contient un fichier qui définit les fonctions nécéssaires pour jouer
au morpion avec notre os (sur une seule ou plusieurs instances).


