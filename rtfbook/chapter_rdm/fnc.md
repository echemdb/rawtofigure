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
# File Naming Convention (FNC)

One of the first steps usually associated with RDM is to agree on a file naming convention (FNC).
While it is beneficial to include the most important information in the filename, this is not necessarily required when using frictionless datapackages since all metadata associated with the measurement will finally be included in the datapackage.
Most importantly the file name of a measurement must be unique, as it is later used as the identifier of the datapackage!
Nevertheless, when you work partly in your file system it is wise to include some additional information in the filename.

A suggested filename could look as follows:

`YYYY-MM-DD_<UserID>_<setupID>_<sampleID>_<measurement_environment>_<measurement_number>.csv`

The IDs' are ideally identical to those used in your electronic lab notebook (or wherever you store such information).

In general we also highgly recommend applying to the following rules which can also be found [elsewhere](https://rdmkit.elixir-europe.org/data_organisation.html#what-is-the-best-way-to-name-a-file):

* Do not use spaces! Use underscores (_), hyphens (- ) instead or capitalized letters to separate elements in the name.
* Do not use special characters: ?!& , * % # ; * ( ) @$ ^ ~ ‘ { } [ ] < >.
