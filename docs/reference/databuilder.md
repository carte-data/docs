# Using Amundsen Databuilder extractors

You can use any extractor available in the [Amundsen Databuilder](https://github.com/amundsen-io/amundsendatabuilder) library, since Carte builds upon the efforts of its authors and is compatible with it. However, you have to configure the Amundsen specific extractors (those that Carte doesn't support) in code.

For this, you can write a normal Databuilder Job, with a Carte loader (and any transformations if needed). You can import the loader class from `carte_cli.loader.carte_loader` like so:

 ```python
 from carte_cli.loader.carte_loader import CarteLoader
 ```
 
 The Carte loader is responsible for saving dataset metadata to files and merging extsting descriptions with new metadata. You'll have to specify the output path (since we lose that by not using the Carte CLI). For this, use the `loader.carte.tables_output_path` key in the Databuilder config.
