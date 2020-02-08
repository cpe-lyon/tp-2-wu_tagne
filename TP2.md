### COMPTE RENDU  TP1

## Exercice 1. Variables d’environnement 

1.  la commande  * printenv PATH*  permet  de trouver  les dossiers bash des commandes tapées par l’utilisateur , d'ou le resultat suivant :
 */usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin :/bin:/usr/games:/usr/local/games:/snap/bin*
   
2. la variable  d’environnement *HOME* permet à la commande cd tapée sans argument de nous ramener dans notre répertoire personnel.

3. la variable *LANG*  determine la langue  que  les logiciels utilisent pour  communiquer  avec l'utilisateur. comme nous sommes  des utilisateur francais  on retrouve  la valeur *fr_FR.UTF-8*.
la variable *PWD*  contient le chemin du repertoire  courant qui est */home/user*
la variable *OLDPWD*  contient le chemin  du repertoire precedent qui est */home*
la variable *SHELL* contient  l'emplacement de l'interpréteur bash , obtient */bin/bash*
la variable *_*  variable qui contient l'emplacement de la commande *printenv* , on obtient */user/bin/printenv*.

4. on a creé la variable My_VAR avec la commande *MY_VAR="faby" * puis on a affiché le contenu avec *echo $My_VAR* , on obtient faby donc cette variable existe vraiment.

5. La commande bash n'affiche rien mais ouvre un interpreteur bash.
Oui, la variable My_VAR n'existe plus dans la session bash car elle est associée localement la session precedente. pour sortir de la session bash on fait un exit .

6. La commande *export My_VAR="faby" * permet de declarer MY_VAR comme une variable d'environnement et deslors cette vaiable est existe aussi dans la session  bash  on  y accede avec la  commande *printenv My_VAR*.

7. en créant la variable NOMS suivant la commande *export NOMS="TAGNE WU"* et en affichant NOMS avec la commande *printenv NOMS*, on a bien le contenu saisit des le depart à savoir  TAGNE WU.

8. La commande *echo "Bonjour à vous deux, $NOMS!"*  aﬀiche "Bonjour à vous deux, binôme1 binôme2!" (où binôme1 et binôme2 sont nos deux noms) , on a le resultat: Bonjour à vous deux, TAGNE WU!

9. La commande *unset* supprime la variable donc pas d'espace mémoire pour la variable, alors que une variable peut exister mais n'a pas de contenu d'où il ya une allocation memoire  pour cette variable .

10. la commande permettant d'écrire ceci: *echo '$HOME = '"$HOME" * qui nous donne le résultat suivant: $HOME =/home/user.

## Programmation Bash

Pour ajourter le chemin vers script à notre PATH de manière permanente, on utilise la commande *sudo vim /etc/environement* pour le modifier. On ajouter */home/user/script:*. <br>
PATH="/HOME/user/scrip:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"

#Exercice 2. Contrôle de mot de passe

<html>#!/bin/bash

<html>PASSWORD="ilovelinux"
<html>read -s -p 'Rentre un mdp: ' PASSWORD_TEST
<html>if [ "$PASSWORD_TEST" = "$PASSWORD" ]; then
<html>    echo -e "\nMot de passe valide"
<html>else
<html>    echo -e "\nMot de passe invalide"
<html>fi




