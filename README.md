# Gradient foam-filled spiral tube finite element dataset

This dataset contains 1,342 finite element simulations of gradient foam-filled spiral tubes under axial compression. It accompanies the manuscript *Multistage prediction of displacement fields and inverse design of gradient foam-filled spiral tubes under deformation constraints*. Each case has ten design variables, crashworthiness indicators, a 101-point force-displacement curve and displacement fields on the spiral tube midsurface at six compression stages.

## Files and case splits

| File | Contents |
| --- | --- |
| `dataset_manifest.csv` | One row per case, with design variables, crashworthiness indicators, split and the locations of the matching curve and displacement field |
| `splits.csv` | The original case-level split of 1,074 training, 134 validation and 134 test cases. The validation label is `val`. |
| `curves.npz` | The arrays `case_ids`, `displacement_mm` and `force_n`. Both numerical arrays have shape `(1342, 101)`. The manifest's zero-based `curve_row_index` identifies the corresponding row. |
| `gffst-fields-train-01.zip` through `gffst-fields-train-04.zip` | Training displacement fields |
| `gffst-fields-validation.zip` and `gffst-fields-test.zip` | Validation and test displacement fields |
| `SHA256SUMS.txt` | SHA-256 checksums for the data files and field archives |

The displacement archives are in the Release assets (the `release-assets` folder in the local package). Each archive member is named `fields/<case_id>.npz`. The manifest provides the archive filename, member path and a SHA-256 checksum of the individual NPZ.

## Design variables and indicators

| Column(s) | Definition and unit |
| --- | --- |
| `wave_height`, `wave_number`, `bellows_thickness` | Spiral tube corrugation height in mm, corrugation count, and tube wall thickness in mm |
| `foam_t_lower`, `foam_t_middle`, `foam_t_upper` | Foam cell wall thickness by axial layer in mm |
| `density_lower`, `density_middle`, `density_upper` | Fractions of the Voronoi seed points allocated to the three axial layers; dimensionless and normalized to sum to one |
| `N` | Total number of Voronoi seed points |
| `sea_kj_per_kg`, `ipcf_n`, `mcf_n` | Specific energy absorption in kJ/kg, initial peak crushing force in N, and mean crushing force in N |
| `cfe_percent`, `mass_kg` | Crushing force efficiency in percent and structural mass in kg |

## Displacement fields

Open the NPZ files with NumPy using `allow_pickle=False`. The `fields` array has shape `(6, 3, 192, 128)`, with axes for compression stage, displacement component, axial coordinate and circumferential angle. The three components are radial, circumferential and axial displacement, all in mm, resolved in the initial cylindrical basis. The exported fields retain the original simulation values. The nominal compression stages are approximately 0, 12, 24, 36, 48 and 60 mm. The arrays `actual_displacement_mm` and `target_displacement_mm` record the selected and target compression levels for each case.

`grid_y_normalized` gives the normalized axial coordinates, `grid_theta_rad` gives the periodic circumferential coordinates, and `grid_valid_mask` gives the source grid validity mask. `initial_xyz_mm` contains the three Cartesian coordinates of the initially sampled midsurface grid in mm and has shape `(3, 192, 128)`.

Use `case_id` to join the manifest, curves, fields and split assignments. The split is preserved by complete simulation case. The package covers the finite element dataset used for training and evaluation.

## Citation

Cite the paper together with the tagged dataset release **v1.0.0**.

