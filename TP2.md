# COMPTE RENDU  TP2

### Exercice 1. Variables d’environnement 

1.  la commande  **printenv PATH**  permet  de trouver  les dossiers bash des commandes tapées par l'utilisateur , d'ou le resultat suivant : <br>
 **/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin :/bin:/usr/games:/usr/local/games:/snap/bin**
   
2. la variable  d'environnement **HOME** permet à la commande cd tapée sans argument de nous ramener dans notre répertoire personnel.

3. la variable *LANG*  determine la langue que les logiciels utilisent pour communiquer avec l'utilisateur. comme nous sommes  des utilisateur francais  on retrouve  la valeur *fr_FR.UTF-8*. <br>
la variable **PWD**  contient le chemin du repertoire  courant qui est **/home/user** <br>
la variable **OLDPWD**  contient le chemin  du repertoire precedent qui est **/home** <br>
la variable **SHELL** contient  l'emplacement de l'interpréteur bash , obtient **/bin/bash** <br>
la variable **_**  variable qui contient l'emplacement de la commande **printenv** , on obtient **/user/bin/printenv**.

4. on a creé la variable MY_VAR avec la commande `MY_VAR="faby"` puis on a affiché le contenu avec `echo $My_VAR` , on obtient faby donc cette variable existe vraiment.

5. La commande bash n'affiche rien mais ouvre un interpreteur bash.
Oui, la variable My_VAR n'existe plus dans la session bash car elle est associée localement la session precedente. pour sortir de la session bash on fait un exit .

6. La commande `export My_VAR="faby"` permet de declarer MY_VAR comme une variable d'environnement et deslors cette vaiable est existe aussi dans la session  bash  on  y accede avec la  commande `printenv My_VAR`.

7. en créant la variable NOMS suivant la commande `export NOMS="TAGNE WU"` et en affichant NOMS avec la commande `printenv NOMS`, on a bien le contenu saisit des le depart à savoir  TAGNE WU.

8. La commande `echo "Bonjour à vous deux, $NOMS!"`  aﬀiche  __"Bonjour à vous deux, binôme1 binôme2!"__ (où binôme1 et binôme2 sont nos deux noms) , on a le resultat: Bonjour à vous deux, TAGNE WU!

9. La commande `unset` supprime la variable donc pas d'espace mémoire pour la variable, alors que une variable peut exister mais n'a pas de contenu d'où il ya une allocation memoire  pour cette variable .

10. la commande permettant d'écrire ceci: `echo '$HOME = '"$HOME"` qui nous donne le résultat suivant: $HOME =/home/user.

## Programmation Bash

Pour ajourter le chemin vers script à notre PATH de manière permanente, on utilise la commande `sudo vim /etc/environement` pour le modifier. On ajouter **/home/user/script:**. <br>
**PATH="/HOME/user/scrip:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"**

### Exercice 2. Contrôle de mot de passe
```shell
#!/bin/bash <br>

PASSWORD="ilovelinux" <br>
read -s -p 'Rentre un mdp: ' PASSWORD_TEST # -s -p pour que la saisie soit cachée et que le message saisi après soit affiché <br>
if [ "$PASSWORD_TEST" = "$PASSWORD" ]; then <br>
    echo -e "\nMot de passe valide" <br>
else <br>
    echo -e "\nMot de passe invalide" #Le -e du echo permet d'activer les retours à la ligne via \n. On n'oublie pas les $ des variables
fi <br>
   ```
   ### Exercice 3. Expressions rationnelles 
```shell
#!/bin/bash

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
return 1
else
return 0
fi
}

is_number $1

if [[ $? == 0 ]]; then
    echo -e "\nCe paramètre est un nombre réel"
else
    echo -e "\nsaisi incorrect"
fi
```


### Exercice 4. Contrôle d’utilisateur
```
<html>#!/bin/bash <br>
<html>
<html>nom_du_script=$0  # on recupère le nom du  script <br>
<html>nom_utilisateur=$1 # on recupère le premier paramètre  <br>
<html>
<html>if  [ -z "$nom_utilisateur" ]; then #  on verifie  si  la chaine de caractère est vide <br>
<html>echo "Utilisation : $nom_du_script nom_utilisateur"<br>
<html>exit<br> 
<html>fi <br>
<html>if id -u $1 >/dev/null 2>&1; then  # on verifie si l'utilisateur existe  ou pas <br>
<html>        echo -e "\nUtilisateur existe!" <br>
<html>else
<html>        echo -e "\nUtilisateur  n'existe pas! " <br>
<html>fi <br>
```


### Exercice 5. Factorielle
```
<html>#!/bin/bash <br>
<html>fact=1 <br>
<html>for i in $(seq 1 $1)  # on recupère les nombres compris entre 1 et le nombre dont on veux le factoriel <br>
<html>do  <br>
<html>    fact=$[fact*i]  # on fait une multiplication recursive  jusqu'à ce que on arrive  sur le nombre donc on veut le factorielle <br>
<html>done <br>
<html>echo -e "\nFactorielle de $1= $fact" 
```


### Exercice 6. Le juste prix
```
<html>#!/bin/bash <br>

<html>RAM=$[$RANDOM%1000 | bc] # ici on genère un nombre compris entre  1 et 1000 en utilisant bc qui se charge de faire la géneartion du nombre <br>

<html>echo -e "\nNombre aléatoire est $RAM" <br>
<html>#nombre=0 on donne une valeur qui ne pourra pas etre le nombre généré <br>
<html>#while [ $RAM -ne $nombre ]  on compare  le nombre genéré et le nombre tapé <br>
<html>#do<br>
<html>read -p ' saisissez un nombre :' nombre # on demande à l'utilisateur d'entrer un nombre  <br
<html>if [ $nombre -gt $RAM ]; then <br> 
<html>    echo -e "\nC’est moins !" <br>
<html>elif [ $nombre -lt $RAM ]; then <br>
<html>    echo -e "\nC’est plus !" <br>
<html>else <br>
<html>    echo -e "Gagné !" <br>
<html>fi<br>
<html>#done
```


### Exercice 7. Statistiques
```
<html>#!/bin/bash<br>

<html>checkInt(){<br>
<html>       expr $1 + 0 &>/dev/null<br>
<html>     [ $? -ne 0 ] && { echo "parametre $1 doit etre entier!";exit 1; }<br>
<html> }<br>
<html> checkInt1(){<br>
<html>         tmp=`echo $1 |sed 's/[0-9]//g'`<br>
<html>         [ -n "${tmp}" ]&& { echo "parametre $1 doit etre entier!";exit 1; }<br>
<html> }<br>

<html> read -p 'saisiez 3 entiers entre -100 et 100(séparez avec espase)' a b c <br>

<html> min=$a<br>
<html> middle=$b<br>
<html> max=$c<br>
<html> tmp=0<br>

<html> checkInt $a<br>
<html> checkInt1 $b<br>
<html> checkInt1 $c<br>

<html> if [[ $min > $middle ]]; then<br>
<html> 	tmp=$min;<br>
<html> 	min=$middle;<br>
<html> 	middle=$tmp;<br>
<html> fi<br>
<html> if [[ $min > $max ]]; then<br>
<html> 	tmp=$min;<br>
<html> 	min=$max;<br>
<html> 	max=$tmp;<br>
<html> fi<br>
<html> if [[ $middle > $max ]]; then<br>
<html> 	tmp=$middle;<br>
<html> 	middle=$max;<br>
<html> 	max=$tmp;<br>
<html> fi<br>
<html> echo -e "\nLe max est $max, le min est $min, la moyenne est $(( ($a + $b + $c) / 3))"<br>
```
