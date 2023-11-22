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
# Unitpackage API

A collection of unitpackages can be loaded with the [unitpackage API](https://echemdb.github.io/unitpackage/usage/local_collection.html) to browse, explore, modify or visualize the entries. A detailed description and usage examples can be found in the [unitpackage documentation](https://echemdb.github.io/unitpackage/usage/unitpackage_usage.html). Here we collect the unitpackages created with this introductory tutorial.

```{code-cell} ipython3
from unitpackage.collection import Collection
from unitpackage.local import collect_datapackages

db = Collection(collect_datapackages('../files/data/generated'))
db
```

IF units were provided to the fields, you can simply transform the units and created a plot with these units.

 ```{code-cell} ipython3
entry = db['data']
entry.rescale({'t':'ms', 'U':'V'}).plot('t', 'U')
```

Other metadata as accessible as attributes from each package.

```{code-cell} ipython3
entry.research_question
```
