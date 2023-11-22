---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.15.2
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Create a unitpackage

Unitpackages can be created the moment files are created or at any later stage from the raw data.
The unitpackage is based on the [frictionless framework](https://framework.frictionlessdata.io/),
which has been adapted to meet the requirements to annotate scientific data.
Read more in the [unitpackage documentation](https://echemdb.github.io/unitpackage/usage/unitpackage.html).

## Creation from scratch

We start with an ideal CSV, where the first row contains the column names and all values are actually separated by commas.

```{code-cell} ipython3
:tags: [remove-input]

import pandas as pd
df = pd.read_csv('../files/data/data_for_packaging.csv')
df
```

We can build the unitpackage from scratch with the frictionless interface. First create the frictionless package.

```{code-cell} ipython3
from frictionless import describe

package = describe('../files/data/data_for_packaging.csv', type="package")
package
```

Next we update the fields such that they also contain the units.

```{code-cell} ipython3
schema = package.resources[0].schema
schema.update_field('t', {'unit': 's'})
schema.update_field('U', {'unit': 'mV'})
schema.update_field('U', {'description': 'Voltage across resistor 1.'})
package
```

Add some metadata. Read more on metadata and its inclusion in datapackages in the [metadata](metadata.md) section.

```{code-cell} ipython3
metadata = {'experimentalist': 'Max Doe',
            'supervisor': 'John Mustermann',
            'research question': 'Resistance of a resistor connected in series to a power supply.'}
package.resources[0].custom.setdefault("metadata", {})
package.resources[0].custom["metadata"].setdefault("echemdb", metadata)
package
```

Finally [save the package](https://framework.frictionlessdata.io/docs/framework/package.html#saving-descriptor) along with the original data.
We save both files in a new folder.
We also tend to save the datapackage with an additional `package` suffix.

```{code-cell} ipython3
:tags: [remove-output]

import shutil

shutil.copyfile('../files/data/data_for_packaging.csv', '../files/data/generated/data_for_packaging.csv')
package.resources[0].path = 'data_for_packaging.csv' # package is usually relative to the path of the file.
package.to_json('../files/data/generated/data_for_packaging.package.json')
```

## Creation by other approaches

The aforementioned workflow will at some point be implemented in the unitpackage API or a related CLI.

Depending on the type of data, for example non-standard CSV files, the data should possibly be converted and them stored as a datapackage.
This topic is addressed in the [echemdb-converters](https://echemdb.github.io/echemdb-converters/).
