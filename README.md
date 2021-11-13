## Introduction
Protein database search is a common approach for shotgun proteomic data, where peptide identification mainly relies on matching tandem mass spectrometry (MS/MS) to peptide candidates using database search tools. Numerous database search engines have been proposed, e.g., Sequest, MSFragger, MSAmanda, and Mascot, but prior knowledge of post-translational modifications potentially exist in a sample is often required during the searches. Here we present a software tool, called AutoMod, which can automatically mine the possible PTMs and export recommended modification patterns for downstream closed searches.

## How to Use

To mine the potential PTMs from open search results, AutoMod requires the pepXML files (from **open search**) as input files. Here we demonstrate how to generate the pepXML files (open search) using MSFragger, mine PTMs from the open search results using AutoMod, and apply the mined PTM patterns to closed searches.
<br>

### System Requirement

- [Java SE Runtime Environment 15(or above)](https://www.oracle.com/java/technologies/javase/jdk15-archive-downloads.html) is required to be installed prior to use AutoMod. 

### Step 1. Generate open search pepXML files using MSFragger

To generate the open search results, users can run MSFragger via the GUI (i.e., FragPipe) or the command-line. The detailed tutorials can be found at: https://github.com/Nesvilab/FragPipe and https://github.com/Nesvilab/MSFragger/wiki/Launching-MSFragger. 

The most important notice during the search is: **Please DO NOT specify any variable/fixed modficiations in the search parameters** (as shown in the figures below). This is because, as a modification is specified, its mass will be excluded from the mass difference and AutoMod can not detect it.   

<img src="https://github.com/ICMOL/AutoMod/blob/main/fig1.png" height="40%" width="40%" title="FragPipe (open search)">

### Step 2. Mine PTMs using AutoMod

#### Parameters

There are two sections in the AutoMod parameter file, including the basic and the advanced. Users can specify the output file path, number of PTMs in a combination, and the number of exported patterns in the basic section. The advanced section provides 109 PTM candidates collected from UniProt, and users can costumize the PTM list by adding or deleting PTM candidates if necessary.

- Basic parameters

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

- Advanced parameters
  
  Please follow the following format when adding new PTM candidates: **UniqueMass@AminoAcid**. For example, ptm:	79.966331@DRCHSTY or 
  ptm:	15.9949@M.

### Commands
- If the pepXML files are not in the same folder
  >  `java -jar AutoMod.jar param-file-path pepXML-path1 pepXML-path2 pepXML-path3`
  >    
  >  e.g., `java -jar AutoMod.jar AutoMod.yml D:\test1.pepXML`


- If the pepXML files are in the same folder
  >  `java -jar AutoMod.jar param-file-path folder-path\*.pepXML`
  >    
  >  e.g., `java -jar AutoMod.jar AutoMod.yml D:\*.pepXML`

#### Output files

AutoMod exports two output files, including details.tsv and mod-pattern.tsv. The details.tsv lists the mass differences and their corresponding PTMs with the confidence and support values, whereas the mod-pattern.tsv lists the top N PTM patterns which can be further apply for closed searches.



### Step 3. Apply modification patterns in closed searches

<br>

## Frequently Asked Questions (FAQ)



