# Batch blending energy optimization

**Decision:** Choose a speed and stop time for one 500 L tank that minimizes modeled shaft energy while meeting a batch deadline. This independent study combines Python time-series analysis with mixer power calculations. All sensor signals are synthetic.

## Run your first case
1. Extract the ZIP and open Batch_Blending_Report.pdf for the two-page study.
2. Open https://colab.research.google.com/ and select File → Upload notebook. Upload Batch_Blending.ipynb from the extracted folder. This is the only file you need to upload.
3. Choose Runtime → Run all. Find the two-probe plot, the six-speed comparison, the selected speed and the PASS message. The default result is 150 rpm, 80 s and 2.37 Wh per batch.
4. In the first code cell change deadline_s from 90 to 75. Run all cells again. You should see 180 rpm, 72 s and 3.69 Wh. Then try 20 seconds: every tested option misses that deadline.
5. Restore 90 and rerun. Save your edited notebook using File → Save a copy in Drive. Colab's Files sidebar contains the regenerated output folder.
6. To explain the result, open Interview_and_Resume.md and check your answers against the table.

## Run locally if preferred
Use Python 3.10 or newer. Open a terminal in this folder and run:
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyterlab Batch_Blending.ipynb
```
On Windows use `py -m venv .venv` and activate with `.venv\Scripts\Activate.ps1`. In JupyterLab select Run → Run All Cells.

## Repository contents
| File | Contents |
|---|---|
| Batch_Blending.ipynb | Self-contained signal generator, endpoint detector, energy comparison, plots and checks |
| Batch_Blending_Report.pdf | Results and implications for the default 90 s case |
| output/synthetic_tracer.csv | 10,128 rows: rpm, run, probe, seconds, normalized local signal |
| output/run_endpoints.csv | 24 two-probe blend times in seconds |
| output/speed_comparison.csv | Six speeds, confirmed runs, median and scheduled times, Re, shaft power, energy and deadline status |
| output/deadline_sensitivity.csv | Speed and energy selected at different deadlines; blank decision cells mean infeasible |
| output/tracer_example.png | A near and a far probe settling after the dye dose |
| output/energy_tradeoff.png | Energy per batch versus time, annotated by speed |
| Interview_and_Resume.md | Project entry, interview explanation and practice questions |
| requirements.txt | Local Python dependencies |

The notebook generates the data from a fixed random seed. The far probe has a nominal 26 s decay time at 150 rpm, modified by speed and run variability; the near probe responds faster. The case uses one 0.35 m impeller, an assumed power number of 1.3, density 1,000 kg/m³ and viscosity 0.001 Pa·s. For real application, replace simulated signals with measured normalized data, verify probe placement and measure shaft power. The reported percentage applies to mixer shaft energy during blending only.
