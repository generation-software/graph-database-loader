=================================
Wilhelm Graph Database Python SDK
=================================

.. contents:: Table of Contents
    :depth: 2

Development
===========

Create virtual environment and install dependencies::

    git@github.com:QubitPi/wilhelm-graphdb-python.git
    cd wilhelm-graphdb-python
    python3 -m venv .venv
    . .venv/bin/activate

Then generate egg information from the `setup.py` and use the requirements.txt from these egg information to install all
the dependencies for development::

    python setup.py egg_info
    pip install -r wilhelm_graphdb_python.egg-info/requires.txt

API Documentation
=================

.. automodule:: wilhelm_graphdb_python.quizlet
   :members:
   :undoc-members:
   :show-inheritance:
