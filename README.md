# MERLOT XFSC FC Shapes
This repository contains the XFSC Federated Catalogue schemas for service offerings and participants that are used in the MERLOT marketplace.

It also contains the necessary build files to build the catalogue as well as the XFSC Self-Description Wizard API with these shapes pre-loaded.

## Structure

```
├── catalog-shapes/shacl
│   ├── ontology                    # ontology files for the catalog
│   ├── shapes                      # shape files for the catalog
│   │   ├── gx                      # shapes based on Gaia-X (Tagus + partially Loire)
│   │   ├── merlot                  # merlot-specific shapes based on the Gaia-X v22.10 shapes
├── gxfs-catalog                    # build files for the XFSC Federated Catalogue
├── sd-creation-wizard-api          # XFSC Self-Description Wizard API
```
