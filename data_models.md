# Data Models 

This document describes how the SHP Ontology is applied to capture the provenance of teh data linkage process using the PowerShell scripts in a Microsoft Server environment. 

# Data Workflow 

![dash_files](https://github.com/TRE-Provenance/TRE-Provenance.github.io/assets/4025828/964fc1ad-df40-4e89-b5ef-1aaf5bbe9856)

The above image illustrates an example sltructure of the DaSH side of the TRE environment with three main folders. 

* **Import Folder**: This folder contains the data files that were transfered from the NHS side of the TRE. The files contain the data (e.g. data.csv) extracted from the protected datasets (e.g., SMR001) following the variable and cohort specification prepared by the researcher (linkage_plan.csv).
* ***Export Folder***:
* ***Release Folder***: This folder contains data files (e.g., data.csv) taht have passed the disclosure checks and are now accessible to the researcher. The folder also contains a provenance file without sensitive details (e.g., file paths) taht were previously present in the analyst's version. 


# Limitations

# Modelling Elements of Provenance Trace

# Provenance Trace Structure 

## @id - unique identifier

```JSON

   "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv"

```

Within the same TRE environment, base IRI for all elements should be the same - e.g., "https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/"

The PowershellScripts will automatically modify IRIs of individual provenance elements based on the project context and their type. 

For example, all project-specific data elements will contain project name in their IRI  - "https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/"

Individual files contained in the folders will contain the name of teh folder in their IRI in order to establish a unique reference to different copies of the same file - e.g., "https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/import/data.csv"

## @type 

```JSON

    "@type":[ "File", "shp_DataLinkagePlan"]

```

This property is typically modelled as a JSON array to enable multiple types to be associated with the particular element (e.g., the element can be of type of File (i.e. to align with the RO-Crate vocabulary) as defined in the schema.org (http://schema.org/MediaObject) but at the same time it can be also of type of https://w3id.org/shp#DataLinkagePlan defined in the SHP ontology. 

## description

```JSON

     "description":"This  is  data  linkage plan description."

```

Auto-generated value.

## label

Auto-generated from the file name.

## path

(only applicable to files)

Physical location of the file on the file system.

## hash

(only applicable to files)

Hash of the file

## wasAttributedTo

Agents that were responsible for the activity or creation/modification of a file. The provenance monitoring 

# Element Examples 

## Data Linkage Plan 

```JSON

{
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv",
      "@type":[
         "File","shp_DataLinkagePlan"
      ],
      "description":"This  is  data  linkage plan description.",
      "label":"linkagePlan.csv",
      "path":"file:///c:/documents/linkagePlan.csv",
      "wasAttributedTo":{
         "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/staff/s10mm2"
      },
      "exifData":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#DataSource.a35d45fd-cfcf-44d7-96a3-b44de21a9652"
         }
      ]
   },
   {
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#DataSource.a35d45fd-cfcf-44d7-96a3-b44de21a9652",
      "@type":[
         "shp_LinkagePlanDataSource"
      ],
      "label":"datasource name",
      "shp_requestedVariables":{
         "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#RequestedVariables.9eedfc96-d26a-45af-8c83-065ccf1d24dc"
      },
      "shp_constraint":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#VariableConstraint.3987e401-abc0-4d84-9ba2-0fd3a635e6e2"
         }
      ]
   },
   {
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#RequestedVariables.9eedfc96-d26a-45af-8c83-065ccf1d24dc",
      "@type":[
         "shp_RequestedVariables"
      ],
      "hadMember":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/variable/GENDER"
         }
      ]
   },
   {
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#VariableConstraint.3987e401-abc0-4d84-9ba2-0fd3a635e6e2",
      "@type":[
         "shp_VariableConstraint"
      ],
      "shp_minValue":"2002-09-24",
      "shp_maxValue":"2022-09-24",
      "shp_targetVariable":{
         "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/variable/GENDER"
      }
   }
	  

```
