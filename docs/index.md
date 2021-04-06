# Home

Carte is a **static site generator** for documenting your organisation's data. It lets you automatically extract metadata from your data sources (SQL databases, AWS, BigQuery, etc.) and document them as text files. It then provides you with a searchable, easy-to-use statically generated front end for navigating your datasets and helping data discovery in your organisation.

[Live demo](https://demo.cartedata.com){ .md-button }

![Carte front end](/assets/images/carte_screenshot.png)

## Who is this for?
Collecting useful data is not enough. You also have to document its structure and meaning somewhere so that it's visible to others. Otherwise people end up collecting or transforming the same data multiple times, or constantly nag your data scientists about the meaning of that `ltv_cust_year` column.
Carte is meant for small to medium sized companies who don't have the time to build a data catalog, and the resources to maintain several microservices just for this task. 
Every major tech organisation creates a custom data catalog for themselves (see Uber, Spotify, Linkedin, Lyft), so why not have one that's tailored for smaller amounts of data and has a lightweight tech stack? Enter Carte.

## How does it work?
Carte relies on simple YAML + Markdown *descriptor* files to document your data's shape. These can have descriptions for datasets, their columns, and also various metadata. Descriptions are not imported from the data sources, since the different sources provide different facilities (if any) for describing tables or datasets. Carte instead lets you write descriptions for your data, and thus separate the **description layer** from the **data layer**.

The YAML descriptors are usually stored in a Git repo, which means it's easy to see how your data changes over time, just by looking at the commits touching a given descriptor. You can see when a field was deprecated, or who edited a given column.
To facilitate this workflow, Carte has two components:

1. [**Carte CLI**](/extraction) – A Python library for extracting metadata from your data sources (SQL databases, AWS, BigQuery, etc.) and creating structure descriptor files. During extraction, the descriptions of the previous extract are preserved, so only the data's shape can change (columns and datasets can only be added or deleted, not changed).
2. [**Carte frontend**](/frontend) – A front end that takes the extracted metadata, and generates a searchable, easy-to-use static site that documents your data. This site is only a directory of HTML and JavaScript files, so it can be deployed easily on GitHub Pages, Netlify, AWS S3, you name it.

To edit the descriptions of your datasets, you can either edit them in the repo and push it back up, or alternatively there's an optional component to simplify this:

- [**Netlify CMS**](/admin) – A flat-file CMS that lets you edit your dataset's descriptions on a UI and commit it back to the source repo. Carte includes Netlify CMS with minimum configuration to enable easy editing of dataset and column descriptions for less technical users as well.
