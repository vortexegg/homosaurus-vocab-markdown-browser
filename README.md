# Homosaurus Vocab Markdown Browswer

This is a Python notebook that converts the [Homosaurus v5 vocabulary](https://homosaurus.org/v5) into markdown files for browsing in an Obsidian vault.

Input to the script is a [Turtle](https://en.wikipedia.org/wiki/Turtle_(syntax)) (Terse RDF Triple Language) .ttl file that uses a SKOS (Simple Knowledge Organization System Namespace Document) linked data vocabulary. The contents of the file is itself a data dictionary for a controlled vocabulary. Each element in the .ttl file corresponds to a Homosaurus vocabulary term and its associated metadata.

The goal of this notebook is to read in the .ttl file and convert each of the vocab term elements into a markdown file with the file name taken from the English preferred name (`skos:prefLabel` tagged with `@en` suffix), certain of the metadata elements stored as yaml frontmatter elements (TBD), and the english description stored as the markdown file body (`rdfs:comment` tagged with `@en` suffix). Finally these will be emitted as markdown files in a folder that can be opened separately as an Obsidian vault, preprocessed so that it is ready to load.

One complexity is that we want to retain hyperlinks between the controlled vocab terms and structurally related terms (e.g. `skos:broader`, `skos:hasTopConcept`, etc). The .ttl file includes links to the _identifiers_ of these terms, but we want to store our Markdown files using the filename of the common preferred name. The script will also need to do a translation step where it replaces each of identifiers of the linked terms with a [[wikilink]] link to the preferred name of that term (the markdown file name).

## Fields

This is a suggested set of fields that will be retained and where the are placed in the resulting markdown file.

```text
Convert to file name:
skos:prefLabel (@en only)

In frontmatter:
URL
dc:identifier

In body:
rdfs:comment (@en only)
skos:altLabel (@en only)

Links (these can be in the body):
skos:broader
skos:narrower
skos:related

The URL is at the top of each item followed by "a skos:Concept;"
```
