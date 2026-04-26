# Interactive PPR Validation Tool for Production Systems

A Streamlit-based **Product–Process–Resource (PPR) visualizer** for modeling, validating, and exploring production-system structures. The application supports both **imported models** and **models created from scratch**, and it provides multiple viewpoints for analysis, including **PPR**, **Engineering**, and **Sustainability**.

---

## Overview

This repository contains an interactive app for working with PPR models in production systems engineering. It is designed to help users:

- import existing PPR models from **AML** or **XLSX** files,
- validate whether a model follows the expected PPR structure,
- create a new PPR model interactively inside the app,
- explore a predefined sample model,
- and read documentation about the model rules and application workflow.

The app is built with **Streamlit** and uses graph-visualization tooling to render the model as an interactive network.

---

## Main Capabilities

### 1. Import Model
The import workspace lets you upload an AML or Excel file, parse the model into nodes and edges, and validate it against PPR rules. After import, the model can be viewed from different perspectives:

- **PPR View**
- **Engineering View**
- **Sustainability View**

If the model does not satisfy the expected structure, the app reports validation errors and keeps the user in the import/diagnostic flow.

### 2. Build PPR Model
This workspace allows you to construct a PPR model directly in the app. It is session-state driven, so the created model persists during the current session. The page supports viewpoint switching and uses workspace locking to avoid conflicts with an already imported model.

### 3. Explore Sample
This page loads a predefined example model so new users can quickly understand the app behavior, the PPR structure, and the viewpoint-based visualization workflow.

### 4. Help and Docs
The documentation page explains the PPR meta-model, shows the valid structure diagram, and provides access to the full project report PDF.

---

## Repository Structure

The repository is organized around a Streamlit entry point and a page-based application architecture.

### Key files

- `main.py`  
  Application entry point. Sets up the Streamlit page, initializes session state, provides the sidebar navigation, and routes the user to the selected workspace.

- `pages1/import_model.py`  
  Handles file upload, parsing, validation, and visualization of imported AML/XLSX models.

- `pages1/build_ppr.py`  
  Handles interactive creation of a new PPR model from scratch.

- `pages1/explore_sample.py`  
  Loads and displays a predefined sample model.

- `pages1/help_docs.py`  
  Presents the PPR rules, visual reference, and project documentation.

- `pages1/views/`  
  Contains reusable visualization components for the different viewpoints.

- `pages1/Utils1/`  
  Contains helper utilities, including viewpoint handling.

- `pages1/data/sample_data.py`  
  Stores the sample engineering and sustainability node/edge data used in the sample view.

### Supporting files

- `Lego_ppr.aml`  
  Example AML model file.

- `Lego_ppr.xlsx`  
  Example Excel-based model file.

- `valid_ppr_structure.png`  
  Diagram showing the valid PPR meta-model.

- `PyPE2026_Group2FinalDraft.pdf`  
  Full project report and documentation.

- `requirements.txt`  
  Python dependency list.

---

## Application Workflow

The app follows a clear workflow:

### Step 1: Choose a workspace
Use the sidebar to select one of the available workspaces:

- Import Model
- Build PPR Model
- Explore Sample
- Help and Docs

### Step 2: Load or create model data
Depending on the selected workspace, the application will either:

- accept an uploaded AML/XLSX file,
- allow the user to create nodes and links interactively,
- or load a predefined sample model.

### Step 3: Validate structure
For imported models, the app checks whether the node and link structure follows the PPR rules. Validation results are stored in session state and shown to the user if issues are found.

### Step 4: Visualize the model
The model can be rendered in different viewpoints:

- **PPR View** for the overall production-system model,
- **Engineering View** for engineering-oriented structure,
- **Sustainability View** for sustainability-oriented structure.

### Step 5: Reset or continue
A dedicated **Reset Workspace** control clears the working state while preserving navigation context, allowing the user to start over cleanly.

---

## PPR Model Logic

A valid PPR model in this application is based on three core concepts:

- **Product** — the item being created or transformed
- **Process** — the value-adding activity
- **Resource** — the means used to perform the process

The documentation in the app highlights the following valid connection patterns:

- Product → Process
- Process → Product
- Process → Resource

The app also communicates that:

- a product instance can undergo only one process,
- and there must be no direct Product ↔ Resource link.

---

## Technical Highlights

- **Streamlit** powers the web UI.
- **Session state** is used extensively to preserve model data between reruns.
- **Graph visualization** is handled with `yfiles_graphs_for_streamlit`.
- **Network handling** uses `networkx`.
- **Model parsing** supports AML and Excel inputs.
- **Navigation** is implemented with `streamlit_option_menu`.

---

## Installation

### Prerequisites
- Python 3.11+ recommended
- pip

### Install dependencies
```bash
pip install -r requirements.txt
```

---

## Running the App

From the repository root, run:

```bash
streamlit run main.py
```

Then open the local Streamlit URL shown in the terminal.

---

## Expected Inputs

### AML file
The import flow supports `.aml` files and parses the model structure from the CAEX/AML representation.

### Excel file
The import flow also supports `.xlsx` files for model ingestion.

---

## Typical Use Cases

- validating whether an imported production model conforms to the PPR meta-model,
- comparing engineering and sustainability perspectives of the same structure,
- building a PPR model interactively during coursework or prototyping,
- demonstrating production-system relationships in a visual and auditable format.

---

## Notes on Session Behavior

The application is designed around workspace persistence:

- imported and built models are stored in `st.session_state`,
- viewpoint-specific data is preserved separately,
- and workspace reset is required before switching between certain active model contexts.

This avoids accidental mixing of imported and built datasets.

---

## License

This repository is distributed under the **MIT License**.

---

## Acknowledgment

This project is a fork of `Snotboggie109/PyPSE2026_Group2` and extends it into an interactive PPR validation and visualization tool.
