# Network-Traffic-Analysis-with-TCPDump

|     | Description |
|-----|-------------|
| 1-  | TCPDump Basics |
| 2-  | Script shell pour surveiller le trafic d'un site web et explorer davantage d'options |
| 3-  | Créer et lire des dump files |
| 4-  | Créer une séquence de fichiers de capture (dump files) avec des limites de taille et de temps |
| 5-  | Créer une séquence de fichiers de capture (dump files) avec des limites de taille et de temps |

## 1- TCPDump Basics

TCPdump est un utilitaire largement utilisé par les professionnels de l'informatique et des réseaux pour capturer et analyser le trafic réseau TCP/IP. Il fonctionne au niveau des paquets, permettant aux utilisateurs de capturer et d'afficher les paquets réseau en temps réel ou de les enregistrer dans un fichier pour une analyse ultérieure.

1-Ouvrez un terminal sur votre bureau et saisissez "tcpdump"

2-Vous constaterez que vous n'avez pas l'autorisation de capturer des paquets, vous devrez donc élever les privilèges en utilisant "sudo".

![](https://imgur.com/BfTpMZs.png)

3- Vous commencerez à capturer des paquets et continuerez à les capturer jusqu'à ce que vous lui ordonniez de s'arrêter en utilisant **Ctrl + c**.

![](https://imgur.com/jX31uRR.png)

4-Saisissez **man tcpdump** pour afficher le manuel de toutes les options disponibles avec tcpdump.

![](https://imgur.com/bcBs5oY.png)

5-Pour capturer un nombre limité de paquets, utilisez l'option "-c" suivie du nombre de paquets que vous souhaitez capturer, comme suit : "sudo tcpdump -c 3"

![](https://imgur.com/xuFGMSy.png)

6- Pour numéroter chaque paquet capturé, ajoutez l'option "-#" à la commande, de la manière suivante : "sudo tcpdump -c 3 -#". Cela ajoutera un numéro à chaque paquet capturé dans la sortie de tcpdump.

![](https://imgur.com/oXT53cq.png)

7-L'option "-D" affiche toutes les interfaces réseau disponibles sur votre station. Vous pouvez l'utiliser avec la commande "tcpdump" de la manière suivante : "sudo tcpdump -D". Cela affichera la liste de toutes les interfaces réseau disponibles sur votre système.

![](https://imgur.com/MXDBgka.png)

8-Utilisez l'option "-i" pour limiter la capture de paquets à une interface spécifique. Vous pouvez spécifier l'interface souhaitée en ajoutant son nom après l'option "-i". Par exemple, pour capturer des paquets uniquement sur l'interface "eth0", vous pouvez utiliser la commande suivante : "sudo tcpdump -i eth0". Cela limitera la capture de paquets à l'interface spécifiée.

![](https://imgur.com/pJkI56i.png)

## 2- Script shell pour surveiller le trafic d'un site web et explorer davantage d'options

1-Capturez quelques paquets à partir d'un site web en utilisant la commande "sudo tcpdump -#tttt host skyroute66.com -c 3" L'option -tttt affiche le résultat dans un format lisible par l'homme, en incluant les informations de temps. L'option "host" dans la commande tcpdump fait référence à la fois aux paquets source et aux paquets destination provenant ou se rendant à l'hôte spécifié (dans ce cas, skyroute66.com).

![](https://imgur.com/DpBGZF7.png)

2- Create a script file named watchdog.sh in which we will put the following script(In this tutorial we are using Visual Studio Code) : 

![](https://imgur.com/dhufanM.png)

3-Dans un terminal, utilisez la commande "ls -al" pour vérifier que le fichier a bien été créé.

![](https://imgur.com/MRw9utu.png)

4-Comme vous pouvez le voir dans le résultat précédent, le fichier n'est pas exécutable. Nous allons le rendre exécutable de la manière suivante :

![](![image](https://github.com/EgorGranon/Network-Traffic-Analysis-with-TCPDump/assets/119436283/561a8545-a9bf-41fa-800f-33b2f0de1e6f)
)

5-Nous pouvons ensuite exécuter et admirer le résultat du script dans le terminal de la manière suivante :

![](https://imgur.com/U62npi5.png)

## 3- Créer et lire des dump files

1-Pour créer un fichier de capture (dump file), ajoutez l'option -w à la fin de votre script de capture de paquets, suivi du nom du fichier que vous souhaitez créer.

![](https://imgur.com/SqLkD5L.png)

2-Pour lire le fichier, utilisez la commande "sudo tcpdump -r"

![](https://imgur.com/tIoFDZm.png)

## 4- Créer une séquence de fichiers de capture (dump files) avec des limites de taille et de temps

Les options -C et -G sont utilisées dans la commande "sudo tcpdump -#XXtttt host skyroute66.com -w captured.pcap -C 1 -G 15". Voici leur signification :

L'option -C spécifie la taille maximale du fichier de capture en mégaoctets. Dans cet exemple, -C 1 signifie que le fichier de capture sera limité à 1 mégaoctet. Lorsque cette taille est atteinte, tcpdump créera un nouveau fichier de capture avec un nom différent.

L'option -G spécifie la durée maximale de capture en secondes. Dans cet exemple, -G 15 indique que la capture s'exécutera pendant 15 secondes avant de créer un nouveau fichier de capture. Cela permet de diviser automatiquement la capture en fichiers de taille et de durée gérables

![](https://imgur.com/2tN3xtw.png)

## 5- Script shell qui utilise des expressions avancées pour fournir plus d'options de filtrage lors de la capture de fichiers dump

![](https://imgur.com/HZ22qd7.png)

L'expression tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420 est une expression de filtrage utilisée dans la commande tcpdump pour capturer les paquets TCP contenant un certain motif. Voici une explication détaillée de l'expression :

tcp[12:1] fait référence au champ de l'en-tête TCP situé à l'offset 12, qui contient des informations sur les options de l'en-tête TCP.

& 0xf0 effectue un masquage (bitwise AND) avec la valeur hexadécimale 0xf0 (ou binaire 11110000). Cela permet de conserver uniquement les 4 bits les plus significatifs (les bits 4 à 7) du champ.

`>>` 2 décale les 4 bits vers la droite de 2 positions, ce qui revient à diviser la valeur par 4.

Le résultat de cette opération (((tcp[12:1] & 0xf0) >> 2)) est utilisé comme indice pour accéder aux octets du flux TCP.

:4 spécifie que 4 octets (32 bits) doivent être comparés.

= 0x47455420 indique que la séquence d'octets recherchée est 0x47455420 (correspondant à la représentation ASCII de "GET").

En résumé, cette expression de filtrage vise à capturer les paquets TCP contenant l'en-tête "GET " dans les données de la charge utile. Cela peut être utilisé pour filtrer spécifiquement les requêtes HTTP GET dans le trafic réseau capturé.

Il est important de noter que cette expression est spécifique à tcpdump et peut nécessiter des ajustements en fonction du contexte et des versions spécifiques de tcpdump utilisées.

