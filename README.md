# Network-Traffic-Analysis-with-TCPDump

|     | Description |
|-----|-------------|
| 1-  | TCPDump Basics |
| 2-  | Create shell script for website traffic monitor and explore more options |
| 3-  | Create and read dump files |
| 4-  | Create sequence of dump files with size and time limits |
| 5-  | Advanced expressions for more filtering options |

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

## 2- Create shell script for website traffic monitor and explore more options

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

## 3- Create and read dump files

1-Pour créer un fichier de capture (dump file), ajoutez l'option -w à la fin de votre script de capture de paquets, suivi du nom du fichier que vous souhaitez créer.

![](https://imgur.com/SqLkD5L.png)

2-Pour lire le fichier, utilisez la commande "sudo tcpdump -r"

![](https://imgur.com/tIoFDZm.png)

## 4- 


