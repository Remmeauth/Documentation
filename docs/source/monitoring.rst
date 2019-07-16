**********
Monitoring
**********

Another option to check if your node has completed a correct setup is through monitoring. While starting the node, the
monitoring has also been installed and started. Completing this step is required.

Monitoring is a process of tracking application performance to detect and prevent issues that could occur with your
application on a particular server. For the monitoring, we will use ``ELK stack``. It is an open source, feature-rich
metrics dashboard and graph editor stack.

Step 1: install Docker
======================

Ubuntu
------

.. code-block:: console

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add && \
          sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
          sudo apt-get update && sudo apt-get install docker-ce -y && \
          sudo curl -o /usr/local/bin/docker-compose -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" && \
          sudo chmod +x /usr/local/bin/docker-compose

Step 2: start the project
============================

Download the project and start it with the following command:

.. code-block:: console

    $ git clone https://github.com/Remmeauth/protocol-monitoring && \
          cd protocol-monitoring && \
          sudo docker-compose -f docker-compose-linux.yml up -d && \
          curl -X POST "localhost:5601/api/saved_objects/_import" -H "kbn-xsrf: true" --form file=@export.ndjson

Step 3: visualization and graphs
================================

On confirming the stack is started, navigate to ``Kibana`` at ``http://<ip-address>:5601``.

.. image:: /img/monitoring/kibana-main-page.png
   :width: 100%
   :align: center
   :alt: Kibana main page

To see visualization and graphs, go to ``Dashboards`` -> ``[Metricbeat System] Host overview ECS``.

Dashboards
==========

The toll named ``Metricbeat`` collects the following data: filesystem per host, system overview, CPU, filesystem,
memory, network, overview, processes.

Technical notes
===============

The following summarises some important technical considerations:

1. The ``Elasticsearch`` instances uses a named volume ``esdata`` for data persistence between restarts. It exposes ``HTTP`` port ``9200`` for communication with other containers.
2. Environment variable defaults can be found in the file ``.env``.
3. The Elasticsearch container has its memory limited to ``1g``. This can be adjusted using the environment parameter ``ES_MEM_LIMIT``. ``Elasticsearch`` has a heap size of ``1g``. This can be adjusted through the environment variable ``ES_JVM_HEAP`` and should be set to 50% of the ``ES_MEM_LIMIT``. Users may wish to adjust this value on smaller machines.
4. The Elasticsearch password can be set via the environment variable ``ES_PASSWORD``. This sets the password for the ``Elastic`` and ``Kibana`` user.
5. The Kibana container exposes the port ``5601``.
6. All configuration files can be found in the extracted folder ./config.
7. The Metricbeat container mounts both ``/proc`` and ``/sys/fs/cgroup`` on ``Linux``. This allows ``Metricbeat`` to use the system module report on disk, memory, network and cpu of the host.
8. On systems with ``POSIX`` file permissions, all Beats configuration files are subject to ownership and file permission checks. The purpose of these checks is to prevent unauthorized users from providing or modifying configurations that are run by the Beat. The owner of the configuration file must be either root or the user who is executing the ``Beat`` process. The permissions on the file must disallow writes by anyone other than the owner. As we mount our configurations from the host, where the user is likely different than that used to run the container and the beat process, we disable this check for all beats with ``-strict.perms=false``.

Customising the Stack
=====================

With respect to the current example, we have provided a few simple entry points for customisation:

1. The example includes an ``.env`` file listing environment variables which alter the behaviour of the stack. These environment variables allow the user to change:

  a. ``ELASTIC_VERSION`` - the ``Elastic Stack`` version (default 7.2.0)
  b. ``ES_PASSWORD`` - the password used for authentication with the elastic user. This password is applied for all system users i.e. ``kibana`` and ``logstash_system``. Defaults to ``changeme``.
  c. ``DEFAULT_INDEX_PATTERN`` - The index pattern used as the default in ``Kibana``. Defaults to ``metricbeat-*``.
  d. ``ES_MEM_LIMIT`` - The memory limit used for the ``Elasticsearch`` container. Defaults to 1g. Consider reducing for smaller machines.
  e. ``ES_JVM_HEAP`` - The ``Elasticsearch JVM`` heap size. Defaults to 1024m and should be set to half of the ``ES_MEM_LIMIT``.

2. Modules and Configuration - All configuration to the containers is provided through a mounted ``./config`` directory.
Where possible, this exploits the dynamic configuration loading capabilities of ``Beats``. For example, an additional
module could be added by simply adding a file to the directory ``./config/beats/metricbeat/modules.d/`` in the required format.

Shutting down the stack
=======================

The following command will exit the containers and ensure they are shut down gracefully.

.. code-block:: console

    $ sudo docker-compose -f docker-compose-linux.yml stop

To remove all containers, including their mounted named volumes, use the following command:

.. code-block:: console

    $ sudo docker-compose -f docker-compose-linux.yml down -v
