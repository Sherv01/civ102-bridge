# Section Properties and Stress Analysis of a Composite Beam

This MATLAB code calculates the section properties (area, centroid, moment of inertia) and performs stress analysis (bending stress, shear stress, buckling) for a composite beam made of rectangular pieces. This was part of the Bridge Project for CIV102 (Structures and Materials) at the University of Toronto.

## Description

The code takes a matrix `pieces` as input, where each row represents a rectangular piece of the beam. The columns of the `pieces` matrix define the dimensions and position of each piece:

*   **Column 1:** Width of the piece.
*   **Column 2:** Height of the piece.
*   **Column 3:** Distance from the bottom of the cross-section to the bottom of the piece.

The code then calculates the following:

*   **Total Area:** The total cross-sectional area of the composite beam.
*   **Centroid (ybar):** The vertical position of the centroid of the composite beam.
*   **Moment of Inertia (I):** The moment of inertia of the composite beam about its centroidal axis.
*   **Q (First Moment of Area):** Calculates Q at the centroidal axis (`Qcent`) and at the interface between each piece (`Qglue`). These values are used for shear stress calculations.
*   **Bending Stresses (SigmaComp, SigmaTens):** Compressive and tensile bending stresses.
*   **Shear Stresses (TauCent, TauGlue):** Shear stresses at the centroid and glue lines.
*   **Buckling Stresses (SigmaBuck):** Buckling stresses based on different buckling coefficients (k).
*   **Factors of Safety (FOS):** Factors of safety for compression, tension, shear (centroid and glue), and buckling.

## Input

The primary input is the `pieces` matrix. Several example `pieces` configurations are provided as commented-out code, demonstrating different beam geometries (e.g., I-beam, HSS with various internal members). The active `pieces` matrix defines the beam to be analyzed.

The user is prompted to select a load case (1 or 2), which determines the values of shear force (V) and bending moment (M).

## Usage

1.  **Modify the `pieces` matrix:** Uncomment the desired beam configuration or create a new one. Ensure the dimensions are consistent (e.g., inches or millimeters).
2.  **Run the MATLAB script:** Execute the `.m` file in MATLAB.
3.  **Enter the load case:** Respond to the prompt by entering `1` or `2`.
4.  **View the results:** The calculated values (area, centroid, moment of inertia, stresses, factors of safety) will be displayed in the MATLAB command window.

## Functions

*   `calculate_Q(pieces, depth)`: This function calculates the first moment of area (Q) for a given depth. It handles cases where the depth of interest is above or below the centroidal axis and correctly accounts for partial inclusion of pieces.

## Output

The code outputs the following variables:

*   `total_area`: Total cross-sectional area.
*   `ybar`: Vertical position of the centroid.
*   `I`: Moment of inertia.
*   `Qcent`: First moment of area at the centroid.
*   `Qglue`: First moment of area at the glue lines (interfaces between pieces).
*   `SigmaComp`: Compressive bending stress.
*   `SigmaTens`: Tensile bending stress.
*   `TauCent`: Shear stress at the centroid.
*   `TauGlue`: Shear stress at the glue lines.
*   `SigmaBuck4`, `SigmaBuck0425`, `SigmaBuck6`, `SigmaBuck5`: Buckling stresses for different k values.
*   `FOS_comp`, `FOS_tens`, `FOS_shearcent`, `FOS_shearglue`, `FOS_buck4`, `FOS_buck0425`, `FOS_buck6`, `FOS_buck5`: Factors of safety.

## Notes

*   The code assumes that the beam is made of rectangular pieces.
*   The distance from the bottom is measured to the bottom of each piece, not the centroid.
*   The `Qglue` matrix represents the shear stress between one piece and the piece that follows it in the `pieces` matrix. If two pieces are not glued together, the corresponding Q value should be ignored.
*   The material properties (e.g., modulus of elasticity) are implicitly included in the buckling calculations (4000 value). You might need to adjust them based on your material.
*   The factors of safety used (6, 30, 4, 2) are example values and should be adjusted based on the specific design requirements and applicable codes.
*   The units of the output depend on the units used in the input `pieces` matrix. Ensure consistency.
