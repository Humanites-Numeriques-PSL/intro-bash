##################################
Gestion de Chemin des Applications
##################################

L'esprit d'Unix favorise les petites applications qui font une tache, mais
qu'ils la font bien. On peut, donc avoir plein de petits programs qui font des
différentes choses dans notre système. L'organisation de ces programs, et des
procès qui nous permet d'utiliser ces programs est un enjeu important.

Le bash en tant qu'une outil de gestion, nous permet de dissocier
l'organisation de code source des applications et leurs contexts d'utilisation
par l'intermédiaire des fichiers de profils de configuration.

Il y a des différents profils envisageables, par exemple, on peut imaginer
qu'il y aura une suite de procès nécessaire pour le fonctionnement de tout le
système quelque soit l'utilisateur, et qu'il y aura certains procès qui
dependent plutôt à l'abri d'utilisateur. On peut imaginer aussi des procès
spécifiques à l'authentification des utilisateur, ainsi que ceux qu'il
faudrait lancer uniquement après l'authentification, etc, etc.

Disons que vous avez trouvé un projet qui vous intéresse et téléchargé son
executable pour tester ce qu'il fait. Vous lancez l'application, et voilà,
c'est l'amour. A tel point que vous voulez être capable de le lancer à tout
moment. Hélas, il prend trop de temps de revenir à chaque fois au repertoire
de téléchargement. Qu'est-ce qu'il faut faire ?

Alors vous trouverez une telle application pleine d'amour et de mélodrame dans
le repertoire :code:`appli`. Essayons de le rendre accessible par votre
environnement de travail.

- Ouvrez le terminal et venez au repertoire de cours.

- Entrez :code:`~/intro-bash/topics$ ./appli/adieu`, et tapez sur l'entrée.

- Vous devez voir un personnage mathématique avec un message triste

- Au fait des qualités mentionnées dans le message, le personnage reste
  infiniment reproductible (dans des mesures possibles bien sur), donc vous
  voulez être capable d'appeler le personnage à partir de terminal à tout
  moment.

- D'abord on contrôle s'il y a déjà une application qui utilise le même nom
  lors de son appel, via :code:`whereis adieu`

- Vous devez voir :code:`$ adieu:`. Il vaut dire qu'aucune program est appelé
  par le commande :code:`adieu`

- Entrez :code:`pwd` et tapez entrée. Vous devez voir le chemin absolu d'où
  vous êtes dans le système de repertoire. Notez le parce qu'on va l'utiliser
  dans la prochaine étape.

- Ouvrez un nouvel tab dans le terminal avec :code:`ctrl+shift+t`

- Dans le nouvel onglet écrivez le suivant :code:`gedit ~/.bashrc`

- Vous allez voir plein de couleur dans le terminal. Vous êtes en train de
  voir le fichier de configuration avant l'authentification.

- Allez sur le bas de page, et ajoutez les deux lignes suivantes:

  - :code:`# ajoutee par Moi`
  - :code:`export PATH="${PATH:+${PATH}:}CHEMIN_DE_PWD/adieu`

- Enregistrez et fermez le fichier :code:`.bashrc`

- Maintenant entrez :code:`source ~/.bashrc`

- Puis :code:`cd ~`

- Et finalement essayez de lancer le commande :code:`adieu`

Qu'est-ce qu'on a fait ?

On vient de rendre le programme :code:`adieu` accessible à tout les
utilisateurs de la machine et pour cet interpréteur de command. Notre ajout
serait accessible une fois qu'on a fait un nouvel login au système pour les
autres utilisateurs et pour les autres shells, mais il est déjà accessible
pour cet environnement de travail. 

Cela est effectué par le commande :code:`source ~/.bashrc`. Le signe :code:`~`
est un raccourci pour le répertoire :code:`/home/username/`, et le commande
:code:`source`, un synonyme pour le commande :code:`./`, permet d'exécuter les
contenus d'un fichier.
La ligne :code:`# ajoutee par Moi` est une ligne de commentaire, c'est à dire
elle n'a aucune effet dans le déroulement de programme, elle est là uniquement
pour les autres développeur qui vont lire le code.

Le commande :code:`export` nous permet de changer la portée d'un variable.
Dans le cas de bash, il nous permet de déclarer des variables 'environnement.

Je vous invite à chercher ce que la ligne 
:code:`export PATH="${PATH:+${PATH}:}CHEMIN_DE_PWD/adieu`.
