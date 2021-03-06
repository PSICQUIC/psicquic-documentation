# Version 1.4 #

The documentation in this page corresponds to the version 1.4 of the PSICQUIC specification.

Using SOAP is the traditional way to access a web service. The PSICQUIC specification defines a [standard WSDL](https://github.com/PSICQUIC/psicquic-solr-ws/blob/master/src/main/wsdl/psicquic11.wsdl) that all the implementations must comply with. This file contains the list of web service methods available for users.

The SOAP URL for the different interaction databases can be found in the [Registry](http://www.ebi.ac.uk/Tools/webservices/psicquic/registry/registry?action=STATUS). To fetch the WSDL just append **`?wsdl`** to the SOAP URL ([example](http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/psicquic?wsdl)).

**Important note**: the maximum number of interactions in XML format that can be returned by a SOAP request is **500**. If you want to retrieve more results, do an iteration of requests incrementing the _firstResult_ parameter by 500 until you reach the total number of results.

## Differences from previous versions ##

### From version 1.3 ###

  * The WSDL file has not been updated so the SOAP methods are the same as for the 1.3, 1.2 and 1.1 versions.
  * psi-mi/tab28 is now accepted. The ResultSet returned by the SOAP service will contain the MITAB (2.5, 2.6, 2.7 or 2.8) as a String (same as for the previous versions explaining why the WSDL file has not been updated since version 1.1)

### From version 1.2 ###

  * The WSDL file has not been updated so the SOAP methods are the same as for 1.2 and 1.1.
  * psi-mi/tab26 and psi-mi/tab27 are now accepted. The ResultSet returned by the SOAP service will contain the MITAB (2.5, 2.6 or 2.7) as a String (same as for the previous versions explaining why the WSDL file has not been updated since version 1.1)
  * When returning MITAB (2.5, 2.6 or 2.7), there is no limit in the number of binary interactions returned by the SOAP service as it is doing some pagination internally. However, the maximum number of interaction to be returned in XML is 500. If the user ask for more than 500 results in XML, the SOAP service will return a 400 HTTP error code.

### From version 1.1 ###

None. As the REST implementation has changed, we also updated the SOAP version. The WSDL file is the same as for version 1.1

### From version 1.0 ###

Methods to retrieve properties from the service have been added. These properties are used by the provider to define characteristics of the service.


## Method Summary ##

| Method Name | Description |
|:------------|:------------|
| **[getByQuery](#method-getbyquery)** | Retrieve data using a [MIQL query](MiqlDefinition.md) |
| **[getByInteractor](#method-getbyinteractor)** | Retrieve data using a specific participant identifier |
| **[getByInteractorList](#method-getbyinteractorlist)** | Retrieve data using a list of participant identifiers. This method can be used to retrieve interactions where the two or more participants passed as arguments are found. To do so, set the operand to _AND_. |
| **[getByInteraction](#method-getbyinteraction)** | Retrieve a specific interaction using its identifier |
| **[getByInteractionList](#method-getbyinteractionlist)** | Retrieve a list of interactions, using the identifiers |


Other methods to retrieve information about the service itself (metadata) are also available:

| Method Name | Description |
|:------------|:------------|
| **getSupportedReturnTypes** | Returns the list of possible formats for the retrieved data |
| **getSupportedDbAcs** | Supported database accessions |
| **getVersion** | Gets the version of the service |
| **getProperties** | Retrieve a list of the property objects defined in a service by the provider. Each property object have a key and a value |
| **getProperty** | Retrieve a property from the service |


## Methods ##

This section explains the parameters that can be used in the above methods.


### Method: getByQuery ###

**Description**: Retrieves data using a [MIQL query](MiqlReference.md). This is the more general method an can be used to perform the most flexible queries by using MIQL. The other methods of the web service are just convenience methods that just reduce the scope of the query, hence what the other methods do can be done through this one.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| query  | String  | Yes | The [MIQL query](MiqlReference.md) to use |  |
| infoRequest  | [infoRequest](#inforequest)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryresponse) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteractor ###

**Description**: Retrieves data using a specific participant identifier.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRef  | [dbRef](#dbref)  | Yes | The identifier to search for |  |
| infoRequest  | [infoRequest](#inforequest)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryresponse) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteractorList ###

**Description**: Retrieve data using a list of participant identifiers. This method can be used to retrieve interactions where the two or more participants passed as arguments are found. To do so, set the operand to _AND_.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRefs  | List of [dbRef](#dbref)  | Yes | The identifiers to search for |  |
| infoRequest  | [infoRequest](#inforequest)  | Yes | Used to describe the format our to define the pagination |  |
| Operand | String | No | When multiple identifiers are provided two options are possible, dependening if we want to (a) find the interaction where ALL the provided identifiers are found or (b) just get a list of interactions where ANY of the identifiers is found. For (a) the value of _operand_ is '**AND**', whereas for (b) is '**OR**' (default) | AND, <br />OR |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryresponse) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteraction ###

**Description**: Retrieves a specific interaction using its identifier. This method is identical to the _getByInteractor_, but requiring interaction accessions instead.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRef  | [dbRef](#dbref)  | Yes | The identifier to search for |  |
| infoRequest  | [infoRequest](#inforequest)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryresponse) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteractionList ###

**Description**: Retrieves a list of interactions, using the identifiers.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRefs  | List of [dbRef](#dbref)  | Yes | The identifiers to search for |  |
| infoRequest  | [infoRequest](#inforequest)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryresponse) | Complex object containing the resulting data and some metadata about the results |


## Complex Objects ##


### dbRef ###

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| id | String | Yes | Identifier to use | brca2<br />P12345 |
| dbAc | String | No | Accession number of the database. Use it to avoid ambiguity if two databases contain the same parameter. Rarely used and not supported throughout |  |


### infoRequest ###

| **Name** | **Type** | **Required** | **Description** | **Default** |
|:---------|:---------|:-------------|:----------------|:------------|
| resultType | String | No | Format of the returned results. Possible options are: <br /> '**psi-mi/tab25**' (default): MITAB format. <br /> '**psi-mi/tab26**': MITAB 26 format (not all services provide this format). <br /> '**psi-mi/tab27**': MITAB 27 format (not all services provide this format).  <br /> '**psi-mi/tab28**': MITAB 28 format (not all services provide this format). <br /> '**psi-mi/xml25**': PSI-MI XML 2.5.4 format.<br />'**count**': just contains the result counts. | psi-mi/tab25 |
| firstResult | Integer | No | Index for the first returned value (offset) | 0 |
| blockSize | Integer | No | Number of results to be returned. Maximum is **200**, so higher values will be ignored. | 0 |

When doing queries, the results must be paginated to avoid memory problems. All methods accept the parameters firstResult and blockSize, which are used to define the starting interaction and the number of interactions to be retrieved. Use them to retrieve your data in batches.

### queryResponse ###

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| resultSet | [resultSet](#resultset) | Contains the results of the query |
| resultInfo | [resultInfo](#resultinfo) | Information about the query, such as the total number of results found |

### resultSet ###

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| mitab | String | When the _psi-mi/tab25_, _psi-mi/tab26_, _psi-mi/tab27_ or _psi-mi/tab28_ format is used, this element contains the resulting data as a String in MITAB format. Lines are separated by a carriage return. |
| entrySet | PSI-MI XML 2.5 | When the _psi-mi/xml25_ format is used, the XML file with the results is embedded in the response |

### resultInfo ###

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| firstResult | Integer | The offset used when querying the service |
| blockSize | Integer | The number of results returned. If the service returns a different number of results than those asked for (e.g. the number provided was higher than the server maximum), this value shows how much data was returned by the service |
| totalResults | Integer | The total number of interaction evidences found, irrespectively of the firstResult and blockSize. |

## Querying the service ##

To query the SOAP service specific libraries may be needed by your programs. There is a [JAVA client](JavaClient.md) already implemented, but if you are not using JAVA you may need to create the service yourself (and if it is generic, contributing it to the project would be great!).

When doing queries, the results in XML must be _paginated_ to avoid memory problems. All methods accept the parameters _firstResult_ and _maxResults_, which are used to define the starting interaction and the number of interactions to be retrieved. Use them to retrieve your data in batches.

The default return types are:

  * **psi-mi/tab25**: returns PSI-MI TAB 2.5 format.
  * **psi-mi/tab26**: returns PSI-MI TAB 2.6 format. (not all services provide this format)
  * **psi-mi/tab27**: returns PSI-MI TAB 2.7 format. (not all services provide this format)
  * **psi-mi/tab28**: returns PSI-MI TAB 2.8 format. (not all services provide this format)
  * **psi-mi/xml25**: returns PSI-MI XML 2.5.4 format.