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
# Metadata

In principle each measurement file should be annotated by metadata including for example a description of the data itself (units, origin of values), the experimental conditions (sample, instruments, environment parameters, ...), and possibly also non specific metadata (users, project, ...).

Preferably such information is stored in a template, where for each experiment only a limited number of values are modified.
For example, you could perform a series of measurements at different temperatures.

While metadata can be retrieved from different sources such as in another repository or your electronic lab notebook,
a rather accessible approach is to store the template as YAML in your local file system.
An extensive example of such a YAML template can be found
[here](https://github.com/echemdb/metadata-schema/blob/main/examples/file_schemas/autotag.yaml).

In the workflow to [create the unitpackage](unitpackage_creation.md), the YAML file can be loaded as Python dictionary.

```{code-cell} ipython3
import yaml

metadata = yaml.load('../data/files/data.csv.meta.yaml', Loader=yaml.SafeLoader)
```

This approach works perfectly fine when you export your newly acquired data after each experiment manually or in a workflow as unitpackage.
However, in case you do not have the means to do so, for example when you work with proprietary software
or a workstation which does not provide you with a programmable interface,
you should nevertheless store metadata along with your file.
Doing so by creating a new file for each measurement and adapting its content to the experimental conditions can be time consuming.
In that case we suggest using [autotag-metadata](https://echemdb.github.io/autotag-metadata/),
which allows storing the metadata in YAML automatically along with the measurement file when it is created.

For further unitpackage creation, the information on the fields of the data file should be included in that YAML.
All echemdb projects expect this information to be nested in `figure description.fields`.
We used the name `figure description` since the data in a CSV is in principle a figure represented by values.
An example YAML looks as follows.

```{warning}
Since the echemdb modules are still under development, the key `figure description.fields` might change. Keep an eye on the Changelogs.
```

```{code-cell} ipython3
:tags: [remove-input]
from IPython.display import Code

Code(filename='../files/data/data.csv.meta.yaml', language='yaml')
```
