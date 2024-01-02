Camelot: PDF Table Extraction for Humans

**Camelot** is a Python library that can help you extract tables from PDFs

----

**Here's how you can extract tables from PDFs.** You can check out the PDF used in this example [here](pdf/foo.pdf).

``` py
>>> import camelot
>>> tables = camelot.read_pdf('foo.pdf')
>>> tables
<TableList n=1>
>>> tables.export('foo.csv', f='csv', compress=True) # json, excel, html, markdown, sqlite
>>> tables[0]
<Table shape=(7, 7)>
>>> tables[0].parsing_report
{
    'accuracy': 99.02,
    'whitespace': 12.24,
    'order': 1,
    'page': 1
}
>>> tables[0].to_csv('foo.csv') # to_json, to_excel, to_html, to_markdown, to_sqlite
>>> tables[0].df # get a pandas DataFrame!
```

{{ read_csv('csv/foo.csv') }}

Camelot also comes packaged with a [command-line interface](user_guide/cli.md)

!!! note
    Camelot only works with text-based PDFs and not scanned documents. As Tabula [explains](https://github.com/tabulapdf/tabula#why-tabula), "If you can click and drag to select text in your table in a PDF viewer, then your PDF is text-based".

You can check out some frequently asked questions [here](user_guide/faq.md).

## Why Camelot?

- **Configurability**: Camelot gives you control over the table extraction process with [tweakable settings](user_guide/advanced.md).
- **Metrics**: You can discard bad tables based on metrics like accuracy and whitespace, without having to manually look at each table.
- **Output**: Each table is extracted into a **pandas DataFrame**, which seamlessly integrates into *ETL and data analysis workflows*. You can also export tables to multiple formats, which include CSV, JSON, Excel, HTML, Markdown, and Sqlite.

- **ETL and data analysis workflows**: [see example notebook here](https://gist.github.com/vinayak-mehta/e5949f7c2410a0e12f25d3682dc9e873)

See [comparison with similar libraries and tools](https://github.com/camelot-dev/camelot/wiki/Comparison-with-other-PDF-Table-Extraction-libraries-and-tools).


## Support the development

If Camelot has helped you, please consider supporting its development with a one-time or monthly donation [on OpenCollective](https://opencollective.com/camelot).


## User Guide

This part of the documentation begins with some background information about why Camelot was created, takes you through some implementation details, and then focuses on step-by-step instructions for getting the most out of Camelot.

[User Guide](user_guide/advanced.md)

## API Reference

If you are looking for information on a specific function, class, or method, this part of the documentation is for you.

[API Reference](api.md)

## Contributor Guide

If you want to contribute to the project, this part of the documentation is for you.

[Contributor Guide](developers/contributing.md)
