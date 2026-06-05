# Quantum Spectroscopy of the Mertens Weight Function on IBM Quantum Hardware

**Earl Decker** — Independent Researcher  
earldecker@gmail.com

Code and data repository for:

> *Quantum Spectroscopy of the Mertens Weight Function on IBM Quantum Hardware* (2026)  
> Published on Academia.edu

---

## Overview

This repository contains all Python scripts, raw IBM job results, and figures for the paper. The work demonstrates that the Mertens weight function f(n) = ln(n)/n is physically measurable on IBM Quantum superconducting hardware using a Bell-pair XX correlator spectrometer.

**Key results:**
- All 6 prime spectral isolation conditions resolved with r > 0.991 (Experiment 6)
- Precision floor reaching Δf = 0.00157 (Experiment 7, N = 4096 shots, 1250 α-steps)
- Complete Mertens spectrum f(n) for n = 2–20 measured with <1.5% error (Experiment 8)
- f(4) = f(2) degeneracy confirmed on hardware

**Hardware:** IBM ibm_marrakesh (156-qubit Eagle-generation superconducting processor)  
**Access:** IBM Quantum Platform (https://quantum.ibm.com)

---

## Repository Structure

### Experiment Scripts

| Script | Experiment | Description |
|--------|-----------|-------------|
| `experiment6_spectral_isolation.py` | 6 | Bell-pair spectrometer: prime spectral isolation. Resolves Δf between primes and neighbors on ibm_marrakesh |
| `experiment7_precision_floor.py` | 7 | Precision floor measurement. α-sweep from N=100 to N=1250 steps to characterize resolution limit |
| `experiment8_full_spectrum.py` | 8 | Complete Mertens spectrum f(n) for n=2–20. 19 conditions, single α-sweep per condition |

### Data Retrieval Scripts

| Script | Description |
|--------|-------------|
| `retrieve_experiment6.py` | Retrieve and parse Experiment 6 IBM job results |
| `retrieve_experiment7.py` | Retrieve and parse Experiment 7 IBM job results |
| `retrieve_experiment8.py` | Retrieve and parse Experiment 8 IBM job results |

### Raw IBM Job Results

| File | Experiment | Job ID | Description |
|------|-----------|--------|-------------|
| `job-d8fkb63alsvc7391spug-result.json` | 6 | d8fkb63a | Prime spectral isolation (raw counts) |
| `job-d8fkb63alsvc7391spug-info.json` | 6 | d8fkb63a | Prime spectral isolation (job metadata) |
| `job-d8g2259vjngc73aqkp00-result.json` | 7 | d8g2259v | Precision floor (raw counts) |
| `job-d8g2259vjngc73aqkp00-info.json` | 7 | d8g2259v | Precision floor (job metadata) |
| `exp7_results_d8g2259vjngc.json` | 7 | d8g2259v | Precision floor results (processed) |
| `exp8_results_d8g6ktro3njc.json` | 8 | d8g6ktro | Full spectrum results (raw counts) |
| `exp8_spectrum_d8g6ktro3njc.json` | 8 | d8g6ktro | Full spectrum (processed frequencies) |

### Figures

| File | Description |
|------|-------------|
| `fig1_circuit.png` | Bell-pair XX correlator circuit diagram |
| `fig2_oscillations.png` | Interference fringe fits for Experiment 6 |
| `fig3_precision.png` | Precision floor vs. α-sweep length (Experiment 7) |
| `fig4_full_spectrum.png` | Complete Mertens spectrum n=2–20 (Experiment 8) |

---

## Installation

```bash
pip install numpy scipy matplotlib qiskit qiskit-ibm-runtime
```

Python 3.10+ recommended.

**Note:** Running the experiment scripts requires an IBM Quantum account and valid API credentials. Set your token via:

```python
from qiskit_ibm_runtime import QiskitRuntimeService
QiskitRuntimeService.save_account(channel="ibm_quantum", token="YOUR_TOKEN")
```

The raw result files in this repository allow full reproduction of all figures and analysis without IBM hardware access.

---

## Reproducing Key Results

### From raw data (no IBM account needed)

All figures in the paper can be reproduced directly from the JSON result files:

```bash
python retrieve_experiment6.py   # Generates Experiment 6 spectral isolation plots
python retrieve_experiment7.py   # Generates Experiment 7 precision floor plot
python retrieve_experiment8.py   # Generates Experiment 8 full spectrum plot
```

### Running fresh experiments on IBM hardware

```bash
python experiment6_spectral_isolation.py   # ~5 min on ibm_marrakesh
python experiment7_precision_floor.py      # ~10 min on ibm_marrakesh
python experiment8_full_spectrum.py        # ~8 min on ibm_marrakesh
```

---

## IBM Quantum Hardware

All experiments were performed on **ibm_marrakesh**, a 156-qubit Eagle-generation superconducting quantum processor, accessed via the IBM Quantum Platform. Each circuit uses 2 qubits and 4096 shots. The Bell-pair spectrometer circuit has depth 6 (H, CNOT, X, RZ×2, H, measure).

Job IDs are embedded in the result filenames and can be retrieved from IBM Quantum Platform job history.

---

## Key Results Summary

### Experiment 6: Prime Spectral Isolation

| Pair | Δf theory | Δf fitted | Error | r (fit) |
|------|-----------|-----------|-------|---------|
| (7,8) | 0.01806 | 0.01823 | +0.96% | 0.9943 |
| (7,6) | 0.02064 | 0.02077 | +0.63% | 0.9921 |
| (5,6) | 0.03385 | 0.03398 | +0.38% | 0.9964 |
| (5,4) | 0.01963 | 0.01975 | +0.61% | 0.9958 |
| (3,4) | 0.08822 | 0.08889 | +0.76% | 0.9981 |
| (11,12)| 0.03870 | 0.03897 | +0.70% | 0.9969 |

### Experiment 8: Complete Spectrum (selected)

| n | f(n) theory | f(n) measured | Error |
|---|-------------|---------------|-------|
| 2 | 0.346574 | 0.342529 | −1.17% |
| 3 | 0.366204 | 0.361646 | −1.24% |
| 7 | 0.277987 | 0.274293 | −1.33% |
| 11| 0.217990 | 0.215569 | −1.11% |
| 20| 0.149787 | 0.147928 | −1.24% |

---

## Citation

```
Decker, E. (2026). Quantum Spectroscopy of the Mertens Weight Function
on IBM Quantum Hardware. Independent Researcher.
Academia.edu: https://www.academia.edu/[your-paper-id]
Code DOI: 10.5281/zenodo.20562836
```

---

## License

MIT License — see `LICENSE` for details.
