## Source et énoncé du CTF

https://www.root-me.org/fr/Challenges/Forensic/Trouvez-le-chat

## Write-up

![1](https://drive.google.com/file/d/1LPc1bLOcL_MnG6kNs8xxPUUPO0BLDd9C/view?usp=drive_link)

https://drive.google.com/file/d/1LPc1bLOcL_MnG6kNs8xxPUUPO0BLDd9C/view?usp=drive_link


L’énoncé du problème nous indique que le fichier que l’on télécharge est le dump d’une clé USB du suspect. On a donc ici à faire à une analyse de mémoire non-volatile.

Un outil très intéressant pour analyse la mémoire non-volatile est Autopsy/The Sleuth Kit qui nous permet notamment de naviguer dans le file system et en particulier de récupérer les fichiers supprimés. On ouvre donc le fichier de dump avec le logiciel :

 

Remarque : d’autres outils Windows et Linux sont utilisables pour explorer le file system comme TestDisk/PhotoREC, Access Data FTK Imager, ou encore Bulk Extractor, Foremost

En fouillant dans le répertoire, on remarque un document intéressant qui avait été supprimé : le fichier revendication.odt. En ouvrant le fichier, on voit la photo du chat recherché et le message de revendication. On se dit alors que peut-être que la photo du chat contient des données EXIF et en particulier des coordonnées GPS. On extrait/enregistre donc l’image et on analyse ses données EXIF. Et là, rien du tout ! On peut patauger très longtemps si on ne sait pas qu’un fichier .odt est en réalité une archive .zip de fichiers .xml. 

En changeant l’extension .odt en .zip du fichier revendication.odt, et en l’extrayant, on obtient le contenu du fichier sous forme de fichiers .xml. 

 
Dans cette arborescence, on retrouve la photo du chat :
 

Et en extrayant les données EXIF de cette photo, on retrouve les coordonnées GPS de la ville recherchées :
 

Remarque : pour quoi ne retrouve-t’on pas les coordonnées GPS en analysant simplement les données EXIF de la photo du chat que l’on enregistre simplement depuis le fichier .odt ??? Mystère



## Flag


