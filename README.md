# tcell-ontology
Metaanalysis ontology

Metadata annotation is the same as single-cell-curation schema v. 3.0.0 (see [here](https://github.com/chanzuckerberg/single-cell-curation/blob/d39a93274ea10c54064bffec59eed0cce2c21413/schema/3.0.0/schema.md))


# Metadata / .obs attribute 

## General information 

| Key | Description | Type | Examples |
| --- | --- | --- | --- |
| study_id | Unique identifier of study | str | | 
| donor_id | Unique identifier of donor | str | |
| sample_id | Unique identifier of sample | str | |
| cell_id | Unique identifier of cell | str |
| is_primary_data | Whether it is primary data (true) or otherwise collected data (false). False for initial studies | bool | | 
| organism_ontology_term_id | Organism ontology defined by NCBI taxonomy | str | Homo sapiens: NCBITaxon:9606, Mus musculus: NCBITaxon:100090 | 
| organism | Organism corresponding to `organism_ontology_term_id` | str | Homo sapiens, Mus musculus


## Patient-level information

| Key | Description | Type | Examples |
| --- | --- | --- | --- |
| development_stage_ontology_term_id | Developmental stage | str | Human <1m: Human neonate stage HsapDv:0000082, Human 1m-23m: HsapDv:0000083, Human 2y-12y: HsapDv:0000081, 13y-18y: HsapDv:0000086, >18y HsapDv:0000087 | 
| development_stage | Development stage corresponding to `development_stage_ontology_term_id` | str | human neonate stage, human infant stage, human child stage, human adolescent stage, human adult stage |
| disease_ontology_term_id | PATO identifier of disease | str | PATO:XXXX |  
| disease | Disease name corresponding to `disease_ontology_term_id` | str | |
| disease_severity_scale | Name of disease severity scale | str | e.g. Tumor scale, viral load | 
| disease_severity_scale_type | type of disease severity | str | Type of scale nominal/ordinal/standardized (standardized ordinal scale such as tumor stage)/metric | 
| disease_severity_score | Score of disease severity scaled from 0 (minimum in dataset) to 1 (maximum in dataset) | float | |
| disease_severity_score_original | Score of disease severity on original scale | (varies) | healthy/mild/severe, 0-4, etc. | 
| sex_ontology_term_id | PATO ID of sex. | str | female: PATO:0000383, male: PATO:0000384, "unknown" | 
| sex | Sex corresponding to sex_ontology_term_id | str | female, male, unknown
| self_reported_ethnicity_ontology_term_id | Self reported ethinicity ID as defined by HANCESTRO | str | white/european/caucasian: HANCESTRO:0005, Middle Eastern/North African: HANCESTRO:0015, afro-american/carribean: HANCESTRO:0016, asian (east asia, south asia, south east asia) HANCESTRO:0008, hispanic/south-american: HANCESTRO:0014, Native american: HANCESTRO:0013, Oceanian: HANCESTRO:0017, african: HANCESTRO:0010, multiethnic, unknown, na (non human) |
| self_reported_ethnicity  | Ethnicity corresponding to `self_reported_ethnicity_ontology_term_id` | str | white, afro-american, african, asian, hispanic, native american, oceanian, multiethnic, unknown, na (non human) | 
| lifestyle_smoking_status | Whether the patient smokes or not | str | never, previous, smoker, na |
| lifestyle_bmi | Body mass index | float | float | float/na |


## Sample-level information 

| Key | Description | Type | Examples |
| --- | --- | --- | --- |
| assay_ontology_term_id | Assay ID, defined by the Experimental Factor Ontology (EFO) | str | 10x 3' v2 "EFO:0009899", 10x 3' v3	"EFO:0009922", 10x 5' v1 "EFO:0011025", "EFO:0011025" "EFO:0009900", Smart-seq	"EFO:0008930", Smart-seq2	"EFO:0008931"
| assay | Assay corresponding to `assay_ontology_term_id` | str | 10x 3' v2, 10x 3' v3, 10x 5' v1, 10x 5' v2, Smart-seq, Smart-seq2
| suspension_type | Single cell or single nucleus sequencing | Literal['cell', 'nucleus', 'na'] | 'cell', 'nucleus', 'na' | 
| tissue_ontology_term_id | UBERON ID of tissue. If enriched/sorted MUST be an UBERON or CL term and SHOULD NOT use terms that do not capture the tissue of origin | str | UBERON:XXX |  
| tissue | Tissue `corresponding to tissue_ontology_term_id` | str | |
| tissue_location_level_0 | Coarse tissue location | str | large intestine, small intestine, lung |
| tissue_layer | Precise tissue location | str | e.g. lamina propria/epithelium |
| sample_disease_status | Disease status of sample, relevant if multiple samples were taken from the same patient | str | healthy (if patient is healthy), non_affected if non-affected tissue is taken from affected subject, affected (if affected tissue is taken), affected_metastases (In case of tumor metastases), systemic (e.g. if blood of affected subject is taken or disease affects the whole system)

## Cell-level information

| Key | Description | Type | Examples |
| --- | --- | --- | --- |
| cell_type_ontology_term_id | cell type as defined by the CL ontology | str | CL:XX |
| cell_type | cell type corresponding to `cell_type_ontology_term_id` | str | |
| cell_type_original | annotation from original authors | str | T cell |
| cell_type_original_level_0 | Coarse cell type annotation (same for all studies) | str (default: empty)| Immune cell | 
| cell_type_original_level_1 | Finer cell type annotation (same for all studies) | str (default: empty) | T cell lineage | 
| cell_type_original_level_2 | Finer cell type annotation (same for all studies) | str (default: empty) | T cell | 
| cell_type_original_level_3 | Finer cell type annotation (same for all studies) | str (default: empty) | CD4-positive alpha-beta T cell | 
| cell_type_original_level_4 | Finer cell type annotation (same for all studies), same annotation level as human lung atlas | str (default: empty) |  T helper 1 cell | 
| cell_type_level_0 | Coarse cell type annotation (same for all studies) | str (default: empty)| Immune cell | 
| cell_type_level_1 | Finer cell type annotation (same for all studies) | str (default: empty) | T cell lineage | 
| cell_type_level_2 | Finer cell type annotation (same for all studies) | str (default: empty) | T cell | 
| cell_type_level_3 | Finer cell type annotation (same for all studies) | str (default: empty) | CD4-positive alpha-beta T cell | 
| cell_type_level_4 | Finer cell type annotation (same for all studies), same annotation level as human lung atlas | str (default: empty) | T helper 1 cell | 


Available cell types are stored in celltype-mapping.tsv. Mapping format is similar to human lung cell atlas by the Theis Lab ([Sikkema et al, 2022](https://doi.org/10.1101/2022.03.10.483747))


# .var

Key | Description | Type | Example |
| --- | --- | --- | --- |
index | ENSEMBL ID | int | |
feature_is_filtered | False | bool | 
feature_biotype | "gene" | Literal['gene'] | |
feature_name | ENSEMBL gene name | str ||
feature_name_original | Original gene name as specified by the authors | str ||
feature_reference | Taxonomy (Human: NCBITaxon:9606, Mus Musculus: NCBITaxon:10090) | str | |
gene_is_mitochondrial | Whether gene is mitochondrial or not | bool | True/False | 


# .uns 

Key | Description | type | Example |
| --- | --- | --- | --- |
schema_version | 3.0.0 | Literal['3.0.0'] | |
title | string | | |
batch_condition | List of covariates that might induce batch effects | List[str] | |
default_embedding | UMAP | str | |
X_approximate_distribution | Do not set (will be set automatically | |
