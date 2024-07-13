# Installation d'une IA et d'un chatbot en local
Document rédigé à partir d'une vidéo tutorielle de NetworkChuck : https://www.youtube.com/watch?v=Wjrdr0NU4Sk&t=264s

## Prerequis
- Système : MacOS, Linux, Windows avec WSL
- [Docker](https://www.docker.com/)
- [pyenv](https://github.com/pyenv/pyenv) et installer python 3.10 (13/07/2024)
- Du [café](https://fr.wikipedia.org/wiki/Caf%C3%A9)

## Liste des tâches

### Installer ollama 
#### Installation
- Download pour mac : https://ollama.ai
- Pour Windows (WSL) et Linux : 
```shell
curl -fsSL https://ollama.com/install.sh | sh
```

#### Tester
http://localhost:11434

#### Installer un LLM (llama2)
- `ollama pull llama2` 
- `ollama run llama2`
- Lancer son 1er prompt
- Utiliser `/bye` pour quitter le prompt

#### Monitorer son GPU NVidia (wsl / linux)
- Sur Windows(WSL)/Linux : `watch -n 0.5 nvidia-smi`
- Sur MacOS : Lancer le moniteur d'activités puis `Fenêtre`, `Historique GPU`
<!--  -->
### Installer openWebUI
- Repo github :  https://github.com/open-webui/open-webui
- Commande d'installation en local : 
`docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main`

### Accéder à OpenWebUi
- http://localhost:3000
- Créer son compte (enregistrement local, no worries)
- Jouer

## Installer d'autres modèles
- Liste des modèles mis à disposition : https://ollama.com/library
- Exemple d'installation de codegemma : `ollama pull codegemma`
- (coffee time !)

## Le générateur d'images (Stable Diffusion)
### Installation
- ATTENTION : À date, il faut utiliser la version 3.10 de python. La 3.12 ne fonctionnera pas avec la version actuelle de Stable Diffusion
- Télécharger `wget -q https://raw.githubusercontent.com/AUTOMATIC1111/stable-diffusion-webui/master/webui.sh`
- Lancer le script d'installation
```shell
chmod +x webui.sh
./webui.sh --listen --api
```
Les switchs `--listen` et `--api` servent à autoriser l'utilisation de l'API de Stable Diffusion (à utiliser pour l'intégration dans OpenWeb UI, ci-après)
- Reprendre du café. C'est un peu long...
- Tester : http://localhost:7860

### Intégration dans OpenWeb UI
- Dans la page des **Admin Settings** d'OpenWeb UI, aller dans **Images** et saisir l'adresse `http://host.docker.internal:7860` ou `http://localhost:7860`. Cela dépend si vous avez lancé OpenWeb UI dans une instance docker (auquel cas, l'instance docker doit aller sur le host et non pas s'appeler elle-même) ou non
- Cliquer sur le bouton juste à coté du champ contenant l'URL afin de vérifier la connexion
- Autoriser la fonctionnalité expérimentale de génération d'images

