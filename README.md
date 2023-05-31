## Introduction
Protein database search is a common approach for shotgun proteomics data, where peptide identification mainly relies on matching tandem mass spectrometry (MS/MS) with peptide candidates using database search tools. Numerous database search engines have been proposed, e.g., Sequest, MSFragger, MSAmanda, and Mascot, but prior knowledge of post-translational modifications (PTMs) potentially exist in a sample is often required during the searches. Here we present a software tool, called AutoMod, which can automatically detect possible PTMs and export recommended modification patterns for downstream closed searches.

## How to Use

To detect potential PTMs from open search results, AutoMod requires the pepXML files obtained from **open (mass-tolerant) searches** as input files. Here we demonstrate how to generate the open search pepXML files using MSFragger, detect PTMs from the open search results using AutoMod, and apply the detected PTM combinations to downstream closed searches.
<br>

### System Requirement

- [Java SE Runtime Environment 8(or above)](https://www.oracle.com/tw/java/technologies/javase/javase8-archive-downloads.html) is required to be installed prior to use AutoMod. 

### Step 1. Generate open search pepXML files using MSFragger

To generate the open search results, users can run MSFragger via FragPipe or the command-line. The detailed tutorials can be found at: https://github.com/Nesvilab/FragPipe and https://github.com/Nesvilab/MSFragger/wiki/Launching-MSFragger. 

**Please DO NOT specify any variable/fixed modficiations in the search parameters** (as shown in the figures below), because, as a modification is specified, its mass will be excluded from the mass difference and AutoMod cannot detect it.   

<img src="https://github.com/ICMOL/AutoMod/blob/main/fig1.png" height="40%" width="40%" title="FragPipe (open search)">

### Step 2. Detect PTMs using AutoMod

### Parameters

There are two sections in the AutoMod parameter file, including the basic and the advanced. Users can specify the output file path, number of PTMs in a combination, and the number of exported patterns in the basic section. The advanced section provides 109 PTM candidates collected from UniProt, and users can customize the PTM list by adding or deleting PTM candidates if necessary.

- Basic parameters

|        Name         |  Default Value | Comments |
|---------------------|----------------|------------------------------|
| output              | D:\test        | the location of output files |
| fragger_param_path  | (can be empty) | path to the MSFragger closed search parameter file  |
| num_threads         | -1             | number of threads used in the process. "-1" means that AutoMod will use (total number of threads - 1) in your computer for processing  |
| num_ptm_comb        |  4             | maximum combination number of post-translational modification per peptide |
| precursor_mass_tolerance    |  20    | precursor mass tolerance (unit: ppm) |
| output_pattern_num  | 10             | export top N patterns based on the number of matches |
| min_match           | 10             | print out the patterns with the minimum match number |
| frag_site           | true           | use the suggested ptm sites in MSFragger open search results |

- PTM candidates
  
  Please follow the format when adding new PTM candidates: **UniqueMass@AminoAcid**. For example, ptm: 79.966331@DRCHSTY or ptm: 15.9949@M.

### Commands
- For a single pepXML file
  > `xjar.exe java --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar AutoMod.jar path\AutoMod.yml path\pepXML`
  > 
  > e.g., `xjar.exe java --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar AutoMod.jar AutoMod.yml D:\test1.pepXML`


- For multiple pepXML files
  > `xjar.exe java --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar AutoMod.jar path\AutoMod.yml path\pepXML1 path\pepXML2 path\pepXML3`
  > 
  > e.g., `xjar.exe java --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar AutoMod.jar AutoMod.yml test1.pepXML test2.pepXML test3.pepXML`
  > 
  > `xjar.exe java --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar AutoMod.jar param-file-path folder-path\*.pepXML`
  > 
  > e.g., `xjar.exe java --add-opens java.base/jdk.internal.loader=ALL-UNNAMED -jar AutoMod.jar AutoMod.yml D:\*.pepXML`

### Output files

AutoMod exports two output files, including details.tsv and mod-pattern.tsv. The details.tsv lists the mass differences and their corresponding PTMs with the confidence and support values, whereas the mod-pattern.tsv lists the top _N_ PTM patterns which can be further apply for closed searches.

<br>

### Step 3. Apply modification patterns in closed searches

As the recommended PTM patterns are obtained, one can easily use for closed searches with any search engine (including Sequest, MS Amanda, and MSFragger).

<br>


## License

A US patent has been filed for AutoMod (application number: 18142035). It is currently free for academic use. Please contact us (email: dr.chuiyin@gmail.com) if you intend to use the software tool for commercial purpose.

<br>

## Frequently Asked Questions (FAQ)



