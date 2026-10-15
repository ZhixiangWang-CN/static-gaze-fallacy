# Software review guide

This guide accompanies the manuscript *Human gaze defines conditional supervision targets in
medical imaging AI* and is intended for editors and peer reviewers.

## System requirements

- Python 3.10 or 3.11; the packaged environment pins Python 3.11.
- Base dependencies and tested versions are listed in `environment.yml` and `pyproject.toml`.
- The continuous-integration workflow tests the base package successfully on GitHub Actions
  `ubuntu-latest` with Python 3.10 and 3.11.
- The authors also ran the unit tests and data-free demonstration on macOS 26.5.1 (Apple silicon)
  with Python 3.12.13.
- The data-free demo and base analyses require only a standard CPU. A CUDA-capable GPU is
  recommended for the optional ResNet training experiments.

## Installation

```bash
git clone https://github.com/ZhixiangWang-CN/static-gaze-fallacy.git
cd static-gaze-fallacy
conda env create -f environment.yml
conda activate eyeassist-reproducibility
python -m pip install -e '.[dev]'
```

Installation typically takes approximately 5--15 minutes on a standard desktop computer,
depending on the package manager and network connection.

## Data-free demonstration

```bash
python -m unittest discover -s tests -v
python examples/synthetic_demo.py --output outputs/synthetic_demo
```

The demonstration constructs simulated gaze data and does not require clinical images or gaze
records. It writes:

- `outputs/synthetic_demo/summary.json`;
- `outputs/synthetic_demo/held_out_scores.csv`;
- `outputs/synthetic_demo/group_disjoint_splits.csv`.

On the authors' reference workstation (macOS 26.5.1 on Apple silicon, Python 3.12.13), the synthetic demo
completed in approximately 2 seconds. Exact time varies with hardware and environment.

## Use with authorized study data

The controlled EyeAssist data are available through the gated repository linked in `README.md`.
Authorized users place the data under `data/private/`, copy
`configs/analysis.example.yaml` to `configs/analysis.yaml`, and edit only that local configuration
and manifest. The analysis map in `README.md`, the data specification in
`docs/DATA_SCHEMA.md`, and the claim-to-code crosswalk in `docs/METHODS_TO_CODE.md` provide the
commands, expected inputs and outputs for each analysis.

The public GazeVaLM analysis is documented separately in `external/gazevalm/README.md`.

## Reproduction boundary

The repository includes the source code, configurations, deterministic unit tests, a data-free
end-to-end demonstration and the analysis specification. Clinical images, gaze records,
case-level predictions, fitted weights and derived numerical result files are not redistributed.
Consequently, the data-free demonstration is directly runnable by reviewers, whereas full
reproduction of the EyeAssist numerical results requires authorized access to the controlled data.

## License

The source code is released under the OSI-approved MIT License. See `LICENSE` in the repository
root for the complete terms.
