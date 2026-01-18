# Multi-Modal Knowledge Graph Generation & Pruning Pipeline

[](https://ai.google.dev/)
[](https://www.python.org/)

This project implements an end-to-end pipeline that transforms raw images into structured Knowledge Graphs (KG), optimizes them using a hybrid pruning strategy, and reconstructs vector illustrations (SVG) from the refined data.

## 🚀 Features

  * **Step 1: Image to Text**: Uses Gemini Vision to generate detailed semantic summaries of input images.
  * **Step 2: KG Extraction**: Converts unstructured text into a structured Knowledge Graph (Entities, Attributes, Relationships).
  * **Step 3: Hybrid Pruning**: Optimizes the graph using a 3-stage strategy:
      * *Topology Analysis*: Removes isolated nodes using NetworkX.
      * *Semantic Fusion*: Merges redundant attributes using Vector Embeddings (Cosine Similarity).
      * *LLM Refinement*: Performs final logical cleanup.
  * **Step 4: Comparative Analysis**: Generates statistical charts and Excel reports comparing the graph before and after pruning.
  * **Step 5: Scene Reconstruction**: Generates a flat-style SVG cartoon illustration based on the optimized Knowledge Graph.

-----

## 📂 Project Structure

Ensure your directory is organized as follows:

```text
.
├── api.py               # Step 1: Image summarization module
├── generateKG.py        # Step 2: Initial KG extraction module
├── pruningKG.py         # Step 3: Hybrid pruning module (Topology + Embedding + LLM)
├── compareKG.py         # Step 4: Data analysis and visualization module
├── KG2Image.py          # Step 5: SVG generation module
├── workflow.py     # MODE 1: Headless automated pipeline (Saves files silently)
├── run_local.py         # MODE 2: Local visualization (Pop-up windows)
├── gui_main.py          # MODE 3: Streamlit Web Interface
├── test.png             # Default input image (Required)
└── README.md            # This file
```

-----

## 🛠️ Prerequisites & Installation

1.  **Python Version**: Python 3.9 or higher is recommended.
2.  **Install Dependencies**:

<!-- end list -->

```bash
pip install google-generativeai networkx matplotlib pandas numpy pillow openpyxl streamlit
```

3.  **API Key Configuration**:

      * You need a valid Google Gemini API Key.
      * The scripts currently have a placeholder key. It is recommended to set this via environment variables or modify the `GOOGLE_API_KEY` variable in the runner scripts (`main_pipeline.py`, etc.).

4.  **Network Proxy (Optional)**:

      * If you are in a region where Google services are restricted, update the `PROXY_URL` in the scripts (default is `http://127.0.0.1:7890`).

-----

## 📖 Usage

You can run the pipeline in three different modes depending on your needs.

### Mode 1: Automated Pipeline (Headless)

Best for batch processing. It runs silently and saves all outputs to a timestamped folder.

```bash
python workflow.py
```

  * **Behavior**: No pop-up windows.
  * **Output**: Creates a folder named `Output_YYYYMMDD_HHMMSS` containing all logs, JSONs, PNGs, and SVGs.

### Mode 2: Local Visualization (Interactive)

Best for debugging or checking results step-by-step.

```bash
python run_local.py
```

  * **Behavior**: Matplotlib windows will pop up for every visualization step.
  * **Action**: You must **close the window** manually to proceed to the next step.
  * **Output**: Also saves files to the timestamped folder.

### Mode 3: Web GUI (Streamlit)

Best for demonstrations and user-friendly interaction.

```bash
streamlit run gui_main.py
```

  * **Behavior**: Opens a web page in your browser.
  * **Features**:
      * Sidebar for API Key/Proxy configuration.
      * Drag-and-drop image upload.
      * Expandable JSON viewers.
      * Side-by-side graph visualization.
      * Download button for the final SVG.

-----

## 📊 Output Artifacts

After running the pipeline, you will find a folder (e.g., `Output_20231209_120000`) containing:

| File Name | Format | Description |
| :--- | :--- | :--- |
| `1_summary.txt` | TXT | The text summary generated from the input image. |
| `2_KG_I.json` | JSON | The initial Knowledge Graph data. |
| `2_KG_I.png` | PNG | Visualization of the initial graph. |
| `3_KG_P.json` | JSON | The pruned (optimized) Knowledge Graph data. |
| `3_KG_P.png` | PNG | Visualization of the pruned graph. |
| `4_analysis_chart.png` | PNG | Bar chart comparing nodes/edges/attributes. |
| `4_analysis_data.xlsx` | Excel | Detailed statistics and list of removed entities. |
| `5_scene.svg` | SVG | AI-generated vector illustration based on the pruned KG. |

-----

## 🧩 Module Details

### `pruningKG.py` (Optimization Logic)

The pruning process is not just a simple deletion. It employs a **Hybrid Pruning Strategy**:

1.  **Topology Pruning**: Removes isolated nodes (Degree=0) and non-core entity types based on a blacklist (e.g., "Background").
2.  **Semantic Fusion**: Uses **Gemini Embeddings** to calculate Cosine Similarity between attributes. Attributes with similarity \> 0.9 are merged to reduce redundancy.
3.  **LLM Refinement**: Sends the cleaned data to Gemini Flash for final logical consistency checks (e.g., merging duplicate entities).

### `KG2Image.py` (SVG Generation)

Instead of hardcoding shapes, this module uses a "Chain of Thought" prompt to instruct the LLM to act as a **Flat Style Illustrator**. It interprets the JSON semantics (e.g., "Attribute: Wheeled" -\> "Draw wheels") to generate generic SVG code.

-----

## ⚠️ Troubleshooting

1.  **`ConnectionTimeout` / `ProxyError`**:

      * Check your VPN/Proxy settings.
      * Update `os.environ["HTTP_PROXY"]` in the Python scripts to match your local proxy port.

2.  **`403 Forbidden` / `API Key Invalid`**:

      * Ensure your API Key is active and has access to `gemini-1.5-flash` and `text-embedding-004`.

3.  **Matplotlib Chinese Characters Display as Boxes (□□)**:

      * The scripts try to use standard fonts (`SimHei`, `Arial Unicode MS`). If you still see boxes, you may need to install a CJK font on your system or modify `plt.rcParams['font.sans-serif']`.

-----

## 📄 License

This project is provided for educational and research purposes.