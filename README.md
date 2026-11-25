[![Abcdspec-compliant](https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg)](https://github.com/brain-life/abcd-spec)
[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.328-blue.svg)](https://doi.org/10.25663/brainlife.app.328)

# Dipy Tractography

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Tracks streamlines with DIPY particle filtering tractography (dipy_track_pft, 1.1.1) from peaks with white matter, gray matter and CSF maps, and outputs a .trk tractogram.**

Runs dipy_track_pft, which uses anatomically constrained particle filtering to recover streamlines that stop in invalid tissue. Use it when you have ODF peaks (for example from CSA or CSD fitting) and tissue masks in diffusion space. Seeds are placed in the seed mask at seed_density per voxel dimension.

| | |
|---|---|
| 📥 **Inputs** | `neuro/peaks_and_metrics` · `neuro/mask` ×4 |
| 📤 **Outputs** | `neuro/track/trk` |
| 🐳 **Container** | `brainlife/dipy:1.1.1` |
| ⚙️ **Resources** | 8 CPUs |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.328](https://doi.org/10.25663/brainlife.app.328) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `peaks` | `neuro/peaks_and_metrics` | yes | ODF peaks and metrics (DIPY .pam5) used for direction getting. |
| `wm` | `neuro/mask` (white_matter, dwi) | yes | White matter map in diffusion space (include map). |
| `gm` | `neuro/mask` (gray_matter, dwi) | yes | Gray matter map in diffusion space. |
| `csf` | `neuro/mask` (csf, dwi) | yes | CSF map in diffusion space (exclude map). |
| `seeds` | `neuro/mask` (dwi) | yes | Seed mask in diffusion space. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/track/trk` | Tractogram (track.trk). |

<details>
<summary><b>⚙️ Parameters</b> (7)</summary>

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

📚 **References used by this App:**
- Garyfallidis E, et al. Dipy, a library for the analysis of diffusion MRI data. Front Neuroinform 8:8 (2014). [doi:10.3389/fninf.2014.00008](https://doi.org/10.3389/fninf.2014.00008)
- Avesani P, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

<!-- brainlife-app:end -->

The App uses the Particle Filtering Tracking method to do a tractography.

### Authors
- [Serge Koudoro](skoudoro@iu.edu)
- [Javier Ricardo Guaje Guerra](jrguajeg@iu.edu)

### Contributors
- [Soichi Hayashi](soichih@gmail.com)

### Funding Acknowledgement
brainlife.io is publicly funded and for the sustainability of the project it is helpful to Acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your code and publications. Copy and past the following lines into your repository when using this code.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)

### Citations
We ask that you the following articles when publishing papers that used data, code or other resources created by the brainlife.io community.

1. Garyfallidis, E., Brett, M., Amirbekian, B., Rokem, A., van der Walt, S., Descoteaux, M., Nimmo-Smith, I., & Dipy Contributors (2014). Dipy, a library for the analysis of diffusion MRI data. Frontiers in neuroinformatics, 8, 8. [https://doi.org/10.3389/fninf.2014.00008](https://doi.org/10.3389/fninf.2014.00008)

2. Avesani, P., McPherson, B., Hayashi, S. et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6, 69 (2019). [https://doi.org/10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Running the App

#### 1. On Brainlife.io

You can see a list of [Dipy Apps currently regsitered on Brainlife](https://brainlife.io/apps#dipy). Find the App that you'd like to run and click "Execute" tab to specify dataset that you'd like to run the App on.

#### 2. On  your machine (Running Locally)

To run this command, you can simply type:

`singularity exec -e docker://brainlife/dipy:1.1.1 dipy_track_pft [your_args]`

To see the documentation of all arguments, [go to the following page](https://dipy.org/documentation/1.1.1./reference_cmd/dipy_track_pft/)

## Input

To see the documentation of all the arguments, follow this [link](https://dipy.org/documentation/1.1.1./reference_cmd/dipy_track_pft/).

## Output

All output files will be generated according to the passed arguments, as explained [here](https://dipy.org/documentation/1.1.1./reference_cmd/dipy_track_pft/).

### Dependencies

This app runs on [singularity](https://www.sylabs.io/singularity/).

### DIPY
- This is a Brainlife wrapper App stemming from the [`dipy_track_pft`](https://dipy.org/documentation/latest/reference_cmd/dipy_track_pft/) workflow.
- This single wrapper is exposed through an apps registered on [Brainlife.io](https://brainlife.io).
- More information about DIPY : [https://dipy.org/](https://dipy.org/).
- More information about the command line `dipy_track_pft`: [Command line Reference](https://dipy.org/documentation/latest/reference_cmd/dipy_track_pft/).
