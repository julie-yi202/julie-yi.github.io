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

