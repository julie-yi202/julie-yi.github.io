# Creating Scripted Inputs in Splunk
What You'll Learn

How Splunk ingests event data

How scripted inputs work

How to work with Representational State Transfer (REST) application programming interfaces (APIs)

How to write a script in Python that generates event data

How to troubleshoot scripted inputs when they fail

What You'll Need

A system with at least Python v3.7 or higher installed

Administrative access to a Splunk Enterprise server (can run on a remote system, or locally on your computer)

If you don't have a licensed Splunk Enterprise installation, you can obtain a free personal-use license from Splunk.com

Access to a REST API that you can query for event data

Assumptions

You have experience with navigating the Splunk Enterprise user interface

You are familiar with how to build basic Splunk Search Processing Language (SPL) queries

You have a basic understanding of shell scripting languages or the Python programming language

## Introducing Splunk

<img width="1222" height="787" alt="Screenshot 2026-06-02 144609" src="https://github.com/user-attachments/assets/5ca68458-22af-466e-aac8-8b4751695444" />


Splunk Enterprise Terminology

Event: A Splunk event is a set of values associated with a timestamp. It is a single data entry in a database, which can contain as much or as little information as necessary.

Metric: A Splunk metric is a data point entry associated with a timestamp, consisting of one or more measurements and, optionally, zero or more "dimensions" (attributes about the data point).

Host: A host is the name or network address of the physical or virtual device where an event or metric originated.

Source: A source is the name of the file, directory, data stream, or other input from which an event or metric originated.

Source types: Source types are unique classifications for data sources, which can either be well-known formats or user-defined. Source types tell Splunk how the incoming event or metric data is formatted, so that it knows how to parse the data into meaningful fields.

Fields: Fields are searchable name and value pairings that are extracted from event data.

Indexes: Indexes are discrete databases on the Splunk platform where event or metric data is stored.

Apps: Apps are collections of configuration settings, knowledge objects, views, and dashboards, which combine to extend the native capabilities of the Splunk platform. The most common purpose for an app is to add product or platform integration, which doesn't exist out of the box in Splunk.

Dashboards: Dashboards are static or interactive web views within Splunk, made up of panels that contain visualization or data filtering modules. Dashboards are used to display the results of search queries in different visual formats.

Search Processing Language (SPL): SPL is a query language, made of a series of search commands and arguments, that is used to filter and transform data returned from Splunk Indexes.

## Creating Scripted Inputs

As mentioned earlier, this tutorial will show you how to create a custom scripted input in Splunk Enterprise so that you can gather data from a remote system and transform it (if necessary) into an appropriate format that Splunk Enterprise can parse into event data. The possibilities are nearly limitless here; anything that you can script, using a shell language (like Bash or PowerShell) or the Python programming language, can become a data input.

Scripted inputs operate on a timed interval basis; you create a script that obtains and outputs event or metric data, and then you schedule it to run at a specified interval or as a scheduled cron task. The script file or files that you create will be stored on the Splunk Enterprise server (or on a distributed forwarder if you choose that method) in either the $SPLUNK_HOME/bin/scripts or $SPLUNK_HOME/etc/apps/<app_name>/bin directory.

Note: The location of the Splunk Enterprise installation directory (stored in the $SPLUNK_HOME environment variable) depends on the operating system on which it is installed. In this tutorial, we're demonstrating Splunk Enterprise installed on an Ubuntu Linux 22.04 server, where the default installation directory is /opt/splunk.

When you create a scripted input, you will be prompted for a few bits of information:

The location of the script file; it must already be uploaded to the Splunk Enterprise server

The script name; a drop-down picker will automatically populate with scripts found

The script command; in the case of Python, this is just the name and location of the script

The time interval to run the script on; you can choose In Seconds or Cron Schedule

<img width="781" height="516" alt="Screenshot 2026-06-02 151632" src="https://github.com/user-attachments/assets/4ea87566-4d8a-4e34-a70d-fab04f959938" />

In the next step of the wizard, you'll be prompted to configure the following items:

A source type for your input data; you can choose an existing source type or create a new one.

An app context; in other words, where should Splunk Enterprise store any configuration data for your scripted input?

A host field value; which host is this data coming from?

An index database in which to store the event data; you can choose an existing index or create a new one.

<img width="618" height="515" alt="Screenshot 2026-06-02 151647" src="https://github.com/user-attachments/assets/f9d75a41-a57b-4bbe-9b00-79b9f835a785" />

## Understanding The Splunk Enterprise Install Environment

Splunk Enterprise Directory

Let's take a closer look at the installation directory of Splunk Enterprise on an Ubuntu Linux v22.04 server (which is located in the /opt/splunk directory):

<img width="1165" height="335" alt="Screenshot 2026-06-02 152144" src="https://github.com/user-attachments/assets/104b572a-5967-4233-b54a-9164c7190b0e" />

There are a few things going on in there, but here are the important directories that you should be familiar with:

/opt/splunk/bin

This directory contains the executable files and scripts that Splunk uses to run. The most important executable file in this directory is /opt/splunk/bin/splunk; this is the platform's entry point and your primary CLI tool.

Some uses of the splunk executable are:

/opt/splunk/bin/splunk start|stop|restart: Used to start, stop, or restart the Splunk service

/opt/splunk/bin/splunk cmd <command>: Used to execute CLI commands (or run scripts) as the Splunk service

/opt/splunk/bin/splunk help: Provides help documentation on how to use this CLI command

Custom scripted inputs can be placed in the /opt/splunk/bin/scripts directory.

/opt/splunk/var/log/splunk

The Splunk log files live in this directory. The primary log file is /opt/splunk/var/log/splunk/splunk.log, which is where you'll want to look first when troubleshooting most problems. Splunk apps can also create their own independent log files in this directory.

/opt/splunk/etc/apps

Any installed Splunk applications are stored in this directory. It is also where any custom applications that you build should be located.

Custom scripted inputs can also be placed in a unique subdirectory under this directory, whenever you create a new custom application (/opt/splunk/etc/apps/<your_app>). Normally, you would want to use this approach if your scripted input requires additional configuration (.conf) files.

<img width="1153" height="95" alt="Screenshot 2026-06-02 152601" src="https://github.com/user-attachments/assets/23e8d343-7d89-43c7-a069-0b40c5cd9125" />

Your Ubuntu Linux 22.04 server has Python v3.10.12 installed globally, and it is located at /usr/bin/python3. What if Splunk Enterprise is using that same installation of Python as well?

<img width="1142" height="94" alt="Screenshot 2026-06-02 154921" src="https://github.com/user-attachments/assets/dc8f7472-319f-474a-9d92-858093186d0d" />

<img width="1165" height="67" alt="Screenshot 2026-06-02 154608" src="https://github.com/user-attachments/assets/2d26dd6c-d325-4231-b47f-355ab1c1f6a6" />

There are different sets of Python packages installed in different places! This is very important to keep in mind, for two reasons:

Python scripts that are executed by Splunk Enterprise will be run using Python v3.9.25, which is packaged along with the Splunk Enterprise installation files.

Any external packages that you use in your script will need to be included with the Python v3.9.25 installation, packaged with Splunk Enterprise.

## Working With REST API

