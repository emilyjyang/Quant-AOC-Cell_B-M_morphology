# Quant-AOC-Cell_B-M_morphology
Scripts used in Actin Cable Organizing Center paper to measure the bud to mother ratio and morphology of the mother or bud cells.

# AOC-Cell_B-M_morphology-v1.ijm

## Overview
This FIJI macro quantifies **mother and bud morphology** in budding yeast using Cellpose-generated segmentation masks.  
It calculates the **lengths** of mother and bud cells and optionally measures additional shape parameters including **Feret diameter**, **circularity**, **aspect ratio**, and **roundness**.  

This macro complements the *actin cable orientation* analysis workflow by reusing the same segmentation masks and ROI information to perform detailed morphological measurements.

---

## Prerequisites

### Required Software
- [FIJI (ImageJ)](https://fiji.sc/)
- [Bio-Formats plugin](https://www.openmicroscopy.org/bio-formats/)
- [Cellpose](https://www.cellpose.org/) (for mask generation)

### Recommended
- Super-resolution images (optional)  
- Deconvolved widefield images with background removed before MIP generation

### Supported File Types
`.tif`, `.czi`, `.nd2`, `.ome.tiff`  
Other formats supported by Bio-Formats can be added by editing the macro header.

---

## Step 1 – Prepare Input and Output Folders

1. Place your **Cellpose mask images** (from the `x-Mask` folder generated previously) into an **input folder**.  
2. Define an **output folder** to store all morphology and ratio results.  
3. The file naming and folder structure should be consistent with those used in the *actin orientation quantification* workflow.

---

## Step 2 – Load and Select Image Channels

1. Launch the macro:  
   **`AOC-Cell_B-M_morphology-v1.ijm`**  
2. When prompted:
   - Select the **input folder** (containing Cellpose mask images).  
   - Select the **output folder** for saving results.  
   - Choose a **channel** (e.g., actin or mitochondria) to guide cell selection.  
3. File type support and crop size definitions are identical to those in the *actin orientation* macro.

---

## Step 3 – Image Loading and ROI Selection

1. For each image, the macro will:
   - Open the **original input image** and its corresponding **Cellpose mask**.  
   - Automatically adjust contrast for easier visualization.  
2. You may:
   - **Select cells manually** in the displayed image, **or**  
   - **Load existing ROIs** (e.g., cell number ROIs) using the FIJI ROI Manager from a previous quantification step.

3. Based on the ROI coordinates, the macro crops individual cells and prompts the user to select the **mother** and **bud** regions:
   - Use the **wand tool** to select the corresponding areas from the Cellpose mask, **or**
   - Use the **freehand selection tool** if the Cellpose mask is inaccurate.

---

## Step 4 – Morphology Quantification

### Basic Mode
If you skip the morphology quantification option, the macro will only calculate:
- **Mother length**
- **Bud length**
- **Bud-to-mother length ratio**

### Full Morphology Mode
When morphology quantification is enabled, the macro will also measure:
- **Feret diameter**  
- **Circularity**  
- **Aspect ratio**  
- **Roundness**

These parameters are calculated separately for mother and bud cells.

---

## Step 5 – Output Files and Folder Structure

After processing, the macro automatically generates the following output folders:

| Folder | Description |
|---------|-------------|
| `0-M_Bratio` | Contains measurements of mother length, bud length, and bud/mother length ratio |
| `3-morph-M` | Morphology quantification results for mother cells |
| `4-morph-B` | Morphology quantification results for bud cells |

Additional intermediate files are saved for reproducibility:
- **Cell number ROIs**
- **Mother and bud ROIs**

---

## Example Workflow

Below are representative images showing each stage of the morphology analysis.

### 1. Example Input Image
Raw yeast fluorescence image before Cellpose segmentation.  
![Example Input Image](images/example_morph_input.png)

---

### 2. Example Cellpose Mask
Cellpose-generated mask showing separated mother and bud regions.  
![Example Cellpose Mask](images/example_morph_mask.png)

---

### 3. Example ROI Selection
User-defined ROIs for mother (green) and bud (magenta).  
![Example ROI Selection](images/example_morph_roi.png)

---

### 4. Example Output Measurements
Example CSV or table output showing measured parameters for each cell.  
![Example Output Table](images/example_morph_output.png)

---

## Notes
- Ensure mother and bud are **clearly separated** in the Cellpose mask or by manual ROI drawing.  
- The **crop size** and file-handling settings are identical to those in `Quant-Coherency-dominant_direction.ijm`.  
- This macro can reuse **cell number ROIs** from previous analyses for consistent cell indexing.  
- All measurements are automatically saved and organized by cell identity and cell type (mother vs bud).

---

## Citation
If you use this macro in your research, please cite:  
> Emily J. Yang, *AOC-Cell_B-M_morphology-v1.ijm: FIJI Macro for Yeast Mother–Bud Morphology Quantification*, [2025].

---

## License
This project is released under the [MIT License](LICENSE).

---

## Contact
For questions or feedback, please contact:  
**[Emily J. Yang]**  
Email: [emily.jiening.yang@gmail.com]
