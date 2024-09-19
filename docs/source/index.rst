==================
Wilhelm Python SDK
==================

.. contents:: Table of Contents
    :depth: 2

Install
=======

To install the SDK, simply run::

    pip install wilhelm-python-sdk

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

Wiktionary Parser
=================

Ancient Greek Verb Conjugation Parser
-------------------------------------

Take `ἔχω <https://en.wiktionary.org/wiki/ἔχω#Inflection>`_ as an example:

.. code-block:: python

   from wilhelm_python_sdk.ancient_greek_wiktionary_parser import parse_all_conjugation_tables

   tables = parse_all_conjugation_tables("https://en.wiktionary.org/wiki/ἔχω")

shall produce a dictionary of 12 key-value pairs::

    "Present: ἔχω, ἔχομαι": [
        [number        , number     , singular, singular  , singular, dual    , dual          , plural        , plural        , plural        ]
        [              ,            , first   , second    , third   , second  , third         , first         , second        , third         ]
        [active        , indicative , ἔχω     , ἔχεις     , ἔχει    , ἔχετον  , ἔχετον        , ἔχομεν        , ἔχετε         , ἔχουσῐ(ν)     ]
        [active        , subjunctive, ἔχω     , ἔχῃς      , ἔχῃ     , ἔχητον  , ἔχητον        , ἔχωμεν        , ἔχητε         , ἔχωσῐ(ν)      ]
        [active        , optative   , ἔχοιμῐ  , ἔχοις     , ἔχοι    , ἔχοιτον , ἐχοίτην       , ἔχοιμεν       , ἔχοιτε        , ἔχοιεν        ]
        [active        , imperative ,         , ἔχε       , ἐχέτω   , ἔχετον  , ἐχέτων        ,               , ἔχετε         , ἐχόντων       ]
        [middle/passive, indicative , ἔχομαι  , "ἔχῃ,ἔχει", ἔχεται  , ἔχεσθον , ἔχεσθον       , ἐχόμεθᾰ       , ἔχεσθε        , ἔχονται       ]
        [middle/passive, subjunctive, ἔχωμαι  , ἔχῃ       , ἔχηται  , ἔχησθον , ἔχησθον       , ἐχώμεθᾰ       , ἔχησθε        , ἔχωνται       ]
        [middle/passive, optative   , ἐχοίμην , ἔχοιο     , ἔχοιτο  , ἔχοισθον, ἐχοίσθην      , ἐχοίμεθᾰ      , ἔχοισθε       , ἔχοιντο       ]
        [middle/passive, imperative ,         , ἔχου      , ἐχέσθω  , ἔχεσθον , ἐχέσθων       ,               , ἔχεσθε        , ἐχέσθων       ]
        [              ,            , active  , active    , active  , active  , middle/passive, middle/passive, middle/passive, middle/passive]
        [infinitive    , infinitive , ἔχειν   , ἔχειν     , ἔχειν   , ἔχειν   , ἔχεσθαι       , ἔχεσθαι       , ἔχεσθαι       , ἔχεσθαι       ]
        [participle    , m          , ἔχων    , ἔχων      , ἔχων    , ἔχων    , ἐχόμενος      , ἐχόμενος      , ἐχόμενος      , ἐχόμενος      ]
        [participle    , f          , ἔχουσᾰ  , ἔχουσᾰ    , ἔχουσᾰ  , ἔχουσᾰ  , ἐχομένη       , ἐχομένη       , ἐχομένη       , ἐχομένη       ]
        [participle    , n          , ἔχον    , ἔχον      , ἔχον    , ἔχον    , ἐχόμενον      , ἐχόμενον      , ἐχόμενον      , ἐχόμενον      ]
    ],
    "Present: ἔχω, ἔχομαι (Epic)": [...],
    "Imperfect: εἶχον, εἰχόμην": [...],
    ...

Note that the key of the dictionary is of type string and the value is of type double-array

API Documentation
=================

.. automodule:: wilhelm_python_sdk.german_neo4j_loader
   :members:
   :undoc-members:
   :show-inheritance:

.. automodule:: wilhelm_python_sdk.database_manager
   :members:
   :undoc-members:
   :show-inheritance:

.. automodule:: wilhelm_python_sdk.ancient_greek_wiktionary_parser
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

Troubleshooting
---------------

If CI/CD reports an error of::

    Imports are incorrectly sorted and/or formatted.

It's because the project is using `isort <https://pycqa.github.io/isort/>`_ to enforce the import order and in this case
isort detects an incorrectly ordered import in source file. Simply run::

   isort <the reported file>
