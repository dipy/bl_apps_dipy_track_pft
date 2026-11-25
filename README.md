<h1 align="center">Tracking using Particle Filtering (PFT)</h1>

<p align="center">
  Tracks streamlines with DIPY particle filtering tractography (dipy_track_pft, 1.1.1) from peaks with white matter, gray matter and CSF maps, and outputs a .trk tractogram.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.328"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.328-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Tracks streamlines with DIPY particle filtering tractography (dipy_track_pft, 1.1.1) from peaks with white matter, gray matter and CSF maps, and outputs a .trk tractogram.**

Runs dipy_track_pft, which uses anatomically constrained particle filtering to recover streamlines that stop in invalid tissue. Use it when you have ODF peaks (for example from CSA or CSD fitting) and tissue masks in diffusion space. Seeds are placed in the seed mask at seed_density per voxel dimension.

| | |
|---|---|
| **Inputs** | `neuro/peaks_and_metrics` · `neuro/mask` ×4 |
| **Outputs** | `neuro/track/trk` |
| **Container** | `brainlife/dipy:1.1.1` |
| **Resources** | 8 CPUs |
| **Run it** | [doi.org/10.25663/brainlife.app.328](https://doi.org/10.25663/brainlife.app.328) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `peaks` | `neuro/peaks_and_metrics` | yes | ODF peaks and metrics (DIPY .pam5) used for direction getting. |
| `wm` | `neuro/mask` (white_matter, dwi) | yes | White matter map in diffusion space (include map). |
| `gm` | `neuro/mask` (gray_matter, dwi) | yes | Gray matter map in diffusion space. |
| `csf` | `neuro/mask` (csf, dwi) | yes | CSF map in diffusion space (exclude map). |
| `seeds` | `neuro/mask` (dwi) | yes | Seed mask in diffusion space. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/track/trk` | Tractogram (track.trk). |

<details>
<summary><b>Parameters</b> (7)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `step_size` | number | `0.2` | Step size used for tracking (default 0.2mm). |
| `seed_density` | number | `1` | Number of seeds per dimension inside voxel (default 1). For example, seed_density of 2 means 8 regularly distributed points in the voxel. |
| `pmf_threshold` | number | `0.1` | Threshold for ODF functions (default 0.1). |
| `max_angle` | number | `20` | Maximum angle between streamline segments (range [0, 90], default 20). |
| `pft_back` | number | `2` | Distance in mm to back track before starting the particle filtering tractography (default 2mm). The total particle filtering tractography distance is equal to back_tracking_dist + front_tracking_dist. |
| `pft_front` | number | `1` | Distance in mm to run the particle filtering tractography after the back track distance (default 1mm). The total particle filtering tractography distance is equal to back_tracking_dist + front_tracking_dist. |
| `pft_count` | number | `15` | Number of particles to use in the particle filter (default 15). |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.328](https://doi.org/10.25663/brainlife.app.328), choose `neuro/peaks_and_metrics`, `neuro/mask`, `neuro/mask`, `neuro/mask`, `neuro/mask` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/track/trk`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/dipy:1.1.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "peaks": "/path/to/peaks/peaks",
       "wm": "/path/to/wm/wm",
       "gm": "/path/to/gm/gm",
       "csf": "/path/to/csf/csf",
       "seeds": "/path/to/seeds/seeds",
       "step_size": 0.2,
       "seed_density": 1,
       "pmf_threshold": 0.1,
       "max_angle": 20,
       "pft_back": 2,
       "pft_front": 1,
       "pft_count": 15
   }
   ```

3. Run `./main`.

## DIPY

- This is a Brainlife wrapper App stemming from the [`dipy_track_pft`](https://dipy.org/documentation/latest/reference_cmd/dipy_track_pft/) workflow.
- This single wrapper is exposed through an apps registered on [Brainlife.io](https://brainlife.io).
- More information about DIPY : [https://dipy.org/](https://dipy.org/).
- More information about the command line `dipy_track_pft`: [Command line Reference](https://dipy.org/documentation/latest/reference_cmd/dipy_track_pft/).

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Tracking using Particle Filtering (PFT). brainlife.io App. [doi:10.25663/brainlife.app.328](https://doi.org/10.25663/brainlife.app.328)
- Garyfallidis E, et al. Dipy, a library for the analysis of diffusion MRI data. Front Neuroinform 8:8 (2014). [doi:10.3389/fninf.2014.00008](https://doi.org/10.3389/fninf.2014.00008)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Serge Koudoro
- Javier Ricardo Guaje Guerra

**Contributors**

- Soichi Hayashi

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>

## License

See [LICENSE](LICENSE).
