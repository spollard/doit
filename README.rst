================
README
================

.. display some badges

.. image:: https://img.shields.io/pypi/v/doit.svg
    :target: https://pypi.python.org/pypi/doit

.. image:: https://github.com/pydoit/doit/actions/workflows/ci.yml/badge.svg?branch=master
    :target: https://github.com/pydoit/doit/actions/workflows/ci.yml?query=branch%3Amaster

.. image:: https://codecov.io/gh/pydoit/doit/branch/master/graph/badge.svg?token=wxKa1h11zn
    :target: https://codecov.io/gh/pydoit/doit

.. image:: https://xscode.com/assets/promo-banner.svg
    :target: https://xscode.com/schettino72/doit


doit - automation tool
======================

*doit* comes from the idea of bringing the power of build-tools to
execute any kind of task


Sample Code
===========

Define functions returning python dict with task's meta-data.

Snippet from `tutorial <http://pydoit.org/tutorial_1.html>`_:

.. code:: python

  def task_imports():
      """find imports from a python module"""
      for name, module in PKG_MODULES.by_name.items():
          yield {
              'name': name,
              'file_dep': [module.path],
              'actions': [(get_imports, (PKG_MODULES, module.path))],
          }

  def task_dot():
      """generate a graphviz's dot graph from module imports"""
      return {
          'targets': ['requests.dot'],
          'actions': [module_to_dot],
          'getargs': {'imports': ('imports', 'modules')},
          'clean': True,
      }

  def task_draw():
      """generate image from a dot file"""
      return {
          'file_dep': ['requests.dot'],
          'targets': ['requests.png'],
          'actions': ['dot -Tpng %(dependencies)s -o %(targets)s'],
          'clean': True,
      }


Run from terminal::

  $ doit list
  dot       generate a graphviz's dot graph from module imports
  draw      generate image from a dot file
  imports   find imports from a python module
  $ doit
  .  imports:requests.models
  .  imports:requests.__init__
  .  imports:requests.help
  (...)
  .  dot
  .  draw


Project Details
===============

 - Website & docs - http://pydoit.org
 - Project management on github - https://github.com/pydoit/doit
 - Discussion group - https://groups.google.com/forum/#!forum/python-doit
 - News/twitter - https://twitter.com/py_doit
 - Plugins, extensions and projects based on doit - https://github.com/pydoit/doit/wiki/powered-by-doit

license
=======

The MIT License
Copyright (c) 2008-2021 Eduardo Naufel Schettino

see LICENSE file


developers / contributors
==========================

see AUTHORS file


install
=======

*doit* is tested on python 3.6 to 3.9.

The last version supporting python 2 is version 0.29.

.. code:: bash

 $ pip install doit


dependencies
=============

- cloudpickle
- pyinotify (linux)
- macfsevents (mac)

Tools required for development:

- git * VCS
- py.test * unit-tests
- coverage * code coverage
- sphinx * doc tool
- pyflakes * syntax checker
- doit-py * helper to run dev tasks


development setup
==================

The best way to setup an environment to develop *doit* itself is to
create a virtualenv...

.. code:: bash

  doit$ virtualenv dev
  doit$ source dev/bin/activate

install ``doit`` as "editable", and add development dependencies
from `dev_requirements.txt`:

.. code:: bash

  (dev) doit$ pip install --editable .
  (dev) doit$ pip install --requirement dev_requirements.txt



tests
=======

Use py.test - http://pytest.org

.. code:: bash

  $ py.test



documentation
=============

``doc`` folder contains ReST documentation based on Sphinx.

.. code:: bash

 doc$ make html

They are the base for creating the website. The only difference is
that the website includes analytics tracking.
To create it (after installing *doit*):

.. code:: bash

 $ doit website



spell checking
--------------

All documentation is spell checked using the task `spell`:

.. code:: bash

  $ doit spell

It is a bit annoying that code snippets and names always fails the check,
these words must be added into the file `doc/dictionary.txt`.

The spell checker currently uses `hunspell`, to install it on debian based
systems install the hunspell package: `apt-get install hunspell`.


profiling
---------

.. code:: bash

  python -m cProfile -o output.pstats `which doit` list

  gprof2dot -f pstats output.pstats | dot -Tpng -o output.png


releases
========

Update version number at:

- doit/version.py
- setup.py
- doc/conf.py
- doc/index.html

.. code:: bash

   python setup.py sdist
   python setup.py bdist_wheel
   twine upload dist/doit-X.Y.Z.tar.gz
   twine upload dist/doit-X.Y.Z-py3-none-any.whl


contributing
==============

On github create pull requests using a named feature branch.

Financial contribution to support maintenance welcome.
https://xscode.com/schettino72/doit
