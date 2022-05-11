<p align="center"><b>TranSMART-Migrator</b></p>

A solution for migrating patients' information from the OMOP CDM database to TranSMART structure.

### Team
  * João R. Almeida<sup id="a1">[1](#f1)</sup><sup id="a2">[2](#f2)</sup>
  * Luís B. Silva<sup id="a3">[3](#f3)</sup>
  * José L. Oliveira<sup id="a1">[1](#f1)</sup>

1. <small id="f1"> University of Aveiro, Dept. Electronics, Telecommunications and Informatics (DETI / IEETA), Aveiro, Portugal </small> [↩](#a1)
2. <small id="f2"> University of A Coruña, Dept. of Information and Communications Technologies, A Coruña, Spain </small> [↩](#a2)
2. <small id="f3"> BMD Software, Aveiro, Portugal </small> [↩](#a3)


### How to use?

To use this migration, it is necessary to import the TranSMARTMap in the migration script. See the following python example:

```python
import TranSMARTMap

class Harmonizer(object):
    #For changing fields stored in an different format in the OMOP CDM
    def set_2000000013(self, value):
        if value == "2/2" or value == "2/3" or value == "3/3":
            return "Non-carrier"
        if value == "3/4" or value == "2/4":
            return "Heterozygote"
        if value == "4/4":
            return "Homozygote"
        return ""#value

    #For adding new fields that do not exist in the OMOP CDM data
    def add_2000000620(self):#Study name
        return "Berlin"
        
TranSMARTMap.main(adHoc=Harmonizer)
```

It is necessary to define the settings in the ini file. This file contains the variables for the pipeline execution, such as database definitions, paths for the files necessary in the process and data formats. The following example contains the settings file structure.

```ini
[database]
datatype=postgresql
server=localhost
database=db
schema=omopcdm
port=5432
user=
password=

[cohort_info]
cohortdir=
cohortsep=

patientcsv=
obsdir=
results=
vocabulariesdir=
log=execution.log
cohortname=
formatdate=%%d-%%M-%%Y


[cohort_mappings]
columnsmapping=
contentmapping=
usagisep=,

[cohort_transformation]
headers=
measures=
cohortdest=

[cohort_harmonization]
cohortharmonizeddest=

[transmart]
cohortoutputfile=Transmart.tsv
cohortname=
transmartdstdir=
protegeoutput=
visitindependentoutput=
```

### Cite

Please cite the following, if you use TranSMART-Migrator in your work:

```bib
in progress
```

### Issues
Please let us know if there are any
[issues](https://github.com/bioinformatics-ua/TranSMART-migrator/issues).

### License
TranSMART-Migrator is under GPL-3.0 license. For more information, click
[here](https://github.com/bioinformatics-ua/TranSMART-migrator/blob/master/LICENSE).