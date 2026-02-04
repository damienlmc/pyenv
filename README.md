# pyenv (fonction shell Homebrew)

> ⚠️ **Important**  
> Ce projet **n’utilise PAS l’outil officiel `pyenv`**.  
> Il s’agit d’une **fonction shell personnalisée** permettant de créer et d’activer rapidement un environnement virtuel Python à partir d’une version installée via **Homebrew**.

---

## 🎯 Objectif

Ce script a pour objectif de simplifier et automatiser la création d’un environnement virtuel Python.

Avec une seule commande, il permet de :
- sélectionner une version précise de Python installée via Homebrew
- créer un environnement virtuel (`venv`)
- activer automatiquement cet environnement
- créer un dossier de travail dédié au projet
- se positionner directement dans ce dossier

L’objectif principal est de **réduire plusieurs commandes manuelles à une seule commande**.

---

## 📦 Prérequis

- macOS
- Homebrew installé
- Python installé via Homebrew

Exemple :


brew install python@3.11


## Descriptif de fonctionnement du script

```pyenv [version_python] [nom_venv]```

## Script 

À ajouter dans ~/.zshrc ou ~/.bashrc :

```
function pyenv() {
    
    if [ "$1" = "" ] || [ "$2" = "" ]; then
        if [ "$1" = "-a" ] || [ "$1" = "-d"  ] || [ "$1" = "-h" ] || [ "$1" = "-l" ]; then else
                echo "Usage: \n pyenv est un alias pour créer un environnement avec un dossier de python déja installé avec brew pyenv [version de python] [dossier de la venv python] \n
        Pour avoir le path utiliser la commande brew --prefix [version de python]
        "
        fi
    else
        /opt/homebrew/opt/python@$1/bin/python$1 -m venv ~/$2
        source ~/$2/bin/activate
        cd ~/$2
        mkdir $2-data
        cd $2-data
    fi
    if [ "$1" = "-a" ]; then
        source ./bin/activate
        cd *-data
    fi
    if [ "$1" = "-d" ]; then
        deactivate
        cd
    fi
    if [ "$1" = "-l" ]; then
       brew list | grep python@
    fi
    if [ "$1" = "-h" ]; then
       echo "\n -a Pour activer la venv
             \n -d Pour désactiver la venv
             \n -l Pour lister les versions de python disponible"
    fi
}
alias pyenv=pyenv

