# OSPREY-manual-RDF-links
links to external RDF resources that haven't been committed to the OSPREY database

This file is served at: http://www.bco-dmo.org/rdf/dumps/bcodmo-matched.rdf
* made available through a VoID document: http://www.bco-dmo.org/.well-known/void

## Annotations

Annotations should always have:

1. `@type: odo:Annotation`
2. `schema:author` pointing to the ORCID of the annotation's author
3. `schema:dateCreated` for the annotation was created
4. At least one of either `odo:asserts` or `odo:refutes`.
5. The `@type` of all assertions and refutations should be `prov:Revision`
6. Every `prov:Revision` requires a `prov:entity` property for identifying the single entity about which an assertion or refutation will be made.
7. Every `prov:Revision` requires at least one or more statement(s) that are being asserted or refuted by the annotation's author.
8. Optionally, a `prov:Revision` may have an `rdfs:comment` for declaring 

### Asserting a statement that does not exist

<pre>
{
  "@context": {
    "odo": "http://ocean-data.org/schema/",
    "prov": "http://www.w3.org/ns/prov#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "schema": "http://schema.org/",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@type": "odo:Annotation",
  "schema:author": { "@id": "https://orcid.org/0000-0003-1023-6239" },
  "schema:dateCreated": "2020-07-01T15:01:34Z"
  "odo:asserts": [
    {
      "@type": "prov:Revision",
      "prov:entity": { "@id": "http://lod.bco-dmo.org/id/dataset-parameter/8956" },
      <strong>"odo:hasNoDataValue": ["NaN", "-99999", "nd"],</strong>
      "rdfs:comment": "This dataset parameter uses one of 'Nan', '-99999', or 'nd' as its no data value"
    }
  ]
}
</pre>

#### Asserting multiple statements about a single entity

<pre>
{
  "@context": {
    "odo": "http://ocean-data.org/",
    "prov": "http://www.w3.org/ns/prov#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "schema": "http://schema.org/",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@type": "odo:Annotation",
  "schema:author": { "@id": "https://orcid.org/0000-0003-1023-6239" },
  "schema:dateCreated": "2020-07-01T15:01:34Z"
  "odo:asserts": [
    {
      "@type": "prov:Revision",
      "prov:entity": { "@id": "http://lod.bco-dmo.org/id/dataset-parameter/8956" },
      <strong>(1) "odo:hasNoDataValue": ["NaN", "-99999", "nd"],
      (2) "odo:requiresConversion": {"@value": true, "@type": "xsd:boolean"}</strong>,
      "rdfs:comment": "This dataset parameter uses one of 'Nan', '-99999', or 'nd' as its no data value, and it requires conversion to community accepted standard units."
    }
  ]
}
</pre>

### Refuting an existing statement

```
{
   "@context": {
    "odo": "http://ocean-data.org/",
    "prov": "http://www.w3.org/ns/prov#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "schema": "http://schema.org/",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@type": "odo:Annotation",
  "schema:author": { "@id": "https://orcid.org/0000-0003-1023-6239" },
  "schema:dateCreated": "2020-07-01T15:01:34Z"
  "odo:refutes": [
    {
      "@type": "prov:Revision",
      "prov:entity": { "@id": "http://lod.bco-dmo.org/id/dataset-parameter/8956" },
      "odo:hasNoDataValue": ["0"],
      "rdfs:comment": "This dataset parameter does not use '0' as a no data value"
    }
  ]
}
```

### Refuting and Asserting in the same Annnotation

<pre>
{
   "@context": {
    "odo": "http://ocean-data.org/",
    "prov": "http://www.w3.org/ns/prov#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "schema": "http://schema.org/",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@type": "odo:Annotation",
  "schema:author": { "@id": "https://orcid.org/0000-0003-1023-6239" },
  "schema:dateCreated": "2020-07-01T15:01:34Z"
  <strong>"odo:refutes"</strong>: [
    {
      "@type": "prov:Revision",
      "prov:entity": { "@id": "http://lod.bco-dmo.org/id/dataset-parameter/8956" },
      "odo:hasNoDataValue": ["0"],
      "rdfs:comment": "This dataset parameter does not use '0' as a no data value"
    }
  ],
  <strong>"odo:asserts"</strong>: [
    {
      "@type": "prov:Revision",
      "prov:entity": { "@id": "http://lod.bco-dmo.org/id/dataset-parameter/8956" },
      "odo:hasNoDataValue": ["NaN", "-99999", "nd"],
      "odo:requiresConversion": {"@value": true, "@type": "xsd:boolean"},
      "rdfs:comment": "This dataset parameter uses one of 'Nan', '-99999', or 'nd' as its no data value, and it requires conversion to community accepted standard units."
    }
  ]
}
</pre>
