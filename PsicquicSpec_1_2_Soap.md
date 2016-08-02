# Version 1.2 #

The documentation in this page corresponds to the version 1.2 of the PSICQUIC specification.

Using SOAP is the traditional way to access a web service. The PSICQUIC specification defines a [standard WSDL](http://code.google.com/p/psicquic/source/browse/trunk/psicquic-solr-ws/src/main/wsdl/psicquic11.wsdl) that all the implementations must comply with. This file contains the list of web service methods available for users.

The SOAP URL for the different interaction databases can be found in the [Registry](http://www.ebi.ac.uk/Tools/webservices/psicquic/registry/registry?action=STATUS). To fetch the WSDL just append **`?wsdl`** to the SOAP URL ([example](http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/psicquic?wsdl)).

**Important note**: the maximum number of interactions that can be returned by a SOAP request is **200**. If you want to retrieve more results, do an iteration of requests incrementing the _firstResult_ parameter by 200 until you reach the total number of results.

## Differences from previous versions ##

### From version 1.1 ###

None. As the REST implementation has changed, we also updated the SOAP version. The WSDL file is the same as for version 1.1

### From version 1.0 ###

Methods to retrieve properties from the service have been added. These properties are used by the provider to define characteristics of the service.

## Method Summary ##

| Method Name | Description |
|:------------|:------------|
| **[getByQuery](#Method:_getByQuery.md)** | Retrieve data using a [MIQL query](MiqlDefinition.md) |
| **[getByInteractor](#Method:_getByInteractor.md)** | Retrieve data using a specific participant identifier |
| **[getByInteractorList](#Method:_getByInteractorList.md)** | Retrieve data using a list of participant identifiers. This method can be used to retrieve interactions where the two or more participants passed as arguments are found. To do so, set the operand to _AND_. |
| **[getByInteraction](#Method:_getByInteraction.md)** | Retrieve a specific interaction using its identifier |
| **[getByInteractionList](#Method:_getByInteractionList.md)** | Retrieve a list of interactions, using the identifiers |


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
| infoRequest  | [infoRequest](#infoRequest.md)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryResponse.md) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteractor ###

**Description**: Retrieves data using a specific participant identifier.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRef  | [dbRef](#dbRef.md)  | Yes | The identifier to search for |  |
| infoRequest  | [infoRequest](#infoRequest.md)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryResponse.md) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteractorList ###

**Description**: Retrieve data using a list of participant identifiers. This method can be used to retrieve interactions where the two or more participants passed as arguments are found. To do so, set the operand to _AND_.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRefs  | List of [dbRef](#dbRef.md)  | Yes | The identifiers to search for |  |
| infoRequest  | [infoRequest](#infoRequest.md)  | Yes | Used to describe the format our to define the pagination |  |
| Operand | String | No | When multiple identifiers are provided two options are possible, dependening if we want to (a) find the interaction where ALL the provided identifiers are found or (b) just get a list of interactions where ANY of the identifiers is found. For (a) the value of _operand_ is '**AND**', whereas for (b) is '**OR**' (default) | AND, <br />OR |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryResponse.md) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteraction ###

**Description**: Retrieves a specific interaction using its identifier. This method is identical to the _getByInteractor_, but requiring interaction accessions instead.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRef  | [dbRef](#dbRef.md)  | Yes | The identifier to search for |  |
| infoRequest  | [infoRequest](#infoRequest.md)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryResponse.md) | Complex object containing the resulting data and some metadata about the results |


### Method: getByInteractionList ###

**Description**: Retrieves a list of interactions, using the identifiers.

**Input parameters**:

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| dbRefs  | List of [dbRef](#dbRef.md)  | Yes | The identifiers to search for |  |
| infoRequest  | [infoRequest](#infoRequest.md)  | Yes | Used to describe the format our to define the pagination |  |

**Output parameters**:

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| queryResponse | [queryResponse](#queryResponse.md) | Complex object containing the resulting data and some metadata about the results |


## Complex Objects ##


### dbRef ###

| **Name** | **Type** | **Required** | **Description** | **Example(s)** |
|:---------|:---------|:-------------|:----------------|:---------------|
| id | String | Yes | Identifier to use | brca2<br />P12345 |
| dbAc | String | No | Accession number of the database. Use it to avoid ambiguity if two databases contain the same parameter. Rarely used and not supported throughout |  |


### infoRequest ###

| **Name** | **Type** | **Required** | **Description** | **Default** |
|:---------|:---------|:-------------|:----------------|:------------|
| resultType | String | No | Format of the returned results. Possible options are: <br /> '**psi-mi/tab25**' (default): MITAB format. <br /> '**psi-mi/xml25**': PSI-MI XML 2.5.4 format.<br />'**count**': just contains the result counts. | psi-mi/tab25 |
| firstResult | Integer | No | Index for the first returned value (offset) | 0 |
| blockSize | Integer | No | Number of results to be returned. Maximum is **200**, so higher values will be ignored. | 0 |

When doing queries, the results must be paginated to avoid memory problems. All methods accept the parameters firstResult and blockSize, which are used to define the starting interaction and the number of interactions to be retrieved. Use them to retrieve your data in batches.

### queryResponse ###

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| resultSet | [resultSet](#resultSet.md) | Contains the results of the query |
| resultInfo | [resultInfo](#resultInfo.md) | Information about the query, such as the total number of results found |

### resultSet ###

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| mitab | String | When the _psi-mi/tab25_ format is used, this elements contains the resulting data as a String in MITAB format. Lines are separated by a carriage return. |
| entrySet | PSI-MI XML 2.5 | When the _psi-mi/xml25_ format is used, the XML file with the results is embedded in the response |

### resultInfo ###

| **Name** | **Type** | **Description** |
|:---------|:---------|:----------------|
| firstResult | Integer | The offset used when querying the service |
| blockSize | Integer | The number of results returned. If the service returns a different number of results than those asked for (e.g. the number provided was higher than the server maximum), this value shows how much data was returned by the service |
| totalResults | Integer | The total number of interaction evidences found, irrespectively of the firstResult and blockSize. |

## Querying the service ##

To query the SOAP service specific libraries may be needed by your programs. There is a [JAVA client](JavaClient.md) already implemented, but if you are not using JAVA you may need to create the service yourself (and if it is generic, contributing it to the project would be great!).

When doing queries, the results must be _paginated_ to avoid memory problems. All methods accept the parameters _firstResult_ and _maxResults_, which are used to define the starting interaction and the number of interactions to be retrieved. Use them to retrieve your data in batches. If they are not specified, the web service will limit the results automatically. Note that this would happen too if you set a value of _maxResults_ higher than a defined threshold, which in the Reference Implementation is **200**.

The default return types are:

  * **psi-mi/tab25**: returns PSI-MI TAB 2.5 format.
  * **psi-mi/xml25**: returns PSI-MI XML 2.5.4 format.