.. _prerequisites:

*************
Prerequisites
*************
 
The following items need to be established before deploying applications on
Slate systems (Marble or Onyx OpenShift clusters).

Establish a project/namespace on Onyx or Marble
-----------------------------------------------

Follow :ref:`slate_getting_started` if you do not already have a
project/namespace established on Onyx or Marble.

Install the OC tool
-------------------

The OC tool provides CLI access to the OpenShift cluster. It needs to be
installed on your machine.

It is a single binary that can be downloaded from a number of places (the
choice is yours):

* Direct from the cluster (preferred):

  * `Marble Command Line Tools <https://console-openshift-console.apps.marble.ccs.ornl.gov/command-line-tools>`_

  * `Onyx Command Line Tools <https://console-openshift-console.apps.onyx.ccs.ornl.gov/command-line-tools>`_

- `Homebrew <https://brew.sh/>`_ on MacOS (need Homebrew setup first): 

 .. note::

     The Homebrew package is not always kept up to date with the latest version
     of OpenShift so some client features may not be available

 .. code-block:: bash

     $ brew install openshift-cli 

- RHEL/CentOS (requires openshift-origin repo):

 .. code-block:: bash

     $ yum install origin-clients

- Download the TAR file for your system `<https://mirror.openshift.com/pub/openshift-v4/clients/oc/latest/>`_
    
     Extract the binary with ``tar -xvf <your.tar.gz>``.

     You can copy the extracted binary to ``/usr/local/bin`` to add it to your
     ``$PATH``. This allows you to call the binary from anywhere in your
     terminal, instead of specifying the full path.

Test login with OC Tool
-----------------------

+-----------------------------------------------------------------------------+--------------------------------------+
| Cluster                                                                     | URL                                  |
+=============================================================================+======================================+
|  Marble (Moderate Production cluster with access to Summit/Alpine)          | `<https://api.marble.ccs.ornl.gov>`_ |
+-----------------------------------------------------------------------------+--------------------------------------+
|  Onyx   (Open Production Cluster with access to Wolf)                       | `<https://onyx.ccs.ornl.gov/>`_      |
+-----------------------------------------------------------------------------+--------------------------------------+

 Replace ``<URL>`` with the appropriate cluster link above (Onyx or Marble).

.. code-block:: bash

   $ oc login <URL>

(**NOTE**: Marble authentication uses NCCS Usernames and RSA passcodes. Onyx
uses XCAMS usernames and passwords).

Once you login, the output will tell you what projects/namespaces you have
access to. 

You can view/select/switch between projects/namespaces with the ``oc`` tool:

 .. code-block:: bash
    
    #List all projects/namespaces available to you
    $ oc get projects

    #Use or work within specific project/namespace
    $ oc project <project-name>

Install Helm
------------

It is recommended to use Helm version 3. 

Helm enables application deployment via `Helm Charts
<https://helm.sh/docs/topics/charts/>`_. The high level `Helm Architecture
<https://helm.sh/docs/topics/architecture/>`_ docs are also a great reference
for understanding Helm.

Like ``oc``, Helm is a single binary executable. 

 - This can be installed on macOS with `Homebrew <https://brew.sh/>`_ : 
 
 .. code-block:: bash 

     $ brew install helm

 - Or can be pulled from the `Helm Release Page
   <https://github.com/helm/helm/releases>`_. If downloading from the GitHub
   release page, you can copy this executable into ``/usr/local/bin`` to add it to
   ``$PATH``.

 **NOTE:** One nice feature of Helm is that it uses the underlying
 authentication credentials used with ``oc``, so once you login with ``oc login``,
 the helm client will authenticate automatically.

 Once ``oc`` and ``helm`` are setup and you are logged in with ``oc login``, test Helm:

  .. code-block:: bash

     $ helm ls
