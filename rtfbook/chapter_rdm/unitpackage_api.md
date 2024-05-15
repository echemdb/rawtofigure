---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
# Create and Browse Unitpackage's

The unitpackage API can be used to [create](https://echemdb.github.io/unitpackage/usage/load_and_save.html#create-local-unitpackages) unitpackages or [browse](https://echemdb.github.io/unitpackage/usage/local_collection.html) such packages. The unitpackage is based on the [frictionless framework](https://framework.frictionlessdata.io/), which has been adapted to meet the requirements to annotate scientific data.
Read more in the [unitpackage documentation](https://echemdb.github.io/unitpackage/usage/unitpackage.html).

## Create unitpackages

The creation of unitpackages with the unitpackage API is described in the [documentation](https://echemdb.github.io/unitpackage/usage/load_and_save.html). They can be created from local CSV files but also directly from pandas dataframes.

The following example illustrates how a unitpackage can be created from a CSV and YAML (containing information on the column names in the CSV and additional metadata)

```{code-cell} ipython3
from unitpackage.entry import Entry
import yaml

with open("../files/data/data.csv.meta.yaml", "rb") as f:
    metadata = yaml.load(f, Loader=yaml.SafeLoader)

fields = metadata["figure description"]["fields"]

entry = Entry.from_csv(csvname="../files/data/data.csv", metadata=metadata, fields=fields)
entry.save(outdir="../generated/files/data/generated/")
```

In case your original data is not standard CSV, we recommend writing a loader that creates a pandas dataframe, which can be stored along with measured metadata as unitpackage, as described in the unitpackage documentation on how to [load unitpackages](https://echemdb.github.io/unitpackage/usage/load_and_save.html#load-entries).
A modular loader and converter is currently developed in [echemdb-converters](https://echemdb.github.io/echemdb-converters/).

## Exploring data

A collection of unitpackages can be loaded with the [unitpackage API](https://echemdb.github.io/unitpackage/usage/local_collection.html) to browse, explore, modify or visualize the entries. A detailed description and usage examples can be found in the [unitpackage documentation](https://echemdb.github.io/unitpackage/usage/unitpackage_usage.html).
Here we collect a demo unitpackage.

```{code-cell} ipython3
from unitpackage.collection import Collection

db = Collection.from_local('../files/data')
db
```

If units were provided to the fields, you can simply transform the units and create a plot with these units.

 ```{code-cell} ipython3
entry = db['data_demo']
entry.rescale({'t':'ms', 'U':'V'}).plot('t', 'U')
```

Other metadata as accessible as attributes from each package.

```{code-cell} ipython3
entry.research_question
```
