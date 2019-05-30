yamllint
========

A linter for YAML files.

yamllint does not only check for syntax validity, but for weirdnesses like key
repetition and cosmetic problems such as lines length, trailing spaces,
indentation, etc.

.. image::
   https://travis-ci.org/adrienverge/yamllint.svg?branch=master
   :target: https://travis-ci.org/adrienverge/yamllint
   :alt: CI tests status
.. image::
   https://coveralls.io/repos/github/adrienverge/yamllint/badge.svg?branch=master
   :target: https://coveralls.io/github/adrienverge/yamllint?branch=master
   :alt: Code coverage status
.. image:: https://readthedocs.org/projects/yamllint/badge/?version=latest
   :target: https://yamllint.readthedocs.io/en/latest/?badge=latest
   :alt: Documentation status

Written in Python (compatible with Python 2 & 3).

Documentation
-------------

https://yamllint.readthedocs.io/

Overview
--------

Screenshot
^^^^^^^^^^

.. image:: docs/screenshot.png
   :alt: yamllint screenshot

Installation
^^^^^^^^^^^^

On Fedora / CentOS (note: `EPEL <https://fedoraproject.org/wiki/EPEL>`_ is
required on CentOS):

.. code:: bash

 sudo dnf install yamllint

On Debian 8+ / Ubuntu 16.04+:

.. code:: bash

 sudo apt-get install yamllint

On FreeBSD:

.. code:: sh

  pkg install py27-yamllint
  pkg install py36-yamllint

On Mac OS 10.11+:

.. code:: bash

 brew install yamllint

Alternatively using pip, the Python package manager:

.. code:: bash

 pip install --user yamllint
 
Using docker:

.. code:: bash

 docker pull xtellurian/yamllint:latest
 docker run -v /path/to/yaml:/yaml xtellurian/yamllint:latest /yaml
 
 
Alternately, using docker in VS Code, add this to 
`VS Code tasks.json <https://code.visualstudio.com/docs/editor/tasks/>`_:

.. code:: json

 "tasks": [
     {
         "label": "Lint YAML",
         "type": "shell",
         "command": "docker",
         "args": [
             "run",
             "-v", 
             "${workspaceFolder}/:/yaml",
             "xtellurian/yamllint:latest",
             "/yaml"
         ]
     }
 ]

Usage
^^^^^

.. code:: bash

 # Lint one or more files
 yamllint my_file.yml my_other_file.yaml ...

.. code:: bash

 # Lint all YAML files in a directory
 yamllint .

.. code:: bash

 # Use a pre-defined lint configuration
 yamllint -d relaxed file.yaml

 # Use a custom lint configuration
 yamllint -c /path/to/myconfig file-to-lint.yaml

.. code:: bash

 # Output a parsable format (for syntax checking in editors like Vim, emacs...)
 yamllint -f parsable file.yaml

`Read more in the complete documentation! <https://yamllint.readthedocs.io/>`_

Features
^^^^^^^^

Here is a yamllint configuration file example:

.. code:: yaml

 extends: default

 rules:
   # 80 chars should be enough, but don't fail if a line is longer
   line-length:
     max: 80
     level: warning

   # don't bother me with this rule
   indentation: disable

Within a YAML file, special comments can be used to disable checks for a single
line:

.. code:: yaml

 This line is waaaaaaaaaay too long  # yamllint disable-line

or for a whole block:

.. code:: yaml

 # yamllint disable rule:colons
 - Lorem       : ipsum
   dolor       : sit amet,
   consectetur : adipiscing elit
 # yamllint enable

Specific files can be ignored (totally or for some rules only) using a
``.gitignore``-style pattern:

.. code:: yaml

 # For all rules
 ignore: |
   *.dont-lint-me.yaml
   /bin/
   !/bin/*.lint-me-anyway.yaml

 rules:
   key-duplicates:
     ignore: |
       generated
       *.template.yaml
   trailing-spaces:
     ignore: |
       *.ignore-trailing-spaces.yaml
       /ascii-art/*

`Read more in the complete documentation! <https://yamllint.readthedocs.io/>`_

License
-------

`GPL version 3 <LICENSE>`_
