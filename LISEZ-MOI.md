# Julien 2027 · Projet MkDocs

## Voir le résultat
Décompressez toute l’archive puis ouvrez site/index.html dans votre navigateur. Les quatre pages, les images, la feuille de style et le PDF sont locaux.

## Publier sur WEB1
Depuis la machine physique, ouvrez un terminal dans le dossier julien-mkdocs extrait. Transférez le site statique dans un dossier temporaire dédié à votre compte sur la VM :

    ssh cha-web@192.168.224.3 'mkdir -p ~/julien-mkdocs-web'
    scp -r site/. cha-web@192.168.224.3:~/julien-mkdocs-web/

Si le DocumentRoot de www.chartres.sportludique.fr est /var/www/sportludique-public, publiez avec :

    ssh -t cha-web@192.168.224.3 'sudo mkdir -p /var/www/sportludique-public/campagne && sudo cp -r ~/julien-mkdocs-web/. /var/www/sportludique-public/campagne/'

Adaptez le chemin si le DocumentRoot diffère. Cette commande met à jour les fichiers de même nom dans campagne/. Visitez http://www.chartres.sportludique.fr/campagne/index.html. Si Apache sert index.html comme page par défaut, /campagne/ suffit.

## Modifier le site
Éditez les quatre fichiers Markdown dans docs/. Le titre et l’introduction de chaque page se trouvent entre les lignes --- en tête du fichier. Le thème est dans theme/main.html et docs/assets/campagne.css. Le programme PDF est un document indépendant à actualiser si les engagements changent.

Depuis le dossier contenant mkdocs.yml, sur une machine disposant de Python 3 et du module venv :

    python3 -m venv .venv
    . .venv/bin/activate
    python -m pip install -r requirements.txt
    python -m mkdocs serve

Ouvrez l’adresse indiquée par MkDocs pour prévisualiser vos modifications. Pour produire une nouvelle version à publier :

    python -m mkdocs build --strict

Transférez ensuite le contenu de site/ comme indiqué ci-dessus. La compilation se fait sur votre poste ; Apache sert uniquement les fichiers de site/.
