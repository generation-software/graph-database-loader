==================
Wilhelm Python SDK
==================

.. contents:: Table of Contents
    :depth: 2

Install
=======

To install the SDK, simply run

```console
pip install wilhelm-python-sdk
```

Load Wilhelm Vocabularies into Neo4J Database
=============================================

# Make ready a Neo4J database instance. A free one can be obtained at https://console.neo4j.io
# Set the following environment variables

  - `NEO4J_URI`: the connection URL of the database, such as "neo4j://localhost", "neo4j+s://xxx.databases.neo4j.io"
  - `NEO4J_USERNAME`: the username for connecting the database
  - `NEO4J_PASSWORD`: the user's password for the connection

  where all of them are available when database is provisioned on https://console.neo4j.io

# Load vocabulary into Neo4J database:

  .. code-block:: python

     from wilhelm_python_sdk.german_neo4j_loader import load_into_database

     if __name__ == "__main__":
         load_into_database("german.yaml")

If this is an experiment and we would like to empty database,
`simply run <https://stackoverflow.com/a/60933970/14312712>`_::

    match (a) -[r] -> () delete a, r;
    match (a) delete a;

API Documentation
=================

.. automodule:: wilhelm_python_sdk.quizlet
   :members:
   :undoc-members:
   :show-inheritance:

Development
===========

Create virtual environment and install dependencies::

    git@github.com:QubitPi/wilhelm-python-sdk.git
    cd wilhelm-python-sdk
    python3 -m venv .venv
    . .venv/bin/activate

Then generate egg information from the `setup.py` and use the requirements.txt from these egg information to install all
the dependencies for development::

    python setup.py egg_info
    pip install -r wilhelm_python_sdk.egg-info/requires.txt
