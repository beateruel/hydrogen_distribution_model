# Dutch Hub WWTP–electrolysis–hydrogen System Dynamics model (IS2H4C)

System Dynamics model of the integrated wastewater treatment plant (WWTP) and renewable hydrogen system of the Dutch Hub (H2Hub Twente). Reclaimed water from the WWTP feeds an electrolyser, electrolytic oxygen partially replaces WWTP aeration, an on-site store buffers hydrogen production, and an external supply with an order-up-to policy covers the demand not met on site. The model runs at hourly resolution and reports hydrogen supply, resource circularity and electricity indicators.

The model was developed in Work Package 4 of the IS2H4C project and is documented in Deliverable D4.3 *Hub logistics and supply chain management*, Section 5.3 and Appendix 2.

## Repository contents

```
hydrogen_distribution_model/
├── README.md
├── LICENSE
├── CITATION.cff
├── inputs/
│   ├── parameters_and_sources.xlsx                 Parameters, values, units and sources
│   └── Dutch_Hub_data_and_crematorium_demand.xlsx  CBS weekly deaths and the seasonal index of the crematorium demand
├── model/
│   ├── electrolysis_baseline.mdl                   Verification (baseline) model (Vensim)
│   └── baseline_model_results.xlsx                 Baseline indicators (D4.3, Tables 27 and 29, Figure 27)
├── verification_scenarios/
│   └── verification_scenarios_summary.xlsx         Scenarios S1–S3 (D4.3, Section 5.3.5, Tables A2.1–A2.3, Figure 28)
└── validation_scenarios/
    ├── BV1/   Expected demand with the planned configuration
    ├── BV2/   Electrolyser and storage sizing (BV2a) and phased expansion (BV2b)
    └── BV3/   Robustness of the external hydrogen supply to logistics changes
```

Each validation folder contains the Vensim model, a results workbook and a text file with the changes made to the model for that scenario:

```
validation_scenarios/
├── BV1/  electrolysis_BV1.mdl, BV1_hydrogen_results_summary.xlsx, BV1_vensim_changes.txt
├── BV2/  electrolysis_BV2.mdl, BV2_hydrogen_results_summary.xlsx, BV2_step_function.txt
└── BV3/  electrolysis_BV3.mdl, BV3_hydrogen_results_summary.xlsx, BV3_step_function.txt
```

The results workbooks follow the same colour code: blue = input or Vensim data, black = formula, green = link to another sheet.

## Requirements

The `.mdl` files open with Vensim (Ventana Systems); the free Vensim PLE can open and run them. The Excel workbooks need no additional software.

Simulation output files (`.vdfx`) are not included. All results can be reproduced with the models and the settings below, and the values used in the deliverable are stored in the Excel workbooks.

## Reproducing the results

All runs use an hourly time step.

| Scenario | Model | Settings | Horizon | Workbook |
|---|---|---|---|---|
| Baseline | `model/electrolysis_baseline.mdl` | Parameters as in `inputs/parameters_and_sources.xlsx` | 336 h (2 weeks) | `model/baseline_model_results.xlsx` |
| S1 — Increasing hydrogen demand | `model/electrolysis_baseline.mdl` | Crematorium demand +20% every 24 h | 336 h | `verification_scenarios/verification_scenarios_summary.xlsx` |
| S2 — Reduced recycled water | `model/electrolysis_baseline.mdl` | Recycled water reduced with a ramp; potable water covers the shortfall | 336 h | idem |
| S3 — Increasing electrolyser capacity | `model/electrolysis_baseline.mdl` | Electrolyzer capacity multiplier = 2, 5, 10, 15, 20, 25 | 336 h | idem |
| BV1 — Expected demand | `validation_scenarios/BV1/electrolysis_BV1.mdl` | Bakery 1 kg H₂/h; crematorium demand with seasonal index and weekly noise (seed 1); electrolyser 1 kg H₂/h; storage 200 kg. See `BV1_vensim_changes.txt` | 26,208 h (156 weeks) | `BV1_hydrogen_results_summary.xlsx` |
| BV2 — Electrolyser and storage sizing | `validation_scenarios/BV2/electrolysis_BV2.mdl` | BV2a: electrolyser 1, 2, 4, 6, 7, 8 kg H₂/h with 200 or 500 kg storage. BV2b: 1 → 4 → 8 kg H₂/h in years 1–3. See `BV2_step_function.txt` | 26,208 h | `BV2_hydrogen_results_summary.xlsx` |
| BV3 — Logistics robustness | `validation_scenarios/BV3/electrolysis_BV3.mdl` | BV2b configuration; one logistics variable changed at a time: safety coverage 0 or 48 h, lead time 48 h, review period 72 h, outsourced capacity 800 kg, and two combinations. See `BV3_step_function.txt` | 26,208 h | `BV3_hydrogen_results_summary.xlsx` |

The exact settings of each run are listed in the sheets Parameters and Runs of each workbook.

## Data and limitations

Input data come from H2Hub Twente (pilot configuration and hydrogen demand), the STOWA (2018) report on the Katwoude WWTP, the literature and Statistics Netherlands (CBS). All sources are listed in `inputs/parameters_and_sources.xlsx`.

The CBS weekly deaths data in `inputs/Dutch_Hub_data_and_crematorium_demand.xlsx` are published by Statistics Netherlands under the CC BY 4.0 licence (StatLine table 70895ENG).

The model is a pilot-scale representation for exploring operating regimes and bottlenecks. WWTP parameters are taken from a reference case study and are pending validation for the Almelo WWTP. Its results are illustrative and do not constitute a validated industrial design. Limitations are discussed in D4.3, Section 5.3.8.

## How to cite

Please cite this repository as indicated in `CITATION.cff` (GitHub: "Cite this repository").

## Funding

This work was carried out within the IS2H4C project (*Sustainable Circular Economy Transition: From Industrial Symbiosis to Hubs for Circularity*), funded by the European Union under grant agreement No 101138473. Views and opinions expressed are however those of the author(s) only and do not necessarily reflect those of the European Union or HADEA. Neither the European Union nor the granting authority can be held responsible for them.

## Licence

MIT License. See `LICENSE`. The CBS data keep their CC BY 4.0 licence.

## Contact

Beatriz Royo, Zaragoza Logistics Center (ZLC).
