# Deploying your site

When deploying your site, you need to

1. Flatten the datasets in the `datasets` folder into normal Markdown so that it's searchable. This is done by the `carte flatten datasets content` command, where the first argument (`datasets`) is the source folder and the second (`content`) is the destination
2. Build the site as normal with MkDocs using the `mkdocs build` command. This puts the HTML output in the `site` folder. This what you deploy then to a static site hosting provider, such as GitHub Pages, Netlify, or Surge.

Both of these things are done by the `scripts/build.sh` script (it just contains the above two commands actually). It's a convenience feature for having just one command to execute on the CI when building the catalog.
