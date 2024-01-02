---
title: Quick Start
---

In a hurry to extract tables from PDFs? This document gives a good introduction to help you get started with Camelot.

## Read the PDF

Reading a PDF to extract tables with Camelot is very simple.

Begin by importing the Camelot module::

``` python
>>> import camelot
```

Now, let's try to read a PDF. (You can check out the PDF used in this example [here](../pdf/foo.pdf)) Since the PDF has a table with clearly demarcated lines, we will use the [Lattice](how-it-works.md/#lattice) method here.

!!! note
    [Lattice](how-it-works.md/#lattice) is used by default. You can use [Stream](how-it-works.md/#stream) with `flavor='stream'`.

``` python
>>> tables = camelot.read_pdf('foo.pdf')
>>> tables
<TableList n=1>
```

Now, we have a [TableList](../api.md/#camelot.core.TableList) object called `tables`, which is a list of [Table](../api.md/#camelot.core.Table) objects. We can get everything we need from this object.

We can access each table using its index. From the code snippet above, we can see that the `tables` object has only one table, since `n=1`. Let's access the table using the index `0` and take a look at its `shape`.

``` python
>>> tables[0]
<Table shape=(7, 7)>
```

Let's print the parsing report.

``` python
>>> print tables[0].parsing_report
{
    'accuracy': 99.02,
    'whitespace': 12.24,
    'order': 1,
    'page': 1
}
```

Woah! The accuracy is top-notch and there is less whitespace, which means the table was most likely extracted correctly. You can access the table as a pandas DataFrame by using the [Table](../api.md/#camelot.core.Table) object's `df` property.

``` python
>>> tables[0].df
```

  {{ read_csv('foo.csv') }}

Looks good! You can now export the table as a CSV file using its [to_csv()](../api.md/#camelot.core.Table.to_csv) method. Alternatively you can use [to_json()](../api.md/#camelot.core.Table.to_json), [to_excel()](../api.md/#camelot.core.Table.to_excel), [to_html()](../api.md/#camelot.core.Table.to_html), [to_markdown()](../api.md/#camelot.core.Table.to_markdown) or [to_sqlite()](../api.md/#camelot.core.Table.to_sqlite) methods to export the table as JSON, Excel, HTML files or a sqlite database respectively.

``` python
>>> tables[0].to_csv('foo.csv')
```

This will export the table as a CSV file at the path specified. In this case, it is ``foo.csv`` in the current directory.

You can also export all tables at once, using the [TableList](../api.md/#camelot.core.TableList) object's  [export()](../api.md/#camelot.core.TableList.export) method.

``` python
>>> tables.export('foo.csv', f='csv')
```

!!! tip
    Here's how you can do the same with the [command-line interface](cli.md).

    ``` bash
    $ camelot --format csv --output foo.csv lattice foo.pdf
    ```

This will export all tables as CSV files at the path specified. Alternatively, you can use ``f='json'``, ``f='excel'``, ``f='html'``, ``f='markdown'`` or ``f='sqlite'``.

!!! note
    The [export()](../api.md/#camelot.core.TableList.export) method exports files with a `page-*-table-*` suffix. In the example above, the single table in the list will be exported to `foo-page-1-table-1.csv`. If the list contains multiple tables, multiple CSV files will be created. To avoid filling up your path with multiple files, you can use `compress=True`, which will create a single ZIP file at your path with all the CSV files.

!!! note
    Camelot handles rotated PDF pages automatically. As an exercise, try to extract the table out of [this PDF](../pdf/rotated.pdf).

## Specify page numbers

By default, Camelot only uses the first page of the PDF to extract tables. To specify multiple pages, you can use the ``pages`` keyword argument::

``` python
>>> camelot.read_pdf('your.pdf', pages='1,2,3')
```

!!! tip
    Here's how you can do the same with the [command-line interface](cli.md).

    ``` bash
    $ camelot --pages 1,2,3 lattice your.pdf
    ```

The ``pages`` keyword argument accepts pages as comma-separated string of page numbers. You can also specify page ranges — for example, ``pages=1,4-10,20-30`` or ``pages=1,4-10,20-end``.


## Reading encrypted PDFs

To extract tables from encrypted PDF files you must provide a password when calling [read_pdf()](../api.md/#camelot.io.read_pdf)`.

``` python
>>> tables = camelot.read_pdf('foo.pdf', password='userpass')
>>> tables
<TableList n=1>
```

!!! tip
    Here's how you can do the same with the [command-line interface](cli.md).

    ``` bash
    $ camelot --password userpass lattice foo.pdf
    ```

Camelot supports PDFs with all encryption types supported by [pypdf](https://pypdf.readthedocs.io/en/latest/user/pdf-version-support.html). This might require installing PyCryptodome. An exception is thrown if the PDF cannot be read. This may be due to no password being provided, an incorrect password, or an unsupported encryption algorithm.

Further encryption support may be added in future, however in the meantime if your PDF files are using unsupported encryption algorithms you are advised to remove encryption before calling [read_pdf()](../api.md/#camelot.io.read_pdf). This can been successfully achieved with third-party tools such as [QPDF](https://www.github.com/qpdf/qpdf).


``` bash
$ qpdf --password=<PASSWORD> --decrypt input.pdf output.pdf
```

----

Ready for more? Check out the [advanced](advanced.md) section.
