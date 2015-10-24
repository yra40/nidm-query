# NIDM Query Repository
NIDM specifies Object Models that are used to capture provenance and relevant metadata about neuroimaging studies using Semantic Web technologies. NIDM documents are expressed using [RDF][rdf] and queried using [SPARQL][sparql]. While not always intuitive, SPARQL is a powerful language to extact information from RDF graphs and provide formats that are more traditional to work with (e.g., a csv file). The collection of queries in this repo provides users of NIDM with ready to use examples that can be executed directly or tweaked for your specific use.

To document and help with query reuse, we define a set of metadata about each query as a JSON document, like the example below.

```
{
  "@context": "http://raw.github.com/incf-nidash/nidm-query/mastercontext.jsonld"
  "title": "Query Title",
  "description": "Query description.",
  "query_type": "Select",
  "nidm_model": "NIDM-Results",
  "query": "SELECT * WHERE {?s ?p ?o .}"
}
```

[rdf]: http://www.w3.org/RDF/
[sparql]: http://www.w3.org/TR/rdf-sparql-query/
