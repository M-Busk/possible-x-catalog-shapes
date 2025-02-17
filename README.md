# POSSIBLE-X Wizard Shapes

This repository contains the XFSC Self-Description Wizard schemas for service offerings and participants that are used
in the POSSIBLE-X project.

It contains the necessary build files to build the XFSC Self-Description Wizard API with these shapes preloaded.

## Structure

```
├── catalog-shapes/shacl
│   ├── ontology                    # ontology files for the catalog
│   ├── shapes                      # shape files for the catalog
│   │   ├── gx                      # shapes based on Gaia-X (Tagus + partially Loire)
│   │   └── px                      # POSSIBLE-X shapes that extend the respective Gaia-X shapes
├── sd-creation-wizard-api          # XFSC Self-Description Wizard API
```
