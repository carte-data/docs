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
pip install -r requirements.txt
```

This will install the necessary dependencies to serve the front end locally.

The frontend comes with dummy data prepopulated, so you can play with the site right away. To start development mode, run
```sh
./scripts/build.sh
mkdocs serve
```
then view your site at [http://localhost:8000](http://localhost:8000).

If you don't want sample data to be included, you can create the site using
```sh
carte new data-catalog --no-sample
```

## Details

The front end is an MkDocs based static site set up with the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme, with some customisations.

The `build.sh` script you ran is for taking the `datasets` folder (which contains the structured Markdown files), and flattening them into the `content` folder as pure Markdown files (no structured front matter). This enables Material for MkDocs to index the fields of the datasets, and make everything searchable.
