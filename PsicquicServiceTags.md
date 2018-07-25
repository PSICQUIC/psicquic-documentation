# Why Tags ? #

In addition to having all PSICQUIC services available via the Registry, some user do need to apply filters on the requested services in order to retrieve specific type of molecular interaction. Here are just a few examples:
  * [Only IMEx data providers](http://www.ebi.ac.uk/Tools/webservices/psicquic/registry/registry?action=STATUS&tags=imex+curation)
  * Only manually curated data
  * Only protein-protein interactions and not (text-mining or predicted)


# Current tags #

We have so far put together the 5 categories of tags described below:

### Interacting molecules (MI:1046) ###
  * protein-protein (MI:1047)
  * smallmolecule-protein (MI:1048)
  * nucleicacid-protein (MI:1049)

### Interaction representation (MI:1050) ###
  * evidence (MI:1051)
  * clustered (MI:1052)

### Curation depth (MI:0955) ###
  * imex curation (MI:0959)
  * mimix curation (MI:0960)
  * rapid curation (MI:0961)

### source (MI:1053) ###
  * experimentally-observed (MI:1054)
  * internally-curated (MI:1055)
  * text-mining (MI:1056)
  * predicted (MI:1057)
  * imported (MI:1058)

### Complex expansion (MI:1059) ###
  * spoke expansion (MI:1060)
  * matrix expansion (MI:1061)
  * bipartite expansion (MI:1062)

You can refer to the [Registry](Registry.md#The-'tags'-parameter) documentation to find out how to use the tags to query for specific lists of services.

# Current limitations #

For the time being the definition of tags is done as a manual curation effort by the maintainers of the PSICQUIC Registry with input from PSICQUIC service providers. The current strategy has been adopted because it could be put in place quickly but suffers from a number of limitations, namely:
  * currently the tags are set to describe a PSICQUIC service as a whole
  * the current tagging strategy do not allow to isolate specific part of the dataset and that further development is already planned to enable that feature.
  * that multiple tags per category can be used to describe specific conditions, for instance, if a provider has included manually curated data of their own as well as imported data from a third party source, both the tags 'imported' and 'internally-curated' should be used. This will now allow users to discriminate the underlying interactions but it is still very informative.
