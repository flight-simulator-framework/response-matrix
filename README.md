# Response Matrix

Calculate how the beam position at each BPM changes when a corrector strength or quadrupole-mover position is varied. The application reconstructs this response from recorded machine snapshots, providing the matrices used for orbit correction and beam-based alignment.

The calculation runs offline. It uses the recorded actuator settings and BPM readings, so no live machine connection is needed.

## Usage

1. Choose the GUI matching your measurements: corrector excitation, quadrupole-mover excitation, or random excitation.
2. Select the directory containing the recorded snapshots and choose the actuators and BPMs to include.
3. Compute the response matrix and inspect the horizontal, vertical and cross-plane response plots.
4. Optionally select a second measurement directory to calculate the difference between two response matrices, for example at nominal and changed beam energy.
5. Save the result as a `.pkl` file for further analysis.

The corrector and quadrupole-mover GUIs read paired positive/negative `DATA*.pkl` snapshots, such as those recorded by System Identification. The random-excitation GUI also supports `SAMPLE`/iteration (data acquired during correction) data and lets you select nominal or changed-energy measurements.

The standard and quadrupole-mover GUIs can also plot singular values to inspect the measured response. The triangular option suppresses responses from an actuator to upstream BPMs, using the recorded beamline order.

## GUI variants

- `ComputeResponseMatrix_GUI.py`: corrector response matrices.
- `ComputeResponseMatrix_QM_GUI.py`: quadrupole-mover response matrices.
- `ComputeResponseMatrix_rnd_GUI.py`: response matrices from random-excitation measurements.

The saved result contains `Rxx`, `Rxy`, `Ryx` and `Ryy`, together with the corresponding BPM and actuator names.

## Development

Development, issues and pull requests are hosted on [GitHub](https://github.com/flight-simulator-framework/response-matrix). The [CERN GitLab repository](https://gitlab.cern.ch/flight-simulator/response-matrix) receives updates from GitHub through a pull mirror.

## Installation and startup

On a control-room computer, install the applications with the deployment script of your machine: [CLEAR](https://github.com/flight-simulator-framework/machine-interfaces/blob/master/backends/clear/clear_deploy.md), [ATF2](https://github.com/flight-simulator-framework/machine-interfaces/blob/master/backends/atf2/atf2_deploy.md), [ESRF](https://github.com/flight-simulator-framework/machine-interfaces/blob/master/backends/esrf/esrf_deploy.md) or [FACET2](https://github.com/flight-simulator-framework/machine-interfaces/blob/master/backends/facet2/facet2_deploy.md). It creates a shared virtual environment and one launcher per GUI, e.g. `./ComputeResponseMatrix_GUI.sh`.

For a local installation, use Python 3.11 or newer and keep the repositories in one directory. The commands below clone from GitHub; to clone from CERN GitLab instead, replace `https://github.com/flight-simulator-framework/` with `https://gitlab.cern.ch/flight-simulator/`:

```bash
git clone https://github.com/flight-simulator-framework/machine-interfaces.git
git clone https://github.com/flight-simulator-framework/response-matrix.git
python3 -m venv venv
source venv/bin/activate
pip install -e machine-interfaces -e response-matrix
cd response-matrix
python ComputeResponseMatrix_GUI.py
```

Other entry files, using the same environment:

- `ComputeResponseMatrix_QM_GUI.py`
- `ComputeResponseMatrix_rnd_GUI.py`
