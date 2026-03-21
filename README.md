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

![pyenv](https://github.com/user-attachments/assets/e7522fa0-2dc7-4df7-a858-995e0a9b7478)


---

## 📦 Prérequis

- macOS Windows et Linux
- Homebrew installé
- Python installé via Homebrew

Exemple :


brew install python@3.11


## Pour instaler brew 

https://brew.sh/

Après installer ```brew install python@3.10 python@3.11 python@3.12 python@3.13 python@3.14``` 

## Descriptif de fonctionnement du script

```pyenv [version_python] [nom_venv]```

## Script

À ajouter dans ~/.zshrc ou ~/.bashrc :

```
function pyenv() {
if [ "$1" = "-a" ]; then
  source ./bin/activate
  cd *-data
elif [ "$1" = "-d" ]; then
  deactivate
  cd
elif [ "$1" = "-h" ]; then
  echo "-a Pour activer la venv"
  echo "-d Pour désactiver la venv"
  echo "-l Pour lister les versions de python disponible"
elif [ "$1" = "-l" ]; then
  brew list | grep python@ | cut -d@ -f2 
elif [ -z "$1" ] || [ -z "$2" ]; then
  echo "Usage: pyenv est un alias pour créer un environnement avec un dossier de python déja installé avec brew pyenv [version de python] [dossier de la venv python]"
else
  
  ################ Script LINUX ################
  /home/linuxbrew/.linuxbrew/opt/python@$1/bin/python$1 -m venv ./$2
  ################ Script WINDOWS WSL #########
  #/home/linuxbrew/.linuxbrew/opt/python@$1/bin/python$1 -m venv ./$2
  ################ Script OSX #################
  #/opt/homebrew/opt/python@$1/bin/python$1 -m venv ./$2

  source ./$2/bin/activate
  cd ./$2
  mkdir $2-data
  cd $2-data
fi
}
alias pyenv=pyenv
```


