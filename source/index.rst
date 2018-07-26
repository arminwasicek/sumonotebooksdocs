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

Running the Sumo Notebooks Docker Container
-------------------------------------------

0. Open a shell or terminal on your computer

1. Load the SumoLab docker container on your computer:
``docker pull sumologic/sumonotebooks:latest``

2. Start the container. API access id and access key can be either submitted via the command line or entered via the Spark interpreter configuration menu in Zeppelin.
``docker run -d -it -p 8088:8080 -e ZEPPELIN_SPARK_SUMO_ACCESSID='XXX' -e ZEPPELIN_SPARK_SUMO_ACCESSKEY='XXX' sumologic/sumonotebooks:latest``

3. Open the Zeppelin UI and find some sample notebooks under the 'Notebook' drop down menu.
``http://localhost:8088``

.. note:: It is a prerequisite to have a working docker installed.

This is it, happy coding!


Setting the Access Keys
-----------------------

Sharing access id/key with the Sumo Notebooks container can be done using two methods:

* Submitting ``ZEPPELIN_SPARK_SUMO_ACCESSID`` and ``ZEPPELIN_SPARK_SUMO_ACCESSKEY`` environment variables to the container as shown in the previous section
* Setting or changing the access id/key pair within the Zeppelin web UI as shown below


Step 1
^^^^^^

Click on the username in the right top corner of the Zeppelin web UI. Scroll down or enter ``spark`` in the search bar to get to the Spark configuration page.

.. figure:: images/sumonotebooks_setting-the-accesskey-1.png
    :width: 600px
    :align: center
    :alt: Open the Spark interpreter configuration page

    Open the Spark interpreter configuration page

Step 2
^^^^^^

On the Spark configuration page click the ``edit`` button and then enter access id, access key, and http endpoint in the according text fields. An overview of the Sumo endpoints for the different deployments is listed on `this page <https://help.sumologic.com/APIs/General-API-Information/Sumo-Logic-Endpoints-and-Firewall-Security>`_. Finally, save the configuration and the interprester will restart with the new configuration.

.. figure:: images/sumonotebooks_setting-the-accesskey-2.png
    :width: 600px
    :align: center
    :alt: Enter the access id/key pair and save

    Enter the access id/key pair and save


Data Science Workflow
=====================

The foundational datastructure for Sumo notebooks is a data frame. A typical data science workflow manipulates data frames in many ways. For instance, data frames might be transformed for feature generation and statistical analysis, or joined with another dataset for enrichment. Therefore, a Sumo notebook returns query results in a Spark dataframe. This enables users to tap into Spark's development universe, or -- using the ``toPandas`` method -- switch over to a python-native approach for data analytics.

Troubleshooting
===============

Common Errors
-------------

**No data or exception:**

* Make sure to have the right access credentials in place

**TTransportException or timeout**

* Restart the interpreter: Use black, top right gear for pulling up interpreter menu, then push restart icon on the left of the blue bar listing the interpreter group for spark, finally save on the bottom.


Debugging
---------

The SparkSumoMemoryCache object is a key value store that holds the context of the most recent operations. It can be used to inquire on exceptions and results that are retrieve behind the scenes.


+---------------------------+----------------------------+--------------------------------------------------------------------------+
| Key                       | Type                       | Description                                                              |
+===========================+============================+==========================================================================+
| lastDataFrame             | DataFrame                  | Holds a reference to the last data frame that has been created           |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| lastLogQueryException     | Exception                  | References the last exception (if any) that the log backend threw        |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| lastMetricsQueryException | Exception                  | References the last exception (if any) that the log backend threw        |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| lastMetricsDimensions     | HashMap[String, String]    | Dictionary to resolve the metrics column header to the actual dimensions |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| lastQueryJob              | JobId                      | References the last job id returned from the search api                  |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| lastTriplet               | QueryTriplet               | Last processed query                                                     |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| metricsClient             | SumoMetricsClient          | Client used to retrieve metrics from Sumo                                |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| sumoClient                | SumoClient                 | Client used to retrieve logs from Sumo                                   |
+---------------------------+----------------------------+--------------------------------------------------------------------------+
| sparkSession              | SparkSession               | Spark session that is used to ingest the data                            |
+---------------------------+----------------------------+--------------------------------------------------------------------------+

Code example
^^^^^^^^^^^^

.. code-block:: scala

   val spark = SparkSumoMemoryCache.get("sparkSession").get.asInstanceOf[SparkSession]


Limitations
-----------

Current limits of the REST API are documented `here <https://help.sumologic.com/APIs/Search-Job-API/About-the-Search-Job-API#Rate_limiting>`_.


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
