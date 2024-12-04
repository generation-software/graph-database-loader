==================
Wilhelm Python SDK
==================

.. contents:: Table of Contents
    :depth: 2

Install
=======

To install the SDK, simply run::

    pip installwilhelm_data_loader

Load Wilhelm Vocabularies into Neo4J Database
=============================================

1. Make ready a Neo4J database instance. A free one can be obtained at https://console.neo4j.io
2. Set the following environment variables

   - **NEO4J_URI**: the connection URL of the database, such as "neo4j://localhost", "neo4j+s://xxx.databases.neo4j.io"
   - **NEO4J_DATABASE**: the database name
   - **NEO4J_USERNAME**: the username for connecting the database
   - **NEO4J_PASSWORD**: the user's password for the connection

  where all of them are available when database is provisioned on https://console.neo4j.io

3. Load vocabulary into Neo4J database:

  .. code-block:: python

     from wilhelm_python_sdk.german_neo4j_loader import load_into_database

     if __name__ == "__main__":
         load_into_database("german.yaml")

If we would like to empty database, we can do

.. code-block:: python

   from wilhelm_python_sdk.database_manager import cleanup_neo4j

   if __name__ == "__main__":
       cleanup_neo4j()

Note that this function targets the same database with the same credentials listed above

API Documentation
=================

.. automodule:: wilhelm_python_sdk.german_loader
   :members:
   :undoc-members:
   :show-inheritance:

.. automodule:: wilhelm_python_sdk.latin_loader
   :members:
   :undoc-members:
   :show-inheritance:

.. automodule:: wilhelm_python_sdk.ancient_greek_loader
   :members:
   :undoc-members:
   :show-inheritance:

.. automodule:: wilhelm_python_sdk.vocabulary_parser
   :members:
   :undoc-members:
   :show-inheritance:

.. automodule:: wilhelm_python_sdk.database_clients
   :members:
   :undoc-members:
   :show-inheritance:

.. automodule:: wilhelm_python_sdk.database_manager
   :members:
   :undoc-members:
   :show-inheritance:

Development
===========

Create virtual environment and install dependencies::

    git@github.com:QubitPi/wilhelm-data-loader.git
    cdwilhelm_data_loader
    python3 -m venv .venv
    . .venv/bin/activate

Then generate egg information from the `setup.py` and use the requirements.txt from these egg information to install all
the dependencies for development::

    python setup.py egg_info
    pip install -r wilhelm_python_sdk.egg-info/requires.txt

Troubleshooting
---------------

If CI/CD reports an error of::

    Imports are incorrectly sorted and/or formatted.

It's because the project is using `isort <https://pycqa.github.io/isort/>`_ to enforce the import order and in this case
isort detects an incorrectly ordered import in source file. Simply run::

   isort <the reported file>
