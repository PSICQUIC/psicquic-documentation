# Introduction #

This is a proposal on the format to use when loading data into a PSICQUIC 2.x server. This example also account for data loaded by IMEx partner.


# Details #
```
<?xml version="1.0" encoding="UTF-8"?>

<entrySet xmlns="http://psi.hupo.org/mi/mif" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" level="2" version="5" minorVersion="4" xsi:schemaLocation="http://psi.hupo.org/mi/mif http://psidev.sourceforge.net/mi/rel25/src/MIF254.xsd">
 <entry>
  <source releaseDate="2008-11-04">
   <names>
    <shortLabel>DIP</shortLabel>
    <fullName>Database of Interacting Proteins</fullName>
   </names>

   <bibref>
    <xref>
     <primaryRef db="pubmed" dbAc="MI:0446" id="14681454" refType="primary-reference" refTypeAc="MI:0358"/>
    </xref>
   </bibref>

   <xref>
    <primaryRef db="psi-mi" dbAc="MI:0448" id="MI:0465" refType="identity" refTypeAc="MI:0356"/>
   </xref>

   <attributeList>
    <attribute name="email">dip@mbi.ucla.edu</attribute>
    <attribute name="postalAddress">611 Young Drive East; Los Angeles CA 90095; USA</attribute>
    <attribute name="url">http://dip.doe-mbi.ucla.edu</attribute>
   </attributeList>
  </source>

  <interactionList>
   <interaction id="97" imexId="IM-9547-4">
    <xref>
     <!-- describe from which database the record comes from - refType to be defined -->
     <secondaryRef db="psi-mi" dbAc="MI:0488" id="MI:0465" refType="?????" refTypeAc="?????" />
    </xref>

    <experimentList>
     <experimentDescription id="102">
      <bibref>
       <xref>
        <primaryRef db="pubmed" dbAc="MI:0446" id="17898163" refType="primary-reference" refTypeAc="MI:0358"/>
       </xref>
      </bibref>

      <xref>
       <!-- Reference to the IMEx id of the corresponding publication -->
       <secondaryRef db="imex" dbAc="MI:0670" id="IM-9547" refType="imex-primary" refTypeAc="MI:0662" />
      </xref>

      <hostOrganismList>
       <hostOrganism ncbiTaxId="4932">
        <names>
         <fullName>Saccharomyces cerevisiae</fullName>
        </names>
       </hostOrganism>
      </hostOrganismList>

      <interactionDetectionMethod>
       <names>
        <fullName>two hybrid</fullName>
       </names>

       <xref>
        <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0018" refType="identity" refTypeAc="MI:0356"/>
       </xref>
      </interactionDetectionMethod>
     </experimentDescription>
    </experimentList>

    <participantList>
     <participant id="98">
      <names>
       <shortLabel>CIPK6</shortLabel>
      </names>

      <interactor id="99">
       <names>
        <shortLabel>CIPK6</shortLabel>
        <fullName>Putative uncharacterized protein F6I18.130</fullName>
       </names>

       <xref>
        <primaryRef db="uniprot knowledge base" dbAc="MI:0486" id="O65554" refType="identity" refTypeAc="MI:0356"/>
        <secondaryRef db="refseq" dbAc="MI:0481" id="NP_194825" refType="identity" refTypeAc="MI:0356"/>
       </xref>

       <interactorType>
        <names>
         <fullName>protein</fullName>
        </names>

        <xref>
         <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0326" refType="identity" refTypeAc="MI:0356"/>
        </xref>
       </interactorType>

       <organism ncbiTaxId="3702">
        <names>
         <fullName>Arabidopsis thaliana</fullName>
        </names>
       </organism>
      </interactor>

      <participantIdentificationMethodList>
       <participantIdentificationMethod>
        <names>
         <fullName>predetermined participant</fullName>
        </names>

        <xref>
         <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0396" refType="identity" refTypeAc="MI:0356"/>
        </xref>
       </participantIdentificationMethod>
      </participantIdentificationMethodList>

      <biologicalRole>
       <names>
        <shortLabel>unspecified role</shortLabel>
       </names>

       <xref>
        <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0499" refType="identity" refTypeAc="MI:0356"/>
       </xref>
      </biologicalRole>

      <experimentalRoleList>
       <experimentalRole>
        <names>
         <fullName>bait</fullName>
        </names>

        <xref>
         <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0496" refType="identity" refTypeAc="MI:0356"/>
        </xref>
       </experimentalRole>
      </experimentalRoleList>

      <hostOrganismList>
       <hostOrganism ncbiTaxId="4932">
        <names>
         <fullName>Saccharomyces cerevisiae</fullName>
        </names>
       </hostOrganism>
      </hostOrganismList>
     </participant>

     <participant id="100">
      <names>
       <shortLabel>CBL9</shortLabel>
      </names>

      <interactor id="101">
       <names>
        <shortLabel>CBL9</shortLabel>
        <fullName>Calcineurin B-like protein 9</fullName>
       </names>

       <xref>
        <primaryRef db="uniprot knowledge base" dbAc="MI:0486" id="Q9LTB8" refType="identity" refTypeAc="MI:0356"/>
        <secondaryRef db="refseq" dbAc="MI:0481" id="NP_199521" refType="identity" refTypeAc="MI:0356"/>
       </xref>

       <interactorType>
        <names>
         <fullName>protein</fullName>
        </names>

        <xref>
         <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0326" refType="identity" refTypeAc="MI:0356"/>
        </xref>
       </interactorType>

       <organism ncbiTaxId="3702">
        <names>
         <fullName>Arabidopsis thaliana</fullName>
        </names>
       </organism>
      </interactor>

      <participantIdentificationMethodList>
       <participantIdentificationMethod>
        <names>
         <fullName>predetermined participant</fullName>
        </names>

        <xref>
         <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0396" refType="identity" refTypeAc="MI:0356"/>
        </xref>
       </participantIdentificationMethod>
      </participantIdentificationMethodList>

      <biologicalRole>
       <names>
        <shortLabel>unspecified role</shortLabel>
       </names>

       <xref>
        <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0499" refType="identity" refTypeAc="MI:0356"/>
       </xref>
      </biologicalRole>

      <experimentalRoleList>
       <experimentalRole>
        <names>
         <fullName>prey</fullName>
        </names>

        <xref>
         <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0498" refType="identity" refTypeAc="MI:0356"/>
        </xref>
       </experimentalRole>
      </experimentalRoleList>

      <hostOrganismList>
       <hostOrganism ncbiTaxId="4932">
        <names>
         <fullName>Saccharomyces cerevisiae</fullName>
        </names>
       </hostOrganism>
      </hostOrganismList>
     </participant>
    </participantList>

    <interactionType>
     <names>
      <fullName>direct interaction</fullName>
     </names>

     <xref>
      <primaryRef db="psi-mi" dbAc="MI:0488" id="MI:0407" refType="identity" refTypeAc="MI:0356"/>
     </xref>
    </interactionType>
   </interaction>

  </interactionList>
 </entry>

</entrySet>

```