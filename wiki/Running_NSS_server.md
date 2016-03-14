---
title: Running NSS server
permalink: wiki/Running_NSS_server/
layout: wiki
---

This page explains how to run NovaSearchServices server for feature
extraction.

Running the server
==================

Preparing configuration file
----------------------------

Create or copy a template a configuration file with the desired services
and their parameters.

A template with some analysers instanced with "sane" defaults is
available at
`/localstore/searchservices/code/searchservices/template.json`. You may
change the parameters and add more analyser instances, but make a copy
of this file before editing.

Full list of available base analysers is available
[here](/wiki/NovaSearchServices#Analyser "wikilink").

The instances can have any desired name, as long as it is unique on this
template file and different from the [base
classes](/wiki/NovaSearchServices#Analyser "wikilink")

The configuration file is a JSON file in the following format:

    // Note, all numbers are defined as strings in the JSON. The C++ cast the string to the appropriate type internally
    {"parameters": {
        // Port for the server. 9383 is the default on the cluster servers
        "port" : "9383" 
        },
     "endpoints": {
        "analyser": [
           {
                // Name of the analyser/extractor instanced with the selected parameters.
                // Use this name when calling the index on the REST services (e.g. ExtractFeatures).
                "newName": "sift0", 

                // Analyser/extractor class name. The available base classes are hardcoded into the code, but new ones may be added in the future.
                "originalName": "sift",

                // Set of parameters for this analyser instance
                // For more information regarding the necessary parameters for instantiation see the template file.
                "params": { 
                    "nFeatures": "0", 
                    "nOctaveLayers": "4",
                    "contrastThreshold": "0.04",
                    "edgeThreshold": "10",
                    "sigma": "1.6"
                }
            },{
                "newName": "gaborFace",
                "originalName": "gaborExtractor",
                "params": {
                    "imageW": "92",
                    "imageH": "112",
                    "nScales": "4",
                    "nOrientations": "6",

                    "minWaveLength": "3",
                    "mult": "2",
                    "sigmaOnf": "0.65",
                    "dThetaOnSigma": "1.5",
                    "rectangles": "0,0,46,64;46,64,46,48;46,0,46,64;0,64,46,48;0,10,92,30;20,65,52,30"
                }
            }
            (...)
        ]
      }
    }

Preparing the environment
-------------------------

Before compiling and running, you may need to add the following
libraries folders to the env. vars. On the cluster server you may run or
add to your startup scripts:

     export LD_LIBRARY_PATH=/localstore/searchservices/libs/lib:$LD_LIBRARY_PATH && export LIBRARY_PATH=/localstore/searchservices/libs/bin:$LIBRARY_PATH && export C_INCLUDE_PATH=/localstore/searchservices/libs/include:$C_INCLUDE_PATH && export CPLUS_INCLUDE_PATH=/localstore/searchservices/libs/include:$CPLUS_INCLUDE_PATH && export LD_LIBRARY_PATH=/usr/lib/jvm/java-7-oracle/:$LD_LIBRARY_PATH && export LD_LIBRARY_PATH=/usr/lib/jvm/java-7-oracle/jre/lib/amd64/server/:$LD_LIBRARY_PATH 

Also, to extract CEDD and FCTH features, the Lire server must be
running. The service should already be running on all machines, and
extraction works if you use the template file parameters.

See the `startLire.sh` script at `/localstore/searchservices/code/lire`
and copy the folder to your machine if you want to deploy locally.

Running the server
------------------

Run the server as:

    ./bin/Release/server <JSON config file>

Calling the server
==================

Simple REST feature extraction
------------------------------

This service extracts the features for a single image and returns the
results through REST.

### Sample url

[`http://localhost:9383/analyserSingleFile?url=/localstore/searchservices/code/searchservices/configs/template.jpg&extractor=sift0`](http://localhost:9383/analyserSingleFile?url=/localstore/searchservices/code/searchservices/configs/template.jpg&extractor=sift0)

### Endpoint

[`http://`](http://)<server>`:`<port>`/analyserSingleFile?url=`<path>`&extractor=`<analyser>

**server:** server address (e.g. localhost)

**port:** server address (e.g. 9383)

### Parameters

**path:** path to the image file.

**analyser:** features to extract. Use the "newName" from the template
file.

### Output

The output format is a JSON file with the result of the request.

If the operation was successful, the field *status* will have the value
**ok**, and the features will be on *result*. The format of the output
is dependent on the type of the features (nVector, ...). See the details
below,

The *type* field indicates the output type (**nVector**, **nKeypoint**
or **nRoi**).

If the operation was unsuccessful, the field *status* will have the
value **error**. Check the *message* field or the server log for more
details.

-   **nVector** result format

The *result* field will be a JSON array with the feature values:

    {"result":[0.442748,0.069965, ... ,0.097223],"type":"nVector"}

-   **nKeypoint** result format

The *result* field will be a JSON array with the detected points and
corresponding features. Each point was the coordinates (*x*,*y*),
features as a JSON array (*features*), angle and other point metadata.

To use for Bag-of-words or Fisher vectors, extract the *features* array
for each point in results.

    {
        "result":[
            {"angle":266,"class_id":-1,"features":[30.0,1.0,...,3.0],"octave":10682624,"response":0,"size":3.89,"x":343,"y":388},
            {"angle":270,"class_id":-1,"features":[14.0,3.0,...,1.0],"octave":15270144,"response":0,"size":4.08,"x":316,"y":389}
            ...
        ]
    }

-   **nRoi** result format

The *result* field will be a an array of JSON fields, each with the
rectangle coordinates, size and types:

    {
        "result":[
            {"type":Face","x":343,"y":388,"width",20,"height",20},
            {"type":Face","x":123,"y":544,"width",24,"height",24},
            ...
        ]
    }
