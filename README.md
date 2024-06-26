# Classifying Antigen Receptors (Antibodies and T-Cell Receptors) with Immunoprofiling

## Background
Immunoprofiling or immune-profiling is used to assess the diversity of antigen receptors (ARs: antibodies and T-Cell receptors) and how this diversity changes in response to allergens, infections, or vaccines. Understanding AR diversity helps scientists develop new vaccines, improve existing vaccines, and treat allergies and disease. Diversity is assessed by sequencing DNA corresponding to the variable regions of ARs. Learn more about immunoprofiling at https://digitalworldbiology.com/blog/what-immunoprofiling. 

## General Workflow
The common source for antibody seqeunce data comes from immune profiling experiements and assays. 

```mermaid
    flowchart TD
    A[Collect Samples] --> B[Isolate DNA / RNA->cDNA] --> C[PCR] -- V-gene, C-gene primers --> D[Sequence DNA] -- NGS - massively parallel --> E[IgBLAST] -- Vh Dh Jh, Vl Jl, Vk Jk references --> F[Immune Profile Dataset];
    F -- repeat --> A
    F --> G[Explore data, analyze];
    F --> H[Machine learning]; 
```
## Repository Contents
This repository contains the work from a one-week hackathon involving college instructors, high school teachers and students that was focused on leaning immunoprofiling concepts through hands on activities. 

One part of the project utilized precomputed datasets to explore statistical methods that are used in determining AR quality, diversity and clonality, and how clonality is used to understand immune responses in certain cancer. Precomputed datasets are large tables, in [Adaptive Immune Receptor Repertoire(AIRR)](https://docs.airr-community.org/en/stable/) format, that contain sample meta data, v-gene, d-gene, and j-gene annotations/sequences, and note productive and unproductive rearrangements.  

Another part explored bioinformatics workflows needed to prepare AR sequences for statistical analyses. Team members worked with datasets from different databases like [OPIG](https://opig.stats.ox.ac.uk/webapps/covabdab/) and the NCBI short read archive ([example influenza data](https://www.ncbi.nlm.nih.gov/sra/?term=PRJNA349143). A small number of datasets (2 to 4) were prepared and processed with command line tools that include quality filtering, merging forward/reverse reads, sequence alignment via IgBLAST, data parsers, and statistical counting tools.  

## Resources
### Jetstream
The NSF supported Jetstream (https://jetstream-cloud.org/) computing resources supported computation. One 64-core instance was created along with user accounts. See [getting started](https://github.com/AntibodyEngineers/2024-Antibodies-and-AI/blob/main/getting-started.md) for 2024 installation and configuration of the computing enviornment based on [lessons learned](#outcomes-and-lessons)(#6).

### Software
Core software tools and languages include:
- [igBLAST](https://ncbi.github.io/igblast/) allows users to view the matches to the germline V, D, J and C genes, details at rearrangement junctions, the delineation of IG V domain framework regions and complementarity determining regions. The package contains the core igblastn and igblastp programs, plus scripts for formating [databases](#reference-data), and other required operational data. 
- [fastp](https://github.com/OpenGene/fastp) used for adapter and quality triming, and merging raw next generation DNA sequencing data (NGS, Illumina fastq format).   
- Jupyter Notebooks (Lab), via [Jupyter Hub](https://jupyterhub.readthedocs.io/en/stable/) provided web-enabled access to data. Team members had their own notebook runinng in Conda virtual envioment. 
- Python scripts, and libraries (packages), run in Jupyter notebooks, are used to run igblastn and convert output data into tables for exploring immune receptor diversity. [Pandas](https://pandas.pydata.org) is to structure and query large tables and pass data to different statistics, visualization, and ML packages. 
   
### Datasets
- igBLAST inputs
  - TBD
- igBLAST Reference data [see Referenece Sequences in getting started](https://github.com/AntibodyEngineers/2024-Antibodies-and-AI/blob/main/getting-started.md#reference-sequences)
- Precomputed tables  
  - [iReceptor](https://gateway.ireceptor.org) (free account required) lymphoma dataset uptained with the following filters:
    - **Study ID:** PRJEB1289;
    - **Study type:** Case Control (Ontology ID): NCIT:C15197;
    - **Filter by Sample > PCR target:** IGH or IGK or IGL

## Outcomes and lessons
### Outcomes:
1. [Several presentations](/presentations)
2. Documentation for [igBLAST data columns](/IgBlast%20column%20documentation.csv)
3. [Several jupyter notebooks](/notebooks)
   - [ireceptor.ipynb](/ireceptor.ipynb) provides examples with a violin plot showing high clonality in lymphoma.
   - [pandas-igblast-viz.ipynb](/pandas-igblast-viz.ipynb) provides examples of working with igblastn output.
   - [SQLlite3.ipynb](/SQLlite3.ipynb) provides an example of working with igblastn output in an SQLite database.
4. [Documentation](https://github.com/AntibodyEngineers/2024-Antibodies-and-AI/blob/main/getting-started.md) for setting up Jetstream VMs based on lesson 6 below. 
   
### Lessons
1.	Immunoprofiling data are excellent for teaching bioinformatics. Raw data needs to be processed and aligned to reference data. This teaches bioinformatics workflow and scripting commands. The output, very large tables plus metadata files, require programs to view, combine, and navigate data. This teaches data science and statistics concepts (what do various plots mean). Working with real life data teaches ways to employ ML and ask questions about data suitability.
2.	Many team members are new to data science. Being able to accommodate beginning programmers is essential. Jupyter notebooks are well suited for this pupose. 
3.	Individuals with more experience can help with infrastructure and workflows for larger data processing activities.
4.	Pre-hackathon preparation is important. Environments like Google CoLab may be helpful for learning standard tools. Encourage new programmers to try those. Connect Google sheets (small datasets) to pandas to help new programmers understand the data.
5.	Work toward scaling projects to incorporate database concepts and machine learning.
6.	Move to a more centralized repository for Jupyter and python packages. The individual conda virtual environments have administration overhead and result in individuals downloading packages to their home directories which replicates data and requires that storage be managed. 


Hackathons are funded by the National Science Foundation DUE 2055036

Work utalized the Jetstream2 resource:  
David Y. Hancock, Jeremy Fischer, John Michael Lowe, Winona Snapp-Childs, Marlon Pierce, Suresh Marru, J. Eric Coulter, Matthew Vaughn, Brian Beck, Nirav Merchant, Edwin Skidmore, and Gwen Jacobs. 2021. “Jetstream2: Accelerating cloud computing via Jetstream.” In Practice and Experience in Advanced Research Computing (PEARC ’21). Association for Computing Machinery, New York, NY, USA, Article 11, 1–8. DOI: https://doi.org/10.1145/3437359.3465565

Timothy J. Boerner, Stephen Deems, Thomas R. Furlani, Shelley L. Knuth, and John Towns. 2023. ACCESS: Advancing Innovation: NSF’s Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support. “In Practice and Experience in Advanced Research Computing (PEARC ’23)”, July 23–27, 2023, Portland, OR, USA. ACM, New York, NY, USA, 4 pages. https://doi.org/10.1145/3569951.3597559

This work used Jetstream2 at Indiana University through allocation BIO220105 from the Advanced Cyberinfrastructure Coordination Ecosystem: Services & Support (ACCESS) program, which is supported by National Science Foundation grants #2138259, #2138286, #2138307, #2137603, and #2138296
