# Data Models 

This document describes how the SHP Ontology is applied to capture the provenance of teh data linkage process using the PowerShell scripts in a Microsoft Server environment. 

# Data Workflow 

![dash_files](https://github.com/TRE-Provenance/TRE-Provenance.github.io/assets/4025828/964fc1ad-df40-4e89-b5ef-1aaf5bbe9856)

The above image illustrates an example sltructure of the DaSH side of the TRE environment with three main folders. 

* **Import Folder**: This folder contains the data files that were transfered from the NHS side of the TRE. The files contain the data (e.g. data_v1.2.csv) extracted from the protected datasets (e.g., SMR001) following the variable and cohort specification prepared by the researcher (linkage_plan.csv).
* ***Export Folder***:
* ***Release Folder***: This folder contains data files (e.g., data_v1.2.csv) that have passed the disclosure checks and are now accessible to the researcher. The folder also contains a provenance file without sensitive details (e.g., file paths) taht were previously present in the analyst's version. 


# Limitations

# Modelling Elements of Provenance Trace

# Provenance Trace Structure 

The provenance trace is modelled as a knowledge graph and stored using a JSON-LD serialisation in a static file. The high level structure of the provenance file is as follows:

```JSON
{
 "@context":[

VOCABULARY TERMS (i.e., RO-Crate + SHP Ontology)

 ],
 "@graph":[

PROVENANCE TRACE CONTENT

]
}
```

Note, we do not use remote references for the @context part, instead we include the full vocabulary of terms in the static file as the TRE environment is typpically cut off from the Internet. 

## @id - unique identifier

```JSON

   "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv"

```

Within the same TRE environment, base IRI for all elements should be the same - e.g., "https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/"

The PowershellScripts will automatically modify IRIs of individual provenance elements based on the project context and their type. 

For example, all project-specific data elements will contain project name in their IRI  - "https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/"

Individual files contained in the folders will contain the name of teh folder in their IRI in order to establish a unique reference to different copies of the same file - e.g., "https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/import/data_v1.2.csv"

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

```JSON

     "label":"linkagePlan.csv",
```

Auto-generated from the file name.

## path

```JSON

  "path":"file:///c:/documents/linkagePlan.csv",

```

(only applicable to files)

Physical location of the file on the file system.

## hash

```JSON

    "shp_hash":"e0d123e5f316bef78bfdf5a008837577",
```

(only applicable to files)

Hash of the file

## wasAttributedTo

```JSON

    "wasAttributedTo":[
         {"@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/staff/c10ll2"}
      ],
```

Agents that were responsible for the activity or creation/modification of a file. The provenance monitoring 

# Element Examples 

## Variables

```JSON
{"@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/exampleDatabase/variable/height",
"@type":["shp_Variable"],"label":"Height"
},
```

The SHP ontology defines a class of Sensitive variables (e.g., those containing identifiable information) which should not appear in the released files.   

```JSON
{"@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/exampleDatabase/variable/postcode",
"@type":["shp_SensitiveVariable"],"label":"postcode"
}
```

## Database

Database represent the sources of raw patient data and together with data linkage plan represent initial inputs into the data linkage workflow.

```JSON

 {
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/exampleDatabase",
      "@type":[
         "shp_Database"
      ],
      "description":"This  is a database full of useful information.",
      "shp_databaseName":"Example Database",
      "shp_abbreviation":"ED",
      "shp_version":"1.2",
      "shp_dataCustodian":"NHS Grampian",
      "shp_contact":"info@example.com",
      "shp_lastKnownUpdate":"2022-09-24",
      "shp_mostRecentRecordDate":"2022-03-24",
      "shp_oldestRecordDate":"1976-03-24",
      "shp_contextualInformationLink":"https://www.abdn.ac.uk/iahs/facilities/dash-datasets.php"
 }
```



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
	  "shp_hash":"e0d123e5f316bef78bfdf5a008837577",
      "wasAttributedTo":[{
         "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/staff/s10mm2"
      }],
      "exifData":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#DataSource.a35d45fd-cfcf-44d7-96a3-b44de21a9652"
         }
      ]
   },
```

Now we need to describe the [LinkagePlanDataResource](https://w3id.org/shp#DataLinkagePlan) which was mentioned in the "exif" part of the previous description. 

```JSON
   {
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#DataSource.a35d45fd-cfcf-44d7-96a3-b44de21a9652",
      "@type":[
         "shp_LinkagePlanDataSource"
      ],
      "label":"Data Source Description Example",
      "shp_database":{"@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/exampleDatabase"},
      "shp_requestedVariables":{
         "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#RequestedVariables.9eedfc96-d26a-45af-8c83-065ccf1d24dc"
      },
      "shp_constraint":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#VariableConstraint.3987e401-abc0-4d84-9ba2-0fd3a635e6e2"
         }
      ]
   },
```

The following code describes the collection of requested variables mentioned in the [LinkagePlanDataResource](https://w3id.org/shp#DataLinkagePlan) description.

```JSON
   {
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#RequestedVariables.9eedfc96-d26a-45af-8c83-065ccf1d24dc",
      "@type":[
         "shp_RequestedVariables"
      ],
      "hadMember":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/exampleDatabase/variable/height"
         }
      ]
   },
```

Finally, we will describe any constraints mentioned in the [LinkagePlanDataResource](https://w3id.org/shp#DataLinkagePlan) description. In this case, we describe a constraint on the height variable with min value of 160 and max value of 190 (assumuning the variable lists height of people in cm).

```JSON
   {
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#VariableConstraint.3987e401-abc0-4d84-9ba2-0fd3a635e6e2",
      "@type":[
         "shp_VariableConstraint"
      ],
      "shp_minValue":"160",
      "shp_maxValue":"190",
      "shp_targetVariable":{
         "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/exampleDatabase/variable/height"
      }
   }
```

## "Black Box" Activities

Sometimes it is not possible to get accurate information about all activities that occured during the data linkage process. For example, in the current implementation of our provenance monitroing system, we cannot access the NHS side of the Safe Haven. Instead, the analysts provide additional metadata (e.g., about the source Database) in a separate CSV file together with the imported result datasets. In order to ensure the consistency of the provenance record we can abstract these activities into a generic [DaSH Activity](https://safehavenprovenance.github.io/SHP-ontology/index-en.html#DashActivity). 

The following example links the Data Linkage Plan and the corresponding source database to the dataset contained in the import folder: 

```JSON

{     "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/Activity/6f41bc5a-9c82-4ea2-8c9c-80fb84be8957",
      "@type":[
         "CreateAction", "shp_DashActivity"
      ],
      "agent":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/staff/username3"
         }
      ],
      "label":"NHS data extraction",
      "object":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv"
         },
	{
            "@id":"ttps://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/exampleDatabase"
         }
      ],
      "result":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/import/data_v1.1.csv"
         }
      ]
   }


```

## Update Activity

```JSON

{     "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/Update/11845ee9-f4d2-4ad0-8b9d-ba8a5fd4116d",
      "@type":[
         "CreateAction", "shp_Update"
      ],
      "agent":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/staff/username2"
         }
      ],
      "label":"Version v1.2 update (data.csv)",
      "object":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/import/data_v1.1.csv"
         }
      ],
      "result":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/import/data_v1.2.csv"
         }
      ]
   }

```


## Data Release Activity

```JSON

{     "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/DatasetRelease/d4c7c1bb-a4a4-42ca-bdb6-188c4a6fd87a",
      "@type":[
         "CreateAction", "shp_DatasetRelease"
      ],
      "agent":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/staff/username2"
         }
      ],
      "label":"Data Release",
      "object":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/export/signedOff/data_v1.2.csv"
         }
      ],
      "result":[
         {
            "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/release/data_v1.2.csv"
         }
      ]
   }

```

## Dataset
