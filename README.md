If you found this repo useful, consider clicking the sponsor button near the top :) Sponsoring via GitHub is as little as $1/month and if you do not use banks or credit cards, there are crypto links included :)<br /><br />
Documentation
=============

Project documentation is built using [Sphinx docs](http://sphinx-doc.org/), which uses [ReST](http://docutils.sourceforge.net/rst.html) for markup.  This allows the docs to cover a vast amount of topics without using a thousand-line README file.

Sphinx docs is pip-installable via `pip install sphinx`.  Once installed, open a command line in the docs folder and run the following commands:

```bash
$ sudo pip install -r requirements.txt
```

This will install the requirements needed for the generating the docs. Afterwards you can run:

```bash
$ make html
```

The docs will be generated, the output files will be placed in the `_build/html/` directory, and can be browsed (locally) with any browser.

The docs can also be found online at <http://bootstrap-datepicker.readthedocs.org/>.
