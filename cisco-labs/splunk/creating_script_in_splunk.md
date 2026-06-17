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

While a deep dive on REST API functionality is beyond the scope of this tutorial, here are some of the basics.

REST is an architectural style that provides standards for how computer systems should communicate with each other and share information over the internet (or any IP computer network). It was designed to be scalable so that it could be used effectively on a network as large as the internet. REST communications are designed to be "stateless,” meaning that there are no long-lived open communication sessions between clients and servers. A request goes out, a response is sent back, and the connection closes.

An API is an intermediary software system that allows computer programs to talk to each other. Often, an API acts as a translator between two computer programs that don't speak the same language -- like a web browser and a Structured Query Language (SQL) database. An API server exposes various endpoints that API clients can communicate with; each endpoint provides a basic service or handles a specific type of request.

### CRUD Method

So REST is an architectural concept, and APIs are software programs ... but neither provides a protocol for communication across a network. How do clients and servers talk to each other? The answer is the HTTP protocol. REST-based API servers and their clients communicate with each other using HTTP messages (more often than not, using the encrypted HTTPS protocol).

<img width="850" height="450" alt="Screenshot 2026-06-09 140324" src="https://github.com/user-attachments/assets/12fc4fe9-2067-4b06-8152-e9856dd7628f" />

### HTTP Headers and Payloads

<img width="1102" height="317" alt="Screenshot 2026-06-09 140626" src="https://github.com/user-attachments/assets/859aa5cf-0663-4ee6-b40b-c69d68b17915" />

The payload of an HTTP message would be like the content of the letter in our metaphorical envelope. The information that is contained in the HTTP header tells you which format that you should expect the content of the letter to be in; it could be plaintext, JavaScript Object Notation (JSON), or XML structured data, or it could even be an encoded file. When working with REST APIs, the most common payload data format will be JSON, which is composed of nested sets of arrays (called lists in Python) and key-value pairs (called dictionaries in Python).

For example, here’s the data that is returned by sending a GET request to https://httpbin.org/json:

<img width="1213" height="596" alt="Screenshot 2026-06-09 140937" src="https://github.com/user-attachments/assets/890b946f-6bbd-4e65-94c3-f603a7bfa121" />

Although we're looking at this JSON data payload in a nice, human-readable format with lots of whitespace, new lines, and indentation, it is important to remember that the actual raw payload data in an HTTP message will be just a string of unformatted text, such as this:

{\n  "slideshow": {\n    "author": "Yours Truly", \n    "date": "date of publication", \n    "slides": [\n      {\n        "title": "Wake up to WonderWidgets!", \n        "type": "all"\n      }, \n      {\n        "items": [\n          "Why <em>WonderWidgets</em> are great", \n          "Who <em>buys</em> WonderWidgets"\n        ], \n        "title": "Overview", \n        "type": "all"\n      }\n    ], \n    "title": "Sample Slide Show"\n  }\n}\n

By inspecting the Content-Type header of the response message, you can determine in which format this string of text was created. You can then use whichever tools are at your disposal to render that string of text in a more readable format. For instance:

<img width="1212" height="805" alt="Screenshot 2026-06-09 141142" src="https://github.com/user-attachments/assets/6da3f5d4-4f58-4bfc-87c0-afbfe5254cf7" />

## Getting Started with API
When writing your scripted input for Splunk Enterprise, you can choose any data source from which you'd like to gather information. For this tutorial, we are using the "Catalyst Center Always-On v2.3.3.6" sandbox lab that is available from the Cisco DevNet Sandbox.
Cisco Catalyst Center (Formerly known as Cisco Digital Network Architecture (DNA) Center) is a centralized management application for the network. Cisco Catalyst Center provides a single pane of management to design, provision, enable policy, and assure network services with full visibility of user and device identity, operating systems and applications across the entire network fabric.

### Cisco Catalyst Center allows you to manage the enterprise network over a centralized dashboard and deploy networks in minutes, not days, using intuitive work flows. The Cisco Catalyst Center Sandbox provides the developer the ability to design, develop and test utilizing the Cisco Catalyst Center development platform with a sample Sandbox Lab Topology.

This sandbox consists of a virtualized Controller and a real hardware sample network topology containing network elements and hosts that developers can utilize so they can develop, debug and test their sample Cisco Catalyst Center application.

In this sandbox, developers can:

Interact with the Cisco Catalyst Center API calls using a variety of REST clients such as POSTMAN or CURL.
Develop and test applications for Cisco Catalyst Center.

Note: In the following examples, we'll be using the Python Requests package to send HTTP messages to an API. Requests is an open-source Python package that does not come with a standard Python installation, so you must download it from the internet (although it is provided with an installation of Splunk Enterprise). You can use the pip package manager that comes with Python to download and install the package. Simply run the command pip install requests.

The Catalyst Center API uses the HTTP basic authentication method to verify the identity of the user, and the resulting JSON Web Token (JWT) that you receive is used in all subsequent API transactions. HTTP basic authentication works like this:

An HTTP message is created, using the POST method.

The Authorization header is added to this HTTP message.

The user provides a username and password for a user account that has permission to access the API.

The username and password are joined together in a single string, separated by a colon -- for example, devnetuser:Cisco123!.

The resulting username:password string is then encoded using Base64.

Note: Base64 is not an encryption method; it is simply an "obfuscation" encoding scheme, which is easily reversible. Base64 does not protect your username and password. Instead, rely on the TLS encryption that is provided by HTTPS to protect the contents of your HTTP message.

<img width="793" height="229" alt="Screenshot 2026-06-09 155711" src="https://github.com/user-attachments/assets/c75cf4a1-7ba0-455d-9143-b636305c2b85" />


Finally, the Base64 encoded username and password string are combined with a keyword, indicating the type of authentication method being used, and the resulting value is placed in the Authorization header: Authorization: Basic ZGV2bmV0dXNlcjpDaXNjbzEyMyE=.

When you combine all this together with a few other parameters that are detailed in the Authentication API documentation, and then send your HTTP message to the Catalyst Center API, you should receive a token in return:

<img width="1093" height="239" alt="Screenshot 2026-06-09 160957" src="https://github.com/user-attachments/assets/912f7c93-c14d-4490-80ae-312d29546a0f" />

Now that you have your authentication token from Catalyst Center, which is valid for 1 hour, you can use it to send additional API requests to the system. All subsequent API requests to the Catalyst Center API will need to include this token in a special custom header named x-auth-token, and you can remove the Authorization header completely. For example:

<img width="1086" height="522" alt="Screenshot 2026-06-09 161704" src="https://github.com/user-attachments/assets/47ce8623-b7fc-4d55-833b-8c18d2faffae" />

We have truncated the output from that API response because it's huge, but look at what was accomplished with a very small amount of Python code. We authenticated to the Catalyst Center API, received a short-lived authorization token, and requested a list of all the sites that exist in this Catalyst Center deployment ... all with just 13 lines of code!

## Collecting Compliance Status from Catalyst Center
In the previous topic, we authenticated to the Catalyst Center API, obtained a temporary JWT for authorization, and made our first informational request API call. So we're experts now, right? Actually, there really isn't much more to a simple Python script that communicates with an API interface! We may not be experts, but we're well on our way to completing this project.

Let's continue by figuring out what is the information that we want to pull from Catalyst Center and insert into a Splunk index. We will want some kind of event data that changes periodically, which will require us to keep checking in on it. A good, simple example to start with is compliance status for devices in the Catalyst Center inventory, and for that, let’s use the Get Compliance Detail API endpoint.

### Get Compliance Detail API

The URL for this API endpoint on any Catalyst Center appliance is https://<catc_ip_or_dns>/dna/intent/api/v1/compliance/detail, and the HTTP method it uses is GET. There are a few optional query parameters that you can use with this API endpoint as well (allowing you to filter the returned results):

complianceType

complianceStatus

deviceUuid

offset

limit

Query parameters are added to the end of the URL, following a question mark, and multiple parameters can be strung together with ampersands (&). For example:

"https://IP_address_of_Catalyst_Center/dna/intent/api/v1/compliance/detail?complianceType=NON_COMPLIANT&limit=50"

You also need to include the necessary HTTP headers in your request:

Content-Type: application/json

x-auth-token: <our_token_from_authentication>

<img width="1022" height="283" alt="Screenshot 2026-06-10 013511" src="https://github.com/user-attachments/assets/71d30a66-f760-4622-a334-1d3f6e3125b8" />

<img width="1025" height="639" alt="Screenshot 2026-06-10 013535" src="https://github.com/user-attachments/assets/b088b362-e014-4235-8549-28b141cf1b65" />

<img width="998" height="277" alt="Screenshot 2026-06-10 013618" src="https://github.com/user-attachments/assets/4d6f34c1-cd8b-4c35-9b3f-5d307cc20cdd" />

### Enrichinbg the data

The output that we get from the "Get Compliance Details" API is excellent—almost exactly what we need. However, there's one minor hang-up: The device universally unique identifier (UUID) isn't as helpful as the device hostname, for instance. While we could easily take this JSON response data and add it to our Splunk index, anyone who is looking at the data afterward would need to perform an additional lookup to match the UUID to the device hostname or management IP address.

So, how can we solve this problem? One method would be to make an additional API call to Catalyst Center to perform a lookup of the device's details, based on each UUID. Although this approach would work, it could result in a lot of additional API calls to make. Suppose that you had 500 compliance status items from the previous API call; you'd need to make as many as 500 additional API calls to get the hostname for each one.

There is a better way, though, which we'll describe in more detail in the upcoming topics. Because UUIDs don't change, and your Catalyst Center inventory will change very infrequently, you can actually make a single API call to obtain all the device details and then store that information in a local file, which you can use for lookups later on.

The API endpoint that we'll use for performing this device lookup is Get Device List (https://<catc_ip_or_dns>/dna/intent/api/v1/network-device), using the GET method. We'll need to include our required HTTP headers again:

<img width="1213" height="243" alt="Screenshot 2026-06-10 014928" src="https://github.com/user-attachments/assets/333306e1-f965-43a5-b41a-7c1fddbcaab0" />

<img width="1222" height="638" alt="Screenshot 2026-06-10 014956" src="https://github.com/user-attachments/assets/c6a4e889-d6aa-4b52-ae2b-8deed1fc74fb" />

<img width="1223" height="665" alt="Screenshot 2026-06-10 015020" src="https://github.com/user-attachments/assets/7547385b-9576-4165-b694-c0dc741fac63" />

<img width="1220" height="684" alt="Screenshot 2026-06-10 015053" src="https://github.com/user-attachments/assets/e1eedfd0-4b30-4744-9c32-577b0b10c301" />

<img width="1225" height="683" alt="Screenshot 2026-06-10 015114" src="https://github.com/user-attachments/assets/f641ac0d-0167-4ed2-a52e-83675d7ca039" />

<img width="1221" height="679" alt="Screenshot 2026-06-10 015139" src="https://github.com/user-attachments/assets/75c56f15-c029-402d-a534-7a8ab6848ef9" />

<img width="1217" height="677" alt="Screenshot 2026-06-10 015205" src="https://github.com/user-attachments/assets/5a6fbbe5-f52e-4817-bcdd-4f44443f16e9" />

<img width="1213" height="269" alt="Screenshot 2026-06-10 015227" src="https://github.com/user-attachments/assets/09beda4b-0be1-4a12-a58e-fa299570ac53" />

With this additional device information, you can create a local JSON file that contains just the bits that you need. We'll use Python dictionaries (aka key-value pairs) to store this information because dictionary lookups are much faster and more efficient than looping through a Python list (aka array). We'll get into more detail about how to do this in the upcoming topics, but here is an example of the JSON file format that you'll want to create:

## Creating the Inventory Lookup Python Script

### Built-in Packages:

os: Contains functions for interacting with the operating system where the script is running.

sys: Contains functions that can perform system-level actions on the operating system where the script is running.

json: Can read and write JSON-formatted data

### External Packages:

requests: Provides an easy-to-use interface for sending and receiving HTTP messages

<img width="1038" height="290" alt="Screenshot 2026-06-10 020457" src="https://github.com/user-attachments/assets/f57fe2cd-8f10-40ba-97fc-e84679def77f" />

### Authentication Function
Our first function should perform an authentication action with the Catalyst Center authentication API, and it should return the JWT, which is valid for 1 hour.

Typically, you would prompt the script's user for the username and password or read it from an environment variable in order to avoid storing those sensitive credentials on disk or exposing them to other system processes. Unfortunately, the design of Splunk Enterprise makes it rather difficult to do that; Splunk does provide a credential encryption system, but it requires significant effort to implement. To keep our scripted input project simple, we'll store the Catalyst Center API credentials inside our Python script, and we'll obfuscate (hide) them using Base64 encoding.

### Script Functions
Every good Python script should be broken into one or more functions, which are reusable blocks of code that perform a single task and return a single result (or set of results). This helps modularize your code and adheres to the “don’t repeat yourself” (DRY) principle.

It is also important to remember that when you use Python functions, they will not be executed by the Python interpreter as it parses the script, line by line, from the top down. It will reach the function, parse it, and store it in memory, but it will not execute that function until you have "called" it later in your script.



### Authentication Function
Our first function should perform an authentication action with the Catalyst Center authentication API, and it should return the JWT, which is valid for 1 hour.

Typically, you would prompt the script's user for the username and password or read it from an environment variable in order to avoid storing those sensitive credentials on disk or exposing them to other system processes. Unfortunately, the design of Splunk Enterprise makes it rather difficult to do that; Splunk does provide a credential encryption system, but it requires significant effort to implement. To keep our scripted input project simple, we'll store the Catalyst Center API credentials inside our Python script, and we'll obfuscate (hide) them using Base64 encoding.

Note: It is highly recommended that you create a special user account in Catalyst Center specifically for this script, with read-only access that is limited to just the areas of Catalyst Center necessary for this script to work.

<img width="1205" height="265" alt="Screenshot 2026-06-16 224502" src="https://github.com/user-attachments/assets/95e1e2d3-9858-4f19-9549-135035fab231" />

### Get Device List Function
The next function should make the API call to Catalyst Center to obtain all the details of devices in its inventory. We'll also add some logic to this function that will handle situations where the inventory is larger than 500 devices; 500 items is the maximum response size that the API endpoint is limited to.

<img width="1206" height="513" alt="Screenshot 2026-06-16 224534" src="https://github.com/user-attachments/assets/edbb6b60-55c9-4c6f-a1d9-c356e527ba36" />

Note: We are checking the length of the API response to see if it contains 500 or more inventoried devices. This can happen in large production systems, and the API is limited to a maximum of 500 results each time that you call it. So, we use a simple while loop to keep requesting inventory information, and each time, we add the length of the previous result to the offset query parameter. This is a simple pagination solution for REST APIs.

### Generate Simple Dictionary Function
Now that we have obtained all the inventory details from Catalyst Center, we'll need to go through them and extract only the information that we need for each device. The following function will loop over that inventory list and build a set of nested dictionaries, which will make it fast and easy to look up devices. For example:

uuid_1

hostname

serialNumber

managementIpAddress

platformId (Cisco PID)

uuid_2

hostname

serialNumber

managementIpAddress

platformId

<img width="1211" height="296" alt="Screenshot 2026-06-16 224605" src="https://github.com/user-attachments/assets/ba763d3f-9ead-4ee1-9dd7-28b0ff456316" />

### Write JSON File Function
The next part is quite simple: We'll first check if the neighboring directory lookups exists (a directory that exists at the same level as the current directory where this Python script resides), and we'll create one if it doesn't. Then, we'll open a JSON text file and write the contents of our nested dictionary to it.

The reason that we are storing this file in a neighboring directory named lookups is for the benefit of the Splunk Enterprise application directory structure. Splunk will expect any local lookup files to exist in that subdirectory (part of a custom application directory), so we'll adhere to that standard:

splunk:~$ tree /opt/splunk/etc/apps/my_app/
/opt/splunk/etc/apps/my_app/
├── bin
│   ├── create_device_lookup.py
│   ├── get_compliance_alerts.py
├── lookups
│   ├── device_inventory.json
├── default
├── local
├── metadata
├── README

<img width="1196" height="222" alt="Screenshot 2026-06-16 224736" src="https://github.com/user-attachments/assets/9d4ee515-1145-4dd3-a877-27c180d3c87e" />

### Main Function and Automatic Execution Statement
Finally, we'll create a main function that acts like a supervisor for all the other functions. It will execute them in a specific order and pass the necessary information between them. This function isn't really a requirement, but it is an accepted best practice when writing complex Python scripts, and it makes understanding and editing them easier for future developers.

<img width="1206" height="271" alt="Screenshot 2026-06-16 224809" src="https://github.com/user-attachments/assets/72fc0579-3986-41a4-968c-a49b239513ee" />

We will also add a simple but very useful if statement that serves one very important purpose: It causes the script to run automatically when it is executed directly from the Python interpreter. What exactly does that mean? Python scripts can be imported into other Python scripts very easily; it is one of the most important reasons for organizing your code into functions. When you do that, you can easily import one or more functions from a separate script, thereby saving yourself time. However, when you import one script into another, you don't want it taking off and running automatically on its own, so you need to add a little bit of logic that prevents this from happening except when you run that script directly.

That magic line of code is if  __ name __  ==  '__ main __':

## Creating Compliance Python Script
### Built-In Packages
datetime: Contains functions for reading the current system time and displaying it in various formats

<img width="1209" height="568" alt="Screenshot 2026-06-16 230925" src="https://github.com/user-attachments/assets/b1cbce78-1e6e-4c21-a604-54e290c5878f" />

Note: Remember to change the string value for the variable basic_auth_base64 in this script. You will need to generate the Base64 encoded string for the Catalyst Center API credentials that you will be using and store it in this variable.

Note: Here, we are using something called a "try/except block" in our script. The try/except block allows you to attempt something that you suspect may cause an error (which would make the script crash); if an error does occur, you can handle it gracefully without crashing the script. In this case, we're attempting to read the device lookup file, and if it doesn't exist, we will simply create an empty dictionary, which will allow the script to continue.

### Authentication Function
This function is identical to the one that we created in the previous topic, and it will return a temporary JWT that we can use for authentication for the next hour:

<img width="1200" height="260" alt="Screenshot 2026-06-16 230947" src="https://github.com/user-attachments/assets/bf576896-9560-4cb3-810b-dca659d0fe52" />

### Get Compliance status Function
The next function should make the API call to Catalyst Center to obtain the all the compliance status details for devices in its inventory. We will add the same logic to this function, which handles situations where the response is larger than 500 items. The returned data will look similar to this:

<img width="1185" height="577" alt="Screenshot 2026-06-16 231906" src="https://github.com/user-attachments/assets/3370734e-eb59-4f3a-88fc-580a0b13a38e" />

Notice that each compliance status item has a key named lastUpdateTime. That field is very useful because it tells you the timestamp of when this compliance status was last updated (represented in Unix time). If the compliance status hasn't changed since the last time it was checked, then there's no point in updating it or logging a new event in the Splunk index.

<img width="1299" height="440" alt="Screenshot 2026-06-16 231243" src="https://github.com/user-attachments/assets/222be935-e63d-4f02-b2ff-5a7789415d6f" />

### Get and Create Checkpoint Function
In addition to creating the device inventory JSON file in the lookups directory, we're also going to create a compliance checkpoints JSON file, and this function will read in that file for later comparison. Why would we do that?

When Splunk Enterprise receives events and parses them for insertion into an index (database), it never actually checks to see if there's a duplicate record already in place. You could easily end up filling your index with lots of duplicate events if you don't include some logic to weed them out. In the case of compliance status, each compliance type is checked on a regular basis by Catalyst Center, and if the status has changed since the last check, it will update the lastUpdateTime key with the latest timestamp. (Reminder: That timestamp is in Unix time.)

We will use that lastUpdateTime value to create a "checkpoint" for our script. Every time that the script runs, it will compare each compliance status to the timestamp saved in our checkpoint file. If the times match, then the script will pass over that item and not print out a new event for Splunk to index.

<img width="1311" height="197" alt="Screenshot 2026-06-16 231302" src="https://github.com/user-attachments/assets/31368f0b-d8c3-47b9-be3e-9ca6f26cea42" />

<img width="1297" height="157" alt="Screenshot 2026-06-16 231339" src="https://github.com/user-attachments/assets/3475c77e-0485-4d6e-8aeb-dd462146f22f" />

That checkpoint file will look similar to this:

<img width="1198" height="397" alt="Screenshot 2026-06-16 232256" src="https://github.com/user-attachments/assets/2d70200b-aa65-40f3-9198-cdd77a7b37a3" />

### Write Event Function
The next function is our largest yet -- and the most important function in this script. The write_events() function loops through all the compliance status data that we received from Catalyst Center. For each individual compliance status, the function performs three tasks:

1. Check whether the device that is being reported on exists in our local inventory file.

2. Check whether this compliance status exists in our local checkpoint file, and if it does, check if the lastUpdateTime timestamps match.

3. If the timestamps do not match, or the device doesn't exist in either the inventory or checkpoint file, then build a Splunk event message and print it to the standard output (STDOUT) interface.

<img width="1301" height="625" alt="Screenshot 2026-06-16 231406" src="https://github.com/user-attachments/assets/12e4bca0-8aff-448b-b1b6-9cb5ea174bf4" />

<img width="1294" height="233" alt="Screenshot 2026-06-16 231440" src="https://github.com/user-attachments/assets/6a42d266-d3c8-47f5-b0ae-51762eb46b13" />

### Main Function and Automatic Execution Statement
Finally, just like in the previous topic and script, we will create the same main function that acts like a supervisor for all the other functions. It will execute them in a specific order and pass the necessary information between them.

We will include the special if statement that triggers the script to automatically run whenever it is executed directly from the Python interpreter:

<img width="1295" height="216" alt="Screenshot 2026-06-16 231459" src="https://github.com/user-attachments/assets/b5161931-fc5f-4a6a-9770-17dd3bad7cb2" />

## Creating New Splunk App
### Create the Directory
Let’s move on to the next phase of our Splunk scripted input: creating a custom application. You might recall earlier in the tutorial that we said scripted inputs could be stored in one of two locations in Splunk:

$SPLUNK_HOME/bin/scripts

$SPLUNK_HOME/etc/apps/<your_app_name>

A simple scripted input would work just fine in the $SPLUNK_HOME/bin/scripts directory, but in our specific example, we're adding some enhanced features that will require us to create a custom application directory. Even so, there's really nothing special required to do that:

Log in to the web user interface of your Splunk Enterprise server.

Click the Apps menu in the upper-left corner of the web page.

Select Manage Apps from the menu.

Click the Create App button in the upper-right corner of the web page.

<img width="1194" height="726" alt="Screenshot 2026-06-17 000551" src="https://github.com/user-attachments/assets/910599d8-6197-4613-8f94-575751a70e56" />

In this case, I copied the two files into the /opt/splunk/bin/scripts directory instead of creating the tar file.

<img width="1051" height="340" alt="Screenshot 2026-06-17 133402" src="https://github.com/user-attachments/assets/5a0fd126-e681-4345-8079-4bff3b0b9555" />

### Create a Custom Source Type

<img width="1159" height="723" alt="Screenshot 2026-06-17 133933" src="https://github.com/user-attachments/assets/f590ba76-0d49-4537-ad03-c404a4a524c3" />

