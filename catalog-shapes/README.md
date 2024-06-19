# MERLOT Dataspace shape and ontology files
This folder contains all the shape and ontology files that are used within the MERLOT marketplace.

## Shapes

The shape files contain the description of the data structure of a particular type as well as what constrains lie on each field.

The `shapes` folder is split into the shapes based on the Gaia-X (Tagus + partially Loire) release in the `gx` folder
and MERLOT specific extensions of these shapes in the `merlot` folder.
Each of the folders contain the Participant and Service Offering shapes respectively. Ressources are currently not considered in MERLOT.

## Ontology

The ontology files contain the description of how a particular type is related to other types (e.g. that a MERLOT Legal Participant is a subclass of a Gaia-X Legal Participant).

The `ontology` folder is analogously separated into Gaia-X and MERLOT specific ontologies.
Both Gaia-X and MERLOT specific types are related back to the base classes that the XFSC catalog expects (gax-core:Participant and gax-core:ServiceOffering).

## Merge script

This folder also contains a `merge_shapes.py` script which is used by the build pipeline to combine all available shapes in the `shapes` folder into a single large `mergedShapes.ttl` file. This is done as the XFSC catalog expects such a single common shape file instead of individual files per type.