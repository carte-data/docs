# Installation

**Prerequisites:**

* Python >=3.7
* [Node.js](https://nodejs.org/)

To install the Carte CLI, run

```sh
pip install carte-cli
```

if you'd like to use PostgreSQL as a source, you need to install optional dependencies as well. So instead of the above command, you need to run

```sh
pip install carte-cli[postgres]
```

This installs the Carte CLI, which is capable of scaffolding data catalog sites, and extracting metadata from your data sources.
