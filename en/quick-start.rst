===================
Quick Startup Guide
===================

Overview
========

This document describes a minimum step to install and use |Fess| .

Download
========

You can get the latest |Fess| release from
http://sourceforge.jp/projects/fess/releases/.

Installation
============

Unzip fess-server-x.y.zip to a directory you want to install. Grant an
execution permission to script files in bin directory.

::

    $ unzip fess-server-x.y.zip
    $ cd fess-server-x.y
    $ chmod +x bin/*.sh

Start |Fess| Server
=================

Run startup.[sh\|bat] script file to start |Fess| server.

::

    $ ./bin/startup.sh

Access to Administrative GUI
============================

Access to http://localhost:8080/fess/admin. The username/password for an
administrator is admin/admin.

Click "Web" link at the menu pane after logging in as admin user. Create
a web crawling configuration (Name, URL, Max access count,..) to crawl a
web site.

Click "Scheduled Jobs" link at the menu pane. Click "Edit" link for
Crawler job. Edit "Schedule" to start a crawling. If you want to start
crawling at 10:35am, type "0 35 10 \* \* ?" into Schedule field. The
format is "Sec Min Hour Day Month Day Year", which is like a cron
format. Click "Confirm" and "Update" button to save parameters. If you
set a crawling time as 10:35am, |Fess| start to crawl at 10:35am
automatically.

Session Info link show you the crawling information. If the crawl is
finished, WebIndexSize is displayed at Session Info page.

Search
======

Finished a crawling, access to http://localhost:8080/fess/. You can
search indexed documents and see the result.

Stop |Fess| 
=========

Run shutdown.[sh\|bat] script file to stop |Fess| server.

::

    $ ./bin/shutdown.sh
