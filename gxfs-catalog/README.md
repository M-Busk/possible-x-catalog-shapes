# XFSC Federated Catalogue
This folder contains the build files for the MERLOT-adapted [XFSC Federated Catalogue](https://gitlab.eclipse.org/eclipse/xfsc/cat/fc-service.git) as well as the patches that are used for the MERLOT specific changes.

## Patches

### truncate_schemas.patch
In the original catalog the shapes and ontologies of the catalog would only be initialized if the database was not initialized yet. Since we want our build pipeline to always use the latest shapes from the `catalog-shapes` folder, this patch will truncate existing schemas in the database and always replace them with the shapes and ontologies from this repository.

### optional_registry.patch
This patch allows to disable the trust anchor registry check in the catalog that gets performed by the catalog after verifying the signature. It can be enabled by setting the `FEDERATEDCATALOGUE_VERIFICATION_TRUSTANCHORURL` parameter to an empty string. Furthermore the `FEDERATEDCATALOGUE_IGNORESSL` can be set to true to also disable checking for proper SSL certificates when resolving a given did:web.

Both of these parameters are necessary for local development where the did:webs neither have a valid SSL certificate nor are they in any trust anchor registry.

### ignore-compliance-signature.patch
This patch disables the signature (verificationMethod) validation for credentials of type `gx:compliance` and `gx:legalRegistrationNumber`. This is neccessary if the Tagus release of the clearing house is used as it uses a custom implementation of the JsonWebSignature2020 standard which is incompatible with the "proper" implementation that is used for validation in the catalog.

### ignore-compliance-claims.patch
This patch blocks the import of claims from credentials of type `gx:compliance` into the graph database. This is necessary as the catalog claims graph is based on IDs and claims from the Credential Subject (CS) of each credential, whereas the compliance credentials are referencing IDs of the Verifiable Credential (VC) which is one layer above. This creates a discrepancy which would let the catalog fail to import a given self-description.
