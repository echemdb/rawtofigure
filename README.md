# RawToFigure

Raw to figure describes echemdb's approaches towards research data management (RDM).

## Contribute

If you want to modify rawtofigure's content itself, get a copy of the latest
unreleased version of this repository:

```sh
git clone https://github.com/echemdb/rawtofigure.git
```

Go to the directory and install the dependencies with

```sh
conda env create --file environment.yaml
conda activate rawtofigure
```

To build the page locally, run

```sh
jb build mybookname/
```

<!--**Note:** The build requires internet access, since data is pulled from
external repositories to evaluate the documentation content.-->

The generated files are located in `rtfbook/_build/html` and can be browsed
by simply opening the generated files or via:

```sh
python -m http.server 8880 -b localhost --directory rtfbook/_build/html
```

Then open http://localhost:8880/ with your browser.
