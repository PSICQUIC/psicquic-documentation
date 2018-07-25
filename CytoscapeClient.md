# PSICQUIC Client Plugin for Cytoscape Quick Start #

## News ##
  * 3/13/2014: Now PSICQUIC Client is a built-in core feature in Cytoscape 3.1.  You do not have to install plugins to use it.
  * 6/1/2012: New Cytoscape Plugin version 0.31 released.  This update is recommended for all current users. Please use with latest version of Cytoscape (2.8.3).
    * _Smart Label_ - Plugin adds more human-readable gene names to the node
    * Color coding based on species name
    * Bug fixes for edge score import function
  * 5/30/2012: Now PSICQUIC Client is part of Cytoscape 3 core!
  * 7/28/2010: version 0.25 released.  This is compatible with Cytoscape 2.7.0 or later.

## Introduction ##

**[Cytoscape](http://www.cytoscape.org)** is an open source platform for general network data integration, analysis, and visualization.  It is widely used in systems biology community and  is expandable by plugins.  PSICQUIC Universal Client is a Cytoscape plugin for querying multiple PSICQUIC-compliant interaction data services from a simple user interface.

The advantage of using PSICQUIC services with Cytoscape client is you can save your work as a snapshot (session file) and also you can use its powerful visualization features.  For more information about Cytoscape, please visit official [web site](http://www.cytoscape.org).

## Overview of Client User Interface ##

PSICQUIC Client for Cytoscape is a part of Cytoscape's web service client framework. You can access PSICQUIC databases just like the [other clients](Clients.md). From a single window, you can send your query to all of [registered PSICQUIC services](http://www.ebi.ac.uk/Tools/webservices/psicquic/registry/registry?action=STATUS) at once.

## How to Use PSICQUIC Client in Cytoscape 2 ##

### Install Plugin ###
The PSICQUIC Client Plugin is compatible with Cytoscape 2.7.0 or later.  If you have older versions, please [download the latest version](http://www.cytoscape.org/). The Plugin is available from Cytoscape Plugin Manager.  Select **Plugin-->Manage Plugins** and then you can find the plugin under _Network and Attribute IO_ section --> PSICQUICUniversalClient

### Start Plugin ###
To start the plugin, select the client from _File-->Import-->Network from web services..._.  If PSICQUIC client is properly installed, you can find it in **Data Source** combo box.

### Query Services ###

There are two search modes in the client:

  * Search by Interactor ID
  * Search by Query ([MIQL](MiqlReference.md))

You can switch the mode from Search Property tab.

#### Search by Interactor ID(s) ####
In this mode, Cytoscape sends list of identifiers as query. You can simply copy and paste list of identifiers to the text box. After the search process, it pops up a window, where you can select which data sets you want to import. If the result is 0 or the service is inactive, it will be ignored. When the import process is finished, you also have the option to edit the network titles if you want. If you press the **Merge** button, the Advanced Network Marge plugin will be started and you can merge imported networks manually.

#### Search by MIQL ####
This mode supports MIQL syntax.  You can simply type the query in the text field.  For more information about MIQL, please read the [reference page](MiqlReference.md).

### PSICQUIC Client in Cytoscape 3 ###
Cytoscape 3.1.0 has been released since 2014 and the PSICQUIC client feature is a built-in function from that version. To try the new version, please visit [here](http://www.cytoscape.org/).

## Need Help? ##
Please join [our user mailing list](https://groups.google.com/forum/?fromgroups#!forum/cytoscape-helpdesk). All core developers of Cytoscape are available to answer your questions.