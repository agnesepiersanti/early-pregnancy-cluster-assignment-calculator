# Early-Pregnancy Metabolic Phenotype Calculator

Interactive web-based calculator for assigning patients to the metabolic
phenotypes (clusters) described in the accompanying study.

## Overview

This repository provides the reference implementation of the
**Early-Pregnancy Metabolic Phenotype Calculator**. The tool implements
the patient cluster-assignment procedure reported in **Table 2** of the
manuscript:

> *Early pregnancy data-driven cluster phenotyping defines risk
> constellations for later gestational diabetes and adverse outcomes.*

The calculator accepts six variables:

-   Age
-   Pre-pregnancy BMI
-   Fasting glucose (OGTT 0 min)
-   60-min glucose (OGTT)
-   120-min glucose (OGTT)
-   Triglycerides

It can be used either for:

1.  **Single-patient assignment**, by entering values directly in the
    browser; or
2.  **Batch assignment**, by uploading an `.xlsx`/`.xls` spreadsheet and
    downloading a new spreadsheet containing the assigned cluster and
    calculated distances.

The web application is implemented as a standalone `index.html` file and
runs entirely in the user's browser.

## Method

For each patient, glucose and triglyceride measurements are converted to
the standard units used by the model (mmol/L where applicable). Each of
the six variables is then standardized using the mean and standard
deviation of the study cohort.

The standardized patient profile is compared with the two cluster
centroids using Euclidean distance:

**Dₖ = √ Σᵢ (zᵢ − cₖᵢ)²**

The patient is assigned to the cluster with the smaller Euclidean
distance.

The implementation contains the cohort means, standard deviations, and
cluster centroids used for this procedure.

## Input format

For batch processing, the spreadsheet should contain one row per patient
and the following columns:

  Column        Description
  ------------- ---------------------------------------
  `PatientID`   Patient identifier chosen by the user
  `Age`         Age in years
  `BMI`         Pre-pregnancy BMI (kg/m²)
  `OGTT0`       Fasting glucose
  `OGTT60`      60-min glucose
  `OGTT120`     120-min glucose
  `TG`          Triglycerides

Glucose and triglyceride units can be selected in the calculator before
processing the spreadsheet.

A spreadsheet template can also be generated directly from the
calculator.

## Privacy

All patient-level calculations are performed **locally in the user's
browser**. Patient data uploaded to the calculator are not transmitted
to or stored on a study server.

The application uses the SheetJS library loaded from a public CDN to
read and write spreadsheet files. No backend server or database is
required.

**Important:** users should nevertheless follow their institutional
policies and applicable data-protection requirements when handling
patient data.

## Intended use and disclaimer

This calculator is provided for **research transparency, methodological
reproducibility, and exploration of the cluster-assignment procedure
described in the accompanying study**.

It is **not a medical device and is not intended to provide clinical
diagnosis, treatment recommendations, or individual clinical
decision-making**.

The cluster centroids and normalization parameters are derived from the
study/training population (DALI and GESTDIA) and have **not been
externally validated** for general clinical use. Cluster assignments
should therefore be interpreted in the context of the study population
and methodology.

## Artificial intelligence disclosure

The code and user-interface implementation of this calculator were
developed with the **assistance of artificial intelligence (AI)-based
coding tools**. AI assistance was used for aspects of code generation,
implementation, and interface development.

The scientific methodology, input variables, normalization procedure,
cluster centroids, and interpretation of the results are based on the
study methodology and were reviewed and verified by the authors.

AI assistance does not replace author responsibility for the
correctness, reproducibility, and scientific validity of the
implementation.

## Repository contents

``` text
early-pregnancy-cluster-assignment-calculator/
├── index.html
└── README.md
```

## Web application

The calculator can be accessed through the GitHub Pages deployment
associated with this repository.

If GitHub Pages is enabled, the URL will generally follow this
structure:

``` text
https://<username>.github.io/<repository-name>/
```

## Citation

If you use this calculator or its implementation in academic work,
please cite the accompanying manuscript:

> *Early pregnancy data-driven cluster phenotyping defines risk
> constellations for later gestational diabetes and adverse outcomes.*

Please also cite this repository when referring specifically to the
software implementation.

## Reproducibility

The repository is intended to make the cluster-assignment procedure
transparent and reproducible. The `index.html` file contains the
complete client-side implementation required to run the calculator; no
local installation, compilation, or server-side processing is required.
