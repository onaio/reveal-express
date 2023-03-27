# fhircore-tooling
A command line utility to support FHIRCore content authoring. This tool supports the HL7 FHIR R4 spec.


## How to use it

Download the latest release from https://github.com/opensrp/fhircore-tooling/releases

To run it as a java jar by using the command `efsity-1.0.0.jar -h` . This is the help command and will list the available options.

If you are using a linux environment e.g. bash you can choose to create an alias for this as shown below. _(Remember to reload the terminal)_

`alias fct='java -jar ~/Downloads/efsity-1.0.0.jar'`

To run the previous help command you can then run `fct -h` in your terminal.

The rest of the documentation will assume you have configured an alias for running the efsity jar file name fct as above.

### Converting structure map .txt to .json
To convert your `structure-map.txt` file to its corresponding `.json` file, you can run the command
```console
$ fct convert -t sm --input ~/Workspace/fhir-resources/coda/structure_map/coda-child-structure-map.txt
```

### Converting library .cql to .json
```console
$ fct convert -t cql -i /some/path/Patient-1.0.0.cql
```

**Options**
```
-t or --type - the type of conversion, can be sm for structure map to json or cql for cql to json library
-i or --input - the input file or file path
-o or --output - the output path, can be a file or directory. Optional - default is current directory
```

### Extracting resources from questionnaire response
To extract FHIR Resources you can run the command:
```console
$ fct extract -qr /patient-registration-questionnaire/questionnaire-response.json -sm /path/to/patient-registration-questionnaire/structure-map.txt
```

**Options**
```
-qr or --questionnaire-response - the questionnaire response json file
-sm or --structure-map - the path to the structure map file
-o or --output - the output path, can be a file or directory. Optional - default is current directory
```

### Validating your app configurations
The tool supports some validations for the fhircore app configurations. To validate you can run the command:
```console
$ fct validate -c ~/path/to/composition_config_file.json -i ~/Workspace/fhir-resources/<project>/app_configs/
```
The above will output a list of errors and warnings based on any rules that have been violated.

**Options**
```
-c or --composition - the composition json file of the project
-i or --input - the input directory path. This should point to the folder with the app configurations e.g. ~/Workspace/fhir-resources/ecbis_cha_preview/
-o or --output - the output path, can be a file or directory. Optional - default is current directory
```
**Sample screenshot output**
<br/>
<img width="715" alt="Screenshot 2023-03-27 at 21 43 09" src="https://user-images.githubusercontent.com/10017086/228037581-209f9bab-d1b9-45eb-a920-aa12c70c5b98.png">

## Development
### Set up
This is a Java + Kotlin maven project. You can import it in you JetBrains IDE as such. The utility is built on the very awesome `Picocli` library https://picocli.info/

### building
To build and create a new jar file run the maven package command

`mvn spotless:apply package`