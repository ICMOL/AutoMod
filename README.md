## Introduction


## How to Use

To mine the potential PTMs from open search results, AutoMod requires the pepXML files (from **open search**) as input files. Here we demonstrate how to generate the pepXML files (open search) using MSFragger, mine PTMs from the open search results using AutoMod, and apply the mined PTM patterns to closed searches.
<br>

### System Requirement

- [Java SE Runtime Environment 15(or above)](https://www.oracle.com/java/technologies/javase/jdk15-archive-downloads.html) is required to be installed prior to use AutoMod. 
<br>

**Step 1.** Generate open search pepXML files using MSFragger

To generate the open search results, users can run MSFragger via the GUI (i.e., FragPipe) or the command-line. The detailed tutorials can be found at: https://github.com/Nesvilab/FragPipe and https://github.com/Nesvilab/MSFragger/wiki/Launching-MSFragger. 

The most important notice during the search is: **Please DO NOT specify any variable/fixed modficiations in the search parameters** (as shown in the figures below). This is because, as a modification is specified, its mass will be excluded from the mass difference and AutoMod can not detect it.   

<img src="https://github.com/ICMOL/AutoMod/blob/main/fig1.png" height="40%" width="40%" title="FragPipe (open search)">

<br>

**Step 2.** Mine PTMs using AutoMod

- Parameters: There are two sections in the AutoMod parameter file, including the basic and the advanced. Users can specify the output file path, number of PTMs in a combination, and the number of exported patterns in the basic section. The advanced section provides 109 PTM candidates collected from UniProt, and users can costumize the PTM list by adding or deleting PTM candidates if necessary.

BASIC

|        Name         |  Default Value | Comments |
|---------------------|----------------|------------------------------|
| output              | D:\test        | the location of output files |
| fragger_param_path  | (can be empty) | path to the MSFragger closed search parameter file  |
| num_threads         | -1             | number of threads used in the process. "-1" means that AutoMod will use (total number of threads - 1) in your computer for processing  |
| num_ptm_comb        |  4             | maximum combination number of post-translational modification per peptide |
| precursor_mass_tolerance    |  20    | precursor mass tolaerance (unit: ppm) |
| output_pattern_num  | 10             | export top N patterns based on the number of matches |
| min_match           | 10             | print out the patterns with the minimum match number |
| frag_site           | true           | use the suggested ptm sites in MSFragger open search results |


ADVANCED
  Please follow the following format when adding new PTM candidates: **UniqueMass@AminoAcid**
  
  ptm:	-0.984016@ARNDCEQGHILKMFPSTWYV
  ptm:	-1.031634@K
  ptm:	-15.010899@S
  
  
- Output files:



<br>

**Step 3.** Apply modification patterns in closed searches

<br>

## Frequently Asked Questions (FAQ)

### Preparing AutoMod
- **Using FragPipe run open search**:

1. To select workflow in open search
2. To cancel all Modifications in MSFagger

The `pepXML` files that is needed to use in AutoMod.

- **Parameter file**:
  - `AM-param.yml`:
    - setting the parameters 
    - fragger_param_path_file that is closed search config in MSFragger

### How to run
- **Windows**:
  - execute the following commands:
    - `java -jar AutoMod-v1.0.0-rc2.jar param-file-path pepXML-file-path`
  - if pepXML files are in same folder,  you can directly use `*.pepXML`:
    - e.g. `java -jar AutoMod-v1.0.0-rc2.jar D:\AM-param.yml D:\*.pepXML`

You will get the `fragger_am.params`.

- **FragPipe**:
1. To select workflow in closed search
2. To load `fragger_am.params` in MSFragger

### Interpreting AutoMod Output
`fragger.params` closed search config in MSFragger

`fragger_am.params` suggested ptm sites in MSFragger

`mod-pattern_n= _s= _c= ` possible modification pattern

`details_n= `
