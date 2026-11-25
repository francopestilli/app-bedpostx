<h1 align="center">bedpostx</h1>

<p align="center">
  Fits FSL BedpostX (GPU version, FSL 6.0.1) multi-fibre ball-and-stick models to preprocessed DWI within a brain mask, producing the sample distributions needed for probabilistic tractography.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.578"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.578-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Fits FSL BedpostX (GPU version, FSL 6.0.1) multi-fibre ball-and-stick models to preprocessed DWI within a brain mask, producing the sample distributions needed for probabilistic tractography.**

Runs bedpostx_gpu on the DWI, bvals, bvecs and nodif brain mask to estimate up to nf fibre orientations per voxel with MCMC sampling. Use it before FSL probtrackx. Needs preprocessed (eddy/motion corrected) DWI and a brain mask in the same space, and a GPU node.

| | |
|---|---|
| **Inputs** | `neuro/dwi` · `neuro/mask` |
| **Outputs** | `neuro/FSLBedpostX` |
| **Container** | `brainlife/fsl:6.0.1` |
| **Resources** | 8 CPUs · 16 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.578](https://doi.org/10.25663/brainlife.app.578) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `dwi` | `neuro/dwi` (preprocessed) | yes | A 4D series of data volumes. This will include diffusion-weighted volumes and volume(s) with no diffusion weighting. |
| `mask` | `neuro/mask` (dwi, brain, preprocessed) | yes | 3D binary brain mask volume derived from running bet on nodif (i.e. on a volume with no diffusion weighting). Created using FSL Brain Extraction (BET) on DWI brainlife/app-FSLBET |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `neuro/FSLBedpostX` | This folder contains the entire set of folders and files outputted by the FSL BedpostX process |

<details>
<summary><b>Parameters</b> (3)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `nf` | number | `3` | Maximum number of fibres to fit in each voxel. |
| `bi` | number | `1000` | burnin period, default 1000 |
| `fudge` | number | `1` | ARD fudge factor (integer) controlling automatic relevance determination of extra fibres. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.578](https://doi.org/10.25663/brainlife.app.578), choose `neuro/dwi`, `neuro/mask` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/FSLBedpostX`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/fsl:6.0.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "dwi": "/path/to/dwi/dwi",
       "bvecs": "/path/to/dwi/bvecs",
       "bvals": "/path/to/dwi/bvals",
       "sbref": "/path/to/dwi/sbref",
       "sbref_json": "/path/to/dwi/sbref_json",
       "mask": "/path/to/mask/mask",
       "nf": 3,
       "bi": 1000,
       "fudge": 1
   }
   ```

3. Run `./main`.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- bedpostx. brainlife.io App. [doi:10.25663/brainlife.app.578](https://doi.org/10.25663/brainlife.app.578)
- Jenkinson et al. FSL. *NeuroImage* 62:782-790 (2012). [doi:10.1016/j.neuroimage.2011.09.015](https://doi.org/10.1016/j.neuroimage.2011.09.015)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

Maintained by [@sandrahanekamp](https://github.com/sandrahanekamp).
