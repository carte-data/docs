# Getting started

You can create a new data catalog folder with the CLI by running

```sh
carte new data-catalog
```
`data-catalog` could be anything that you'd like to name your data catalog.

This clones the latest version of the Carte front end to the `data-catalog` (or the name you provided) folder within the current one, and applies a few project-specific settings.
Then you need to install the front end's dependencies by going into the catalog's folder:
```sh
cd data-catalog
```

and then running

```sh
npm install
```

This will install the necessary dependencies to serve the front end locally.

The frontend comes with dummy data prepopulated, so you can play with the site right away. To start development mode, run
```sh
npm run dev
```
then view your site at [http://localhost:3000](http://localhost:3000).

If you don't want sample data to be included, you can create the site using
```sh
carte new data-catalog --no-sample
```
