# NIDM Query Repository

This repo contains static data structures (jsonld) each of which stores a query and associated meta-data for an NIDM Results, NIDM experiments, or NIDM workflow data structures. You should work with these data structures by way of the [nidm-api](https://github.com/incf-nidash/nidm-api).

Functions will be provided to do the following:

- perform a query on an NIDM turtle file, returning the format of your choice (text and graphical)
- a web interface to generate a new query to add to the database
- validation of query data structures


#### Organization
The folders are organized by the associated NIDM data structure. @vsoch moved some of these from @nnichols repo, and probably got some of them wrong, so please move them into the correct places. :) Higher level queries to return meta-data about the queries themselves will be taken care of by [nidm-api](https://github.com/incf-nidash/nidm-api).


#### Documentation

Documentation will be provided to answer the following questions:

##### How do I contribute a new query?
We will have a function in the [nidm-api](https://github.com/incf-nidash/nidm-api) executable to generate a new data structure. This will work via command line, or via a web interface for you to input fields for your structure. We recommend that you use the generation functions to ensure accuracy in the format and fields of your data structure. You can then add it to the repo by submitting a pull request to add it. A pull request affords group discussion, and we will eventually have continuous integration that will run tests on your new query.

#### How do I integrate queries into my application?
The [nidm-api](https://github.com/incf-nidash/nidm-api) is an executable, but is also a collection of functions organized around the different NIDM objects. You can easily import the same functions to perform the queries into your applications to use them without needing to get them via the REST API.

#### How do I use this as a REST API?
You have several options. By installing the [nidm-api](https://github.com/incf-nidash/nidm-api) you will have a command line tool to immediately serve a localhost version of the REST API.  You could easily run this executable on a server to provide it to a larger group of people. We will also (likely) find a place to serve this officially.

More documentation and details will come, for now it's time to code!

#### Background on Sparql
NIDM specifies Object Models that are used to capture provenance and relevant metadata about neuroimaging studies using Semantic Web technologies. NIDM documents are expressed using RDF and queried using SPARQL. While not always intuitive, SPARQL is a powerful language to extact information from RDF graphs and provide formats that are more traditional to work with (e.g., a csv file). The collection of queries in this repo provides users of NIDM with ready to use examples that can be executed directly or tweaked for your specific use.

To document and help with query reuse, we define a set of metadata about each query as a JSON document, like the example below.
An example structure is provided below:

      {
        "title": "T1 recon-all with freesurfer",
        "description": "Compute FreeSurfer recon-all for every T1 image in the given rdf file",
        "uid":"23ee1631-51a3-43c9-bd71-b02134d7e36a",
        "creator": "<http://orcid.org/0000-0003-1099-3328>",
        "keyword": "recon-all, freesurfer, T1",
        "model": "meta", 
        "parameters": ["?uri", "?t1_uri", "?task"],
        "sparql": ["PREFIX dcat: <http://www.w3.org/ns/dcat#>",
                   "PREFIX nidm: <http://purl.org/nidash/nidm#>",
                   "SELECT DISTINCT ?t1_uri ?task",
                   "WHERE {",
                     "?uri a nidm:MRIAnatomicalT1 ;",
                     "dcat:downloadURL ?t1_uri ;",
                     "dcat:format nidm:NIFTI1Gzip .",
                     "VALUES (?task) {('tasks.fs_reconall')}",
                     "}"],
        "reference": "",
        "@context":""
      }

You should not be creating these structures manually, please use the [nidm-api](https://github.com/incf-nidash/nidm-api)

