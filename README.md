# json-ld-prototypes

**Prototypes for JSON-LD metadata (DESC Hack Week)**.

## Resources

- [json-ld.org](http://json-ld.org). Homepage for the JSON-LD spec.
- [JSON-LD 1.1 Spec](http://json-ld.org/spec/latest/json-ld/). Specifies the format of JSON-LD.
- [JSON-LD API Spec](https://www.w3.org/TR/json-ld-api/) describes how JSON-LD objects can be processed (for example, expanded, compacted, flattened).
- [github.com/codemeta/codemeta](https://github.com/codemeta/codemeta). A minimal JSON-LD schema for scientific software repositories.

  - [CodeMeta Developer Guide](https://github.com/codemeta/codemeta/blob/master/developer-guide.md): orientation for developing against the codemeta context.
  - [CodeMeta concepts](https://github.com/codemeta/codemeta/blob/master/codemeta-concepts.md): documents each field in the codemeta context.
  - [CodeMeta context](https://github.com/codemeta/codemeta/blob/master/codemeta.jsonld).
  - [CodeMeta schema](https://github.com/codemeta/codemeta/blob/master/codemeta-json-schema.json), compatible with [JSON Schema](http://json-schema.org) (see the [jsonschema](https://github.com/Julian/jsonschema) python package).

## Notes/Questions

### Misc.

- Is it possible to *extend* a JSON-LD schema without having to copy it? For example, add additional fields to `codemeta.jsonld` to support internal LSST metadata. Given the [spec page](http://json-ld.org/spec/latest/json-ld/#the-context), it seems that we'll have to copy `codemeta.jsonld` in order to extend it for additional fields.
- CodeMeta uses http://schema.org/name but it might be nice to use http://schema.org/familyName and http://schema.org/givenName. How would this work? Add `familyName` and `givenName` to the context, but ensure that `familyName` and `givenName` are synced to `name` server-side.

### Organizations

How pedantic should we be about organizations? schema.org allows sub-organizations (https://schema.org/parentOrganization) so that in principle we could create a tree of organizations in the `agents` field. For example, we can do AURA -> LSST -> DM -> SQuaRE. This *could* be enable users to browse projects by their sponsoring organization. Alternatively, a direct field could be used instead of presenting a hierarchy. Or place organizations in tags?

### Artifact relationships

The `relationships` codemeta field can be used to specify supersets of repositories. For example,

```
"relationships": {
    "relationshipType": "isPartOf",
    "relatedIdentifier": "urn:uuid:F1A0A7AF-ECF3-4C7D-B675-7C6949963995",
    "relatedIdentifierType": "UUID"
},
```

[PROV Entity](http://www.w3.org/TR/prov-o/#Entity) describes possible `relationshipType` values.

Relationships can also be used to describe releases of a software repository.
