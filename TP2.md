# COMPTE RENDU  TP2

### Exercice 1. Variables d’environnement 

1.  la commande  **printenv PATH**  permet  de trouver  les dossiers bash des commandes tapées par l'utilisateur , d'ou le resultat suivant : <br>
 **/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin :/bin:/usr/games:/usr/local/games:/snap/bin**
   
2. la variable  d’environnement **HOME** permet à la commande cd tapée sans argument de nous ramener dans notre répertoire personnel.

3. la variable *LANG*  determine la langue que les logiciels utilisent pour communiquer avec l'utilisateur. comme nous sommes  des utilisateur francais  on retrouve  la valeur *fr_FR.UTF-8*. <br>
la variable **PWD**  contient le chemin du repertoire  courant qui est **/home/user** <br>
la variable **OLDPWD**  contient le chemin  du repertoire precedent qui est **/home** <br>
la variable **SHELL** contient  l'emplacement de l'interpréteur bash , obtient **/bin/bash** <br>
la variable **_**  variable qui contient l'emplacement de la commande **printenv** , on obtient **/user/bin/printenv**.

4. on a creé la variable MY_VAR avec la commande **MY_VAR="faby"** puis on a affiché le contenu avec **echo $My_VAR** , on obtient faby donc cette variable existe vraiment.

5. La commande bash n'affiche rien mais ouvre un interpreteur bash.
Oui, la variable My_VAR n'existe plus dans la session bash car elle est associée localement la session precedente. pour sortir de la session bash on fait un exit .

6. La commande **export My_VAR="faby"** permet de declarer MY_VAR comme une variable d'environnement et deslors cette vaiable est existe aussi dans la session  bash  on  y accede avec la  commande *printenv My_VAR*.

7. en créant la variable NOMS suivant la commande **export NOMS="TAGNE WU"** et en affichant NOMS avec la commande **printenv NOMS**, on a bien le contenu saisit des le depart à savoir  TAGNE WU.

8. La commande **echo "Bonjour à vous deux, $NOMS!"**  aﬀiche "Bonjour à vous deux, binôme1 binôme2!" (où binôme1 et binôme2 sont nos deux noms) , on a le resultat: Bonjour à vous deux, TAGNE WU!

9. La commande **unset** supprime la variable donc pas d'espace mémoire pour la variable, alors que une variable peut exister mais n'a pas de contenu d'où il ya une allocation memoire  pour cette variable .

10. la commande permettant d'écrire ceci: **echo '$HOME = '"$HOME"** qui nous donne le résultat suivant: $HOME =/home/user.

## Programmation Bash

Pour ajourter le chemin vers script à notre PATH de manière permanente, on utilise la commande**sudo vim /etc/environement** pour le modifier. On ajouter **/home/user/script:**. <br>
**PATH="/HOME/user/scrip:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"**

### Exercice 2. Contrôle de mot de passe

<html>#!/bin/bash <br>

<html>PASSWORD="ilovelinux" <br>
<html>read -s -p 'Rentre un mdp: ' PASSWORD_TEST <br>
<html>if [ "$PASSWORD_TEST" = "$PASSWORD" ]; then <br>
<html>    echo -e "\nMot de passe valide" <br>
<html>else <br>
<html>    echo -e "\nMot de passe invalide" <br>
<html>fi <br>
   
   ### Exercice 3. Expressions rationnelles 

<html>#!/bin/bash <br>

<html>function is_number() <br>
<html>{ <br>
<html>re='^[+-]?[0-9]+([.][0-9]+)?$' <br>
<html>if ! [[ $1 =~ $re ]] ; then <br>
<html>return 1 <br>
<html>else <br>
<html>return 0 <br>
<html>fi <br>
<html>} <br>
<html> <br>
<html>if [ is_number ]; then <br>
<html>    echo -e "\nCe paramètre est un nombre réel" <br>
<html>else <br>
<html>    echo -e "\nsaisi incorrect" <br>
<html>fi <br>



### Exercice 4. Contrôle d’utilisateur

<html>#!/bin/bash <br>
<html>
<html>nom_utilisateur=$(whoami) <br>
<html>
<html>if id -u $1 >/dev/null 2>&1; then <br>
<html>        echo -e "\nUtilisateur existe!" <br>
<html>else
<html>        echo -e "\nUtilisation : $0 $nom_utilisateur" <br>
<html>fi <br>



### Exercice 5. Factorielle

<html>#!/bin/bash <br>
<html>fact=1 <br>
<html>for i in $(seq 1 $1) <br>
<html>do  <br>
<html>    fact=$[fact*i] <br>
<html>done <br>
<html>echo -e "\nFactorielle de $1= $fact" 



### Exercice 6. Le juste prix

<html>#!/bin/bash <br>

<html>RAM=$[$RANDOM%1000 | bc] <br>

<html>echo -e "\nNombre aléatoire est $RAM" <br>

<html>if [[ $1 > $RAM ]]; then <br>
<html>    echo -e "\nC’est moins !" <br>
<html>elif [[ $1 < $RAM ]]; then <br>
<html>    echo -e "\nC’est plus !" <br>
<html>else <br>
<html>    echo -e "Gagné !" <br>
<html>fi 
