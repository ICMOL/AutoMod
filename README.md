## Introduction


## How to Use

AutoMod requires two input files, including _open search pepXML files_ and _a corresponding parameter file_.

**Step 1.** Generate open search pepXML files using MSFragger


**Step 2.** Mine PTMs using AutoMod


**Step 3.** Apply modification patterns in the closed search


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
