.. Sumo Notebooks documentation master file, created by
   sphinx-quickstart on Fri Jul 20 14:54:02 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Sumo Notebooks's documentation!
==========================================

Sumo Notebooks provide a way to seamlessly access data stored in Sumo for the purpose of data exploration and statistical analysis. The notebooks provide an interactive way to gain and share insights of a dataset. Built on top of Apache Zeppelin and Jupyter, Sumo Notebooks provide a state-of-the-art user experience coupled with access to the most recent machine learning frameworks such as Apache Spark, tensorflow, etc to unlock the value of machine data.

.. note::  This is an experimental feature under development.

.. toctree::
   :maxdepth: 2
   :caption: Contents:

Getting Started
===============

Sumo Notebooks are organized as a docker container that assembles all dependencies in a single container. This simplifies installing and updating. A Sumo Notebooks container gets access to an organzation's Sumo data store via Sumo's REST API. For that purpose, we require you to create an access key for Sumo as described in `this guide <https://help.sumologic.com/Manage/Security/Access-Keys>`_. After creating access credentials, please follow these steps to install and run the Sumo Notebooks container.

0. Open a shell or terminal on your computer

1. Load the SumoLab docker container on your computer:
``docker pull sumologic/sumonotebooks:latest``

2. Start the container. API access id and access key can be either submitted via the command line or entered via the Spark interpreter configuration menu in Zeppelin.
``docker run -d -it -p 8088:8080 -e ZEPPELIN_SPARK_SUMO_ACCESSID='XXX' -e ZEPPELIN_SPARK_SUMO_ACCESSKEY='XXX' sumologic/sumonotebooks:latest``

3. Open the Zeppelin UI and find some sample notebooks under the 'Notebook' drop down menu.
``http://localhost:8088``

.. note:: It is a prerequisite to have a working docker installed.

Data Science Workflow
=====================

The foundational datastructure for Sumo notebooks is a data frame. A typical data science workflow manipulates data frames in many ways. For instance, data frames might be transformed for feature generation and statistical analysis, or joined with another dataset for enrichment. Therefore, a Sumo notebook returns query results in a Spark dataframe. This enables users to tap into Spark's development universe, or -- using the ``toPandas`` method -- switch over to a python-native approach for data analytics.

Troubleshooting
===============

**No data or exception:**

* Make sure to have the right access credentials in place

**TTransportException or timeout**

* Restart the interpreter: Use black, top right gear for pulling up interpreter menu, then push restart icon on the left of the blue bar listing the interpreter group for spark, finally save on the bottom.


Other Documentation
======================

* `Apache Zeppelin Documentation <https://zeppelin.apache.org/docs/0.8.0/>`_
* `HortonWorks: How to diagnose zeppelin <https://community.hortonworks.com/articles/70658/how-to-diagnose-zeppelin.html>`_
* `MapR: Troubleshooting Zeppelin <https://maprdocs.mapr.com/home/Zeppelin/TroubleshootingZeppelin.html>`_
* `Qubole: Debugging Notebook Issues <https://docs.qubole.com/en/latest/user-guide/notebook/debug-notebooks.html>`_


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
