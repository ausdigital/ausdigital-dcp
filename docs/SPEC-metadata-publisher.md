# Metadata Publisher v1.0 ![draft](http://rfc.unprotocols.org/spec:2/COSS/draft.svg)

The [Ausustralian Digital Business Council](https://https://ausdigital.github.io/) provides open B2B standards for eInvoicing.

These require:

 - confidence in business identity.
 - common business semantics.
 - dynamic service discovery.


Those requirements are met by a component called the [Service Metadata Publisher](/SPEC-metadata-publisher/).

Implementations must provide a compliant interface. The [REST interface v1.0](https://swaggerhub.com/api/ausdigital/metadata-publisher/1.0) is drafted and available for comment.,

This spec is ![draft](http://rfc.unprotocols.org/spec:2/COSS/draft.svg), and is beind developed with the [Consensus Oriented Specification System](http://rfc.unprotocols.org/spec:2/COSS/)
through a [social repository](https://github.com/ausdigital/metadata-publisher). Contributions welcome!

The metadata registries are the heart of the system and users must have confidence in the integrity of published content. 

This framework operates on the basis that the issuer of a business identifier (the ABR in the case of the ABN) is best positioned to verify the identity of anyone attempting to authorise an update to the metadata registry.  

The Digital Capability Publisher is functionally equivelent to a REST version of the European OASIS standard "Service Metadata Publisher".

Users are expected to have used the Digital Capability Locator [DCL](https://capability-locator.readthedocs.io) to discover the appropriate DCP service for a particular business. They then interact with the DCP using the REST protocol [documented here](https://app.swaggerhub.com/api/ausdigital/metadata-publisher/1.0) to access a collection of ServiceMetaData entries for the business. 

The sample below shows a service metadata record example for a business with ABN 23601120601 that supports both standard invoice and RCTI processes.

```
    {"ServiceMetadata":[{
      "ParticipantIdentifier": {"scheme": "abn", "value": "23601120601"},
      "DocumentIdentifier": {"scheme": "dbc-docid", "value": "invoice-1"},
      "ProcessList": [{
        "ProcessIdentifier": {"scheme": "dbc-procid","value": "invoice-1"},
        "ServiceEndpointList": [
          {
          "transportProfile": "REST-POST",
          "EndpointURI": "https://api.myob.com/au/essentials/businesses/23601120601/purchase/invoice-1",
          "RequireBusinessLevelSignature": "true",
          "MinimumAuthenticationLevel": "2",
          "ServiceActivationDate": "2015-05-01",
          "ServiceExpirationDate": "2018-05-01",
          "Certificate": "TlRMTVNTUAABAAAAt7IY4gk....",
          "ServiceDescription": "invoice service",
          "TechnicalInformationUrl": "http://developer.myob.com/api/essentials-accounting/endpoints/"}
          {
        "ProcessIdentifier": {"scheme": "dbc-procid","value": "rcti-1"},
        "ServiceEndpointList": [
          {
          "transportProfile": "REST-POST",
          "EndpointURI": "https://api.myob.com/au/essentials/businesses/23601120601/sales/invoice-1",
          "RequireBusinessLevelSignature": "true",
          "MinimumAuthenticationLevel": "2",
          "ServiceActivationDate": "2015-05-01",
          "ServiceExpirationDate": "2018-05-01",
          "Certificate": "TlRMTVNTUAABAAAAt7IY4gk....",
          "ServiceDescription": "invoice service",
          "TechnicalInformationUrl": "http://developer.myob.com/api/essentials-accounting/endpoints/"}]
        }]
      },
    "Signature": "AD56YGNN8876TTFJ123…"
    },
    {... another signed service metadata structure ...
    }]
    
```
