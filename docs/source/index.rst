=================================
Wilhelm Graph Database Python SDK
=================================

.. contents:: Table of Contents
    :depth: 2

Install
=======

To install the SDK, simply run

```console
pip install wilhelm-python-sdk
```

Upload Vocabulary CSV into Neo4J
================================

# Make ready a Neo4J database instance. A free one can be obtained at https://console.neo4j.io
# Set the following environment variables

  - `NEO4J_URI`: the connection URL of the database, such as "neo4j://localhost", "neo4j+s://xxx.databases.neo4j.io"
  - `NEO4J_USERNAME`: the username for connecting the database
  - `NEO4J_PASSWORD`: the user's password for the connection

  where all of them are available when database is provisioned on https://console.neo4j.io

# Have a vocabulary file of the following YAML format ready at __german.yaml__ (in this example, we are loading a
  German vocabulary):

  ```yaml
  vocabulary:
    - term: "null"
      definition: 0
    - term: Guten Tag
      definition: Good day
    - term: Hallo
      definition: Hello
    - term: Ich heiße ...
      definition: I am called ...
    - term: Mein Name ist ...
      definition: My name is ...
    - term: bitte
      definition: please
  ```

# Load vocabulary into Neo4J database:

  .. code-block:: python

     from wilhelm_python_sdk.neo4j_loader import load_into_database

     load_into_database("german.yaml", "German")

.. tip::Transform CSV into YAML
   The reason we use YAML is because it supports multi-line field value, a common case for vocabulary definitions. But
   in case the vocabulary is in CSV, the following Python script can be used to transform it into compatible YAML used
   in this library:

   .. code-block:: python
      import csv

      with open("/file/path/to/vocabulary.csv") as f:
          reader = csv.reader(f, delimiter=',')

          with open("/file/path/to/vocabulary.yaml", mode='w') as outfile:
              outfile.write("vocabulary:\n")

              for row in reader:
                  outfile.write("  - term: {}\n    definition: {}\n".format(row[0], row[1]))

   The following words must be quoted in YAML file in order to prevent them from being interpolated by YAML syntax

   - null
   - no

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
