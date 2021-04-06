# CLI Command reference

The arguments to the CLI commands can be found by running `carte -h`. At this point new commands are added fast enough so that only the core ones are documented here.

## extract

The first (required) argument is the path to the extraction config file (detailed in [the Extracting metadata section](/getting_started/extracting_metadata/)).

There's a second, optional option with flag `-o`, which sets the output directory. To perform extraction with the current folder containing the `extract.config.yml` file and pulling the results into the `datasets` folder, you would run

```sh
carte extract extract.config.yml -o datasets
```

## new

This command scaffolds a new Carte catalog site (it clones [the frontend repo](https://github.com/carte-data/carte-frontend) and sets up a few things).

The only required argument is the name of the site. This creates a folder with the same name within the current directory.

There are two optional flags:

1. `--no-admin` – doesn't scaffold a Netlify CMS subsite to edit your dataset descriptions. This means any changes have to be made through Git directly, or another CMS system.
2. `--no-sample` - this deletes the sample datasets that are part of the new site. Use this if this is not your first time setting up a Carte site.


## flatten

This takes a folder with (technically) Markdown files, that have a structured YAML front matter, and outputs a flattened version, that's just Markdown (and special MkDocs syntax for adding HTML classes to Markdown elements). This is helpful, since MkDocs doesn't search the front matter by default, so only the dataset descriptions would be searchable (and not column names for instance).

For this command, the first argument is the input folder (that you specified with the `-o` flag during extraction), and the second is the output folder (`content`, if you're using the Carte front end). If you'd like to customise the HTML classes and the structure of the resulting files, you can add a `--template` flag, with the path of a template file specified afterwards. This is a Jinja2 template that gets the dataset object passed to it. You won't need to specify the `--template` option in most cases, since the default template displays all the information about datasets. However, if you'd like to change this, you can use the [default template](https://raw.githubusercontent.com/carte-data/carte/main/carte_cli/utils/templates/dataset_flattened.md) as a starting point.
