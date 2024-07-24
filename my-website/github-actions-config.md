# Configuration de l'intégration continue (CI) avec GitHub Actions

## Étapes de Configuration

### 1. Création des Fichiers de Workflow

Commencez par créer un fichier de workflow GitHub Actions :

1. Dans votre dépôt GitHub, naviguez vers le répertoire `.github/workflows`.
2. Créez un nouveau fichier YAML, par exemple `build-docusaurus.yml`.
3. Créez un deuxième fichier YAML, par exemple `deploy-docusaurus.yml`.

### 2. Configuration du Workflow

Ajoutez la configuration suivante dans le fichier `build-docusaurus.yml` :

```yaml
name: Build and Deploy Docusaurus site

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install
        working-directory: ./my-website

      - name: Build Docusaurus site
        run: npm run build
        working-directory: ./my-website

      - name: Upload built site to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./my-website/build
```

Ajoutez la configuration suivante dans le fichier `deploy-docusaurus.yml` :

```yaml
name: Deploy Docusaurus site

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install
        working-directory: ./my-website

      - name: Build Docusaurus site
        run: npm run build
        working-directory: ./my-website

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./my-website/build
```

