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

# Advanced unitpackage usage

In principle unitpackages can be used in any kind of workflow which make use of the underlying data and metadata.
An example ist the [echemdb.org](https://www.echemdb.org/cv/) website, showing cyclic voltammograms, which have been classified by certain descriptors given in the unitpackage.
Similarly, one could use [Livemark](https://livemark.frictionlessdata.io/), a solution provided by the authors of [frictionless](https://frictionlessdata.io/).

An adapter to upload and include the unitpackages in electronic lab notebooks such as [ElabFTW](https://www.elabftw.net/), [Chemotion](https://chemotion.net/), [Kadi4Mat](https://kadi.iam.kit.edu/) or [LinkAhead](https://www.indiscale.com/linkahead/), is anticipated.
