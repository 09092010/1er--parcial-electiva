name: Publicar Pagina a Surge.sh

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Clona el repositorio
        uses: actions/checkout@v3

      - name: configura nodejs  
        uses: actions/setup-node@v3
        with:
            node-version: '20' 

      - name: Instala Surge       
        run: npm install --global surge

      - name: Publicar pagina
        run: surge --project ./ --domain ${{ secrets.SURGE_DOMAIN }} --token ${{ secrets.SURGE_API_KEY }}
