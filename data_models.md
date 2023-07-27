# Data Models 

This document describes how the SHP Ontology is applied to capture the provenance of teh data linkage process using the PowerShell scripts in a Microsoft Server environment. 

# Data Workflow 

# Limitations

# Data Elements

## Data Linkage Plan 

```JSON

{
   "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv",
   "@type":[
      "File"
   ],
   "description":"This  is  data  linkage plan description.",
   "label":"linkagePlan.csv",
   "path":"file:///....",
   "wasAttributedTo":{
      "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/staff/username1"
   },
   "exifData":[
      {
         "@id":"https://www.abdn.ac.uk/iahs/facilities/grampian-data-safe-haven/project1/linkagePlan.csv#selectedVariables",
         "@type":[
            "shp_SelectedVariables"
         ],
         "hadMember":[
            {
               "@id":"https://example.com/variable/gender"
            },
            {
               "@id":"https://example.com/variable/height"
            },
            {
               "@id":"https://example.com/variable/chi"
            }
         ]
      },
      {
         "@id":"https://example.com/import_signed/data.csv#variableStats1",
         "@type":[
            "shp_EntityCharacteristic"
         ],
         "shp_minValue":"2",
         "shp_maxValue":"100",
         "shp_targetFile":{
            "@id":"https://example.com/import_signed/data.csv"
         },
         "shp_targetFeature":{
            "@id":"https://example.com/variable/height"
         }
      },
      {
         "@id":"https://example.com/import_signed/data.csv#variableStats2",
         "@type":[
            "shp_EntityCharacteristic"
         ],
         "shp_minValue":"F",
         "shp_maxValue":"M",
         "shp_targetFile":{
            "@id":"https://example.com/import_signed/data.csv"
         },
         "shp_targetFeature":{
            "@id":"https://example.com/variable/gender"
         }
      },
      {
         "@id":"https://example.com/import_signed/data.csv#variableStats3",
         "@type":[
            "shp_EntityCharacteristic"
         ],
         "shp_minValue":"0001",
         "shp_maxValue":"00342",
         "shp_targetFile":{
            "@id":"https://example.com/import_signed/data.csv"
         },
         "shp_targetFeature":{
            "@id":"https://example.com/variable/chi"
         }
      },
      {
         "@id":"https://example.com/import_signed/data.csv#summaryStats",
         "@type":[
            "shp_EntityCharacteristic"
         ],
         "shp_rowCount":"198",
         "shp_targetFile":{
            "@id":"https://example.com/import_signed/data.csv"
         }
      }
	  
	  
	  ]
	  
	  }
	  

```
