## DSI-REPO-NG

Ce projet permet d'assembler des composants (cookbooks) afin de créer un service. Il n'est pas recommander d'utiliser ce projet pour le développement de cookbook "unitaire".

### Installation de l'environnement

Suivant le système d'exploitation que vous utilisez, la méthode d'installation des pré-requis peut différer. Ici, nous documenterons l'installation des pré-requis uniquement pour le système d'exploitation Ubuntu 14.04.

#### Pré-requis

Dans un premier temps, il faut télécharger les softwares suivants et les installer sur votre système.

* Vagrant
  * vagrant-hostmanager : ```vagrant plugin install vagrant-hostmanager```
  * vagrant-berkshelf : ```vagrant plugin install vagrant-berkshelf```
* Virtualbox
* Chefdk

#### Procédure d'installation

Une fois chefdk installé, il ne faut pas oublier de rajouter la ligne suivante dans votre .bashrc et redémarrer votre shell. Ceci fixera l'utilisation du ruby embarqué dans la distribution chefdk.

````
eval "$(chef shell-init bash)"
````

Les commandes suivantes doivent être utilisées avec votre compte utilisateur (non root).

````
git clone https://github.com/dsi-infrastructure/dsi-repo-ng.git
cd dsi-repo-ng
git submodule init
git submodule sync
git submodule update
bundler install
sudo gem uninstall -i /opt/chefdk/embedded/lib/ruby/gems/2.1.0 json
librarian-chef install --verbose
````

La récupération des cookbooks risque de prendre un moment suivant les débits de votre connexion internet. 


### Contribuer à ce projet

Pour contribuer à ce projet, il faut le forker sur Github.

Les règles suivantes sont à appliquer :

* La branche "master" est la branche de production et il est **interdit** d'écrire sur celle-ci ;
* La branche "develop" est la branche de développement et il est **interdit** d'écrire sur celle-ci ;
* **Chaque fonctionnalité** doivent être **décrite sur la page Issue de Github** avant d'être implémenté ;
* **Chaque fonctionnalité** doivent faire l'objet d'une **branche spécifique** hérité de la branche "develop" ;
* Un pull request concerne votre branche spécifique et la branche "develop" **upstream uniquement** ;
* Un commentaire commence par une **MAJUSCULE** et se termine par un
  point **.** ;
* Vous devez **intégrer les modifications** de la branche "develop" **avant** un pull request ;
* Vous devez **obligatoirement intégrer l'environnement** que vous avez utilisé **dans le fichier Vagrantfile** (ce fichier contiendra la totalité des environnements de l'équipe afin de simplifier la revue et la compréhension des configurations par tous) ;
