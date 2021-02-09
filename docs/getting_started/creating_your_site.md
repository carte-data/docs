# Getting started

First, create a new repo with [Carte frontend](https://github.com/carte-data/carte-frontend) as the template. For this, go to the frontend repo, and click the green `Use this template` button. This repo will house the metadata for your data catalog, as well as the front end. Name the new repo however you like. In this example it'll be `data-catalog`. Once it's created, clone your repo locally and enter the directory:
```sh
git clone <data catalog repo URL>
cd data-catalog
```

If you don't have Node.js installed, [install it](https://nodejs.org/). Then install the frontend's dependencies by running `npm install`.

The frontend comes with dummy data prepopulated, so you can play with the site right away. To start development mode, run
```sh
npm run dev
```
then view your site at [http://localhost:3000](http://localhost:3000).
