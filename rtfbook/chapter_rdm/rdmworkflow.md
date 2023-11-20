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
# RDM Workflow

In this chapter we provide a more detailed description on how to implement our RDM approach in your laboratory, i.e., to create unitpackages for further usage.

## Notes

We do not provide solutions on how to include the unitpackages in repositories or ELNs as we are still experimenting with the package structure. Technically an automated inclusion in such system should, however, be possible.
A use case for electrochemical data is presented on [echemdb.org](https://www.echemdb.org/cv), where each entry is automatically generated from unitpackages.

Currently we focus primarily on CSV like files, but the approach can also be extended to image files or other types of data.

Some examples provided in this documentation are related to data found in the research area of electrochemistry, but the concepts are transferrable to any other research areas.

```{hint} All demo files mentioned in this documentation can be found in the [repository](https://github.com/echemdb/rawtofigure/rtfbook/files).
```
