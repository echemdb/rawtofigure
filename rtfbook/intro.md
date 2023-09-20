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
# Welcome to RawToFigure

This documentation describes [echemdbs'](https://github.com/echemdb) take on research data management (RDM) from raw data to publishable figures. We aim at providing a lightweight approach to annotating research data with metadata when it is created and to create machine readable [unitpackages](https://echemdb.github.io/unitpackage/). These unitpackages can be used to browse your data locally, for comparison with published data, for integration in data processing workflows, or for creation of entries in electronic lab notebooks (ELN).

<!--
The examples provided in this documentation are often related to data found in the research area of electrochemistry, but the concepts are transferrable to other research areas.
-->

## Example

Consider you record the following data as a {download}`data.csv <files/data/data.csv>`. It is unclear which units the values have, nor can you infer which voltage `U` has been measured or if it has been applied to something.

```sh .noeval
t,U
0,101
1,102
2,105
```

```{hint}
All demo files mentioned in this documentation can be found in the [repository](https://github.com/echemdb/rawtofigure/rtfbook/files).
```

Such information is stored as additional metadata along with the csv automatically using [`autotag-metadata`](https://echemdb.github.io/autotag-metadata/), a tool which observes a folder for file changes and writes the metadata from a template. For the above CSV the {download}`YAML <files/data/data.csv.meta.yaml>` could look as follows.

```yaml .noeval
experimentalist: Max Doe
supervisor: John Mustermann
research question: Resistance of a resistor connected in series to a power supply.
figure description:
    schema:
        fields:
          - name: t
            unit: s
          - name: U
            unit: mV
            description: Voltage across resistor 1.
```

There is no limitation on the amount of metadata stored along with your data as illustrated on the example of [echemdbs' metadata schema](https://github.com/echemdb/metadata-schema/blob/main/examples/file_schemas/autotag.yaml) for electrochemical data.

The CSV and YAML can be used to create a [unitpackage](https://echemdb.github.io/unitpackage/usage/unitpackage.html), a file standard which is based on [frictionless datpackages](https://framework.frictionlessdata.io/). For our purpose we create unitpackages with [`echemdbconverters`](https://echemdb.github.io/unitpackage/usage/echemdb-converters.html), providing a simple command line interface.

```{code-cell} ipython3
!echemdbconverters csv files/data/data.csv --metadata files/data/data.csv.meta.yaml --outdir files/data/generated
```

A collection of such datapackages can be loaded with the [unitpackage API](https://echemdb.github.io/unitpackage/usage/local_collection.html) to browse, explore, modify or visualize the entries. Here we display the original data of the CSV above with different units.

```{code-cell} ipython3
from unitpackage.collection import Collection
from unitpackage.local import collect_datapackages

db = Collection(collect_datapackages('files/data/generated'))
entry = db['data']
entry.rescale({'t':'ms', 'U':'V'}).plot('t', 'U')
```

The metadata from the YAML is also directly accessible.

```{code-cell} ipython3
entry.research_question
```

## Further usage

The standardized unitpackages allow for further integration of research data in different projects. For example, a collection of electrochemical data extracted from the literature is shown on the echemdb website and are directly accessible with API introduced above. In principle this allows direct comparison between published and raw data.

We suggest that locally stored unitpackages are also useful to generate automatically entries in ELNs, which play an important role in RDM workflows.

```{tableofcontents}
```
