# SPARK AEM Performance Grading and Attention Visualization Tool

An alkaline anion exchange membrane (AEM) structure parsing and performance grading tool based on the **SPARK** model (Graph Attention Network dual-channel encoding + FiLM fusion + knowledge embedding), capable of simultaneously outputting prediction results, visualizing attention weights, and generating comprehensive reports.

## 1. Overview
- Dual-task prediction: Conductivity grading (`condc`) and stability grading (`stabt`).
- Attention visualization: Outputs node attention heatmaps (`.tif`) for input molecules (A/B/C).
- Comprehensive reporting: Automatically generates `summary.txt` summarizing prediction logs and output inventory.

## 2. Installation (Distribution Package)
- The installation package includes a built-in runtime environment, model weights, and resource files. No separate dependency installation required.
- Installation steps:
  1. Double-click the installer and follow the wizard to complete installation (select installation directory; path selection unavailable for subsequent installations).
  2. Launch the program via Start Menu or desktop shortcut after installation.
  3. If security software intercepts on first launch, select "Run anyway" or add the installation directory to the whitelist.

## 3. Operation Instructions
1. Launch the installed executable program.
2. Fill in or confirm input parameters on the left panel of the main interface (defaults will be used if left blank), then click **Start** to begin prediction.
3. The program automatically completes `condc`/`stabt` prediction, attention visualization, and generates a comprehensive report.
4. Output directory is located at `output/timestamp/` alongside the program, containing prediction results CSV, visualization images, and `summary.txt`.

## 4. Input Parameters

| Field | Description | Default / Requirement |
| :--- | :--- | :--- |
| `smilesA` | SMILES of ion-containing (hydrophilic) unit in AEM backbone | Molecular graph to SMILES conversion available via RDKit |
| `smilesB` | SMILES of non-ion-containing (hydrophobic) unit in AEM backbone | `smilesA` and `smilesB` must be strictly filled according to ion presence |
| `smilesC` | Additional structure | For AEM structural units >2, input excess structures here |
| `W1` | Weight of ion-containing unit | Default: `0.5`, can be enumerated or reverse-calculated via IEC |
| `W2` | Weight of non-ion-containing unit | Default: `0.5` |
| `W3` | Weight of additional structure | Default: `0.0` |
| `Temperature` | Test temperature for conductivity task | Default: `80` |
| `TemperatureR` | Test temperature for stability task | Default: `80` |
| `Time` | Test duration for stability task | Default: `1000` |
| `Concentration` | Test concentration for stability task | Default: `1` |

## 5. Workflow
1. Fill in/confirm input fields (defaults applied if blank).
2. After clicking **Start**:
   - Runs `condc` prediction first, generating `output/.../condc/prediction/con_prediction_results.csv`
   - Runs `stabt` prediction, generating `output/.../stabt/prediction/sta_prediction_results.csv`
   - Performs `condc`/`stabt` visualization separately, producing multiple `.tif` files
   - Generates comprehensive report `output/.../summary.txt`
3. Right text panel displays runtime logs and prediction outputs; bottom scrollable area showcases attention maps.

## 6. Output Directory Structure (Example)
```
output/2026_01_01_120000/
 ├─ condc/
 │   ├─ prediction/con_prediction_results.csv
 │   └─ visualization/*.tif
 ├─ stabt/
 │   ├─ prediction/sta_prediction_results.csv
 │   └─ visualization/*.tif
 └─ summary.txt
```

## 7. Important Notes
- `W1` and `W2` are not recommended for individual input as default settings may cause ratio errors.
- Weights and resources are built-in; **DO NOT** modify file structure in installation directory.
- For custom output paths, manually move the `output/timestamp/` directory after program execution.
- If antivirus or security software intercepts, add installation directory to trust/whitelist.
- If program freezes or becomes unresponsive, restart and retry; contact support for persistent issues.
- For program crashes, send data to our email for feedback.

## 8. Troubleshooting
- **Empty output or crashes**: Verify weight files exist and paths are correct; confirm dependency version compatibility.
- **Images not displaying**: Confirm `.tif` files are generated in output directory; enlarge window or scroll if too small.
- **Missing resources after packaging**: Ensure `resources/`, `rc_resources.py`, `weight/` are included in package.

---

**Contact:** huyedut@163.com
