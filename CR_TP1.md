
# Compte rendu TP1
## Administration systèmes
BERARD Lucas
DUFRENE Mélic

## Exercice 2: Prise en main de l'interpréteur de commandes

### Manuel
	1. man which indiques que which permet de trouver l'executable lié à une commande (chemin)
	2. Pour rechercher par mot clef dans le manuel:
		man which *(on entre dans le manuel)*
		/option *(on cherche le terme option dans ces pages du manuel)*
	3. Pour quitter le manuel, il suffit de taper q
	4. Présentation de la section 6 du manuel:
		man 6 introduction *(c'est une page de jeux ou logiciels "funs")*
### Navigation dans l'arborescence de fichiers
	1. Aller dans le dossier /var/log:
		cd /var/log
	2. Revenir au dossier parent:
		cd ..
	3. Revenir au dossier personnel:
		cd ou cd ~
	4. Revenir au dossier précédent:
		cd -
	5. Acceder au dossier /root via cd /root est impossible par manque de droits 
	6. sudo cd /root ne fonctionne pas non plus car le super-user ne possède pas de fonction cd (dans sbin)
	7. Créer un arborescence:
		cd
		touch Dossier1/Fichier1
		touch Dossier2/Dossier2.2/Fichier2
		touch Dossier2/Dossier2.2/Fichier3
		mkdir Dossier2/Dossier2.1
	8. Suppression de fichiers et de dossiers:
		cd
		rm Dossier2/Fichier1
		rm Dossier2 *( Ne fonctionne pas car c'est un dossier )*
		
	9. Pour supprimer un dossier, on fait :
		rmdir Dossier2
	10.La commande précédente supprime le dossier s'il est vide
	11.Pour supprimer un dossier et son contenu :
		rmdir -r Dossier2 *(-r pour récursif)*

### Commandes importantes
	1. Pour afficher l'heure, on utilise la commande date
	2. Les fichiers commençants par un point ne sont pas affichés par la commande ls, ce sont des fichiers cache
	3. La commande ls se trouve dans le dossier /bin :
		whereis ls
	4. Il n'a pas de page de manuel car il s'agit d'un alias de la commande :
			ls -alF 
	Les autres alias présents sur la machine sont la et des alias pour modifier les couleurs d'affichage. Ces alias sont définis dans le fichier .bashrc qui permet de définir les paramètres du shell à son démarrage
	5. Pour afficher le contenu de /bin :
		ls /bin
	6.  La commande ls .. affiche le contenu du dossier parent du dossier courant
	7. Pour afficher le chemin du dossier courant est :
		pwd
	8. echo 'yo' > plop executé 2 fois donne un fichier nommé plop contenant 'yo' 1 fois (la seconde exécution remplace le contenu du fichier plop par 'yo'
	9. echo 'yo' > plop exécuté 2 fois donne un fichier plop contenant 2 lignes yo (on ajoute à la fin du fichier avec >>)
	10. La commande *file* permet d'afficher le type des fichiers (texte, exécutable etc...)
	11. 	echo 'Hello Toto !' > toto
		ln toto titi
		echo 'Salut' >> toto *( On remarque que les modifications sont aussi faites dans titi)*
	toto et titi pointent sur les mêmes données. Si l'on supprime toto titi reste valide et inversement
	12.  	ln -s titi tutu
	 Ici le lien est symbolique donc tutu pointe vers le fichier titi. La suppression de titi rend invalide le fichier tutu. Les modifications sont vues quelque soit le nom de fichier que l'on utilise
	13. Pour afficher le contenu d'un fichier, on fait :
		cat /var/log/syslog
		CTRL + S *arrête le défilement*
		CTRL + Q *reprend le défilement*
	14. Afficher les 5 premières lignes du fichier :
		head -5 /var/log/syslog
	     Afficher les 15 dernières lignes du fichier :
		tail -15 /var/log/syslog
	     Afficher les lignes 10 à 20 :
		head -20 /var/log/syslog | tail -11 *de 10 à 20 cela fait 11 lignes*
	15. La commande dmesg | less permet d'afficher des informations sur le système d'exploitation et de compatibilité notamment
	16. Afficher le fichier /etc/passwd puis son manuel :
		cat /etc/passwd
		man /etc/passwd
	17. Afficher la 1e colonne triée dans l'ordre inverse :
		cut -d ':' -f1 /etc/passwd | sort -r *( -d indique une coupe par champ, ':' est le séparateur et f1 signifie que l'on prend le 1er champ → 1ere colonne)*
	18. Compter le nombre d'utilisateur sur la machine, connectés ou nom :
	On compte le nombre de lignes dans le fichier /etc/passwd
		cat /etc/passwd | wc -l 
	19. Pour trouver le nombre de pages du manuel contenant le mot conversion, on tape :
		man -k 'conversion' | wc -l
	20. Trouver les fichiers se nommant passwd dans tout le système :
		find / -name 'passwd'
	21. Enregistrer le résultat dans le fichier ~/liste_passwd_files.txt et les erreurs dans le fichier /dev/null :
		find / -name 'passwd'  > ~/liste_passwd_files.txt 2> /dev/null
	22.  Cherche l'alias ll dans le dossier personnel :
		la ~ | grep 'll'
	23.  Trouver le fichier history.log :
		locate history.log
	24. locate ne fonctionne pas sur un fichier qui vient d'être créé car cette fonction s'appuie sur un fichier régulièrement mis à jour des différents fichiers présents sur le système

## Exercice 3 : Découverte de l'éditeur de texte nano (variante vim)

	1. copier un fichier dans le dossier personnel puis l'ouvrir avec nano :
		cp /var/log/syslog ~/log.txt
		cd
		nano log.txt
	2. Remplacer les occurrences de kernel par noyau :
		CTRL + \
		kernel
		noyau
	3.  Mettre les 10 premières lignes du fichier à la fin de celui-ci :
		CTRL + _  *go to*
		0 , 0
		ALT + A    *mark text*
		11 , 0
		CTRL + K *cut text*
		ALT + /      *end of file*
		CTRL + V  *coller*
	4. Annuler cette action :
		ALT + U *x2*
	5. Enregistrer et quitter nano
		CTRL + S
		CTRL + X

## Exercice 4 : Personnalisation du shell

	3. .bashrc est chargé à l'ouverture du shell et permet de définir la configuration du shell comme les couleurs par exemple
	4. on écrit PS1= '\e[35m\A \e[97m- \e[92m\u@\h \e[97m:\e[96m\w\e[97m$'
	le code \e[xxm permet de définir une couleur puis on écrit ce que l'on veut dans cette couleur \x permet d'écrire des éléments spéciaux (chemin, user, date, heure etc...)
