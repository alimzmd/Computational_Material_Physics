======================================================
 Data Repository for: Operando Scanning SAXS/WAXS Cell Design for Multiscale Analysis of All-Solid-State Battery Systems
======================================================

This repository contains the underlying data used to generate the figures in the publication "Operando Scanning SAXS/WAXS Cell Design for Multiscale Analysis of All-Solid-State Battery Systems". The data is provided to ensure reproducibility and allow for further analysis by the community.

The data is primarily stored in two formats:
* `.csv` (Comma-Separated Values): For 2D data like line plots. These are human-readable and can be opened by almost any data analysis software.
* `.npz` (NumPy Archive): For multi-dimensional data like heatmaps or multiple related arrays. This is an efficient binary format.

--------------------------------------------------------------------------------

--- Data Access Guide ---

Below is a figure-by-figure guide describing each data file and how to access its contents using Python with the Pandas and NumPy libraries.

-- Requirements --
You'll need to have Python installed with the following libraries:
  pip install numpy pandas

--------------------------------------------------------------------------------

--- Figure 1 Data ---

Figure 1 consists of a multi-panel plot (electrochemistry, SAXS, WAXS) and a separate heatmap of integrated intensity.

* Files:
  `figure1_data_electrochemistry.csv`
  `figure1_data_scattering_data.npz`
  `figure1_heatmap_data.npz`

* Description:
  The `.csv` file contains the electrochemistry data (Potential vs. Capacity).
  The `..._scattering_data.npz` file contains the waterfall plot data for the SAXS and WAXS measurements, including the q-vectors and the 2D intensity matrices (time x q-points).
  The `..._heatmap_data.npz` file contains the 17x3 data array for the 'First Discharge' heatmap.

* How to Access:
  import pandas as pd
  import numpy as np

  # --- Access the multi-panel data ---
  # Load the electrochemistry CSV
  echem_df_fig1 = pd.read_csv('figure1_data_electrochemistry.csv')
  print("Figure 1 Electrochemistry:\n", echem_df_fig1.head())

  # Load the scattering data NPZ archive
  scattering_data_fig1 = np.load('figure1_data_scattering_data.npz')
  # You can see all arrays stored in the file
  print("\nArrays in Figure 1 scattering file:", list(scattering_data_fig1.keys()))
  saxs_intensity_fig1 = scattering_data_fig1['saxs_intensity_cm']
  print("Shape of SAXS intensity matrix:", saxs_intensity_fig1.shape)


  # --- Access the heatmap data ---
  heatmap_data_fig1 = np.load('figure1_heatmap_data.npz')
  first_discharge_map = heatmap_data_fig1['First_Discharge']
  print("\nShape of Figure 1 heatmap:", first_discharge_map.shape)

--------------------------------------------------------------------------------

--- Figure 2 Data ---

Figure 2 is a comprehensive plot with electrochemistry, three WAXS heatmaps (anode, separator, cathode), an integrated intensity line plot, and a separate figure with four state-of-charge heatmaps.

* Files:
  `figure2_data_electrochemistry.csv`
  `figure2_data_li2s_intensity.csv`
  `figure2_data_waxs_heatmaps.npz`
  `figure2b_data_heatmap_data.npz`

* Description:
  The two `.csv` files contain the electrochemistry and the integrated Li₂S intensity line plots, respectively.
  The `...waxs_heatmaps.npz` file contains the data for the three WAXS heatmaps from Figure 2a, including intensity matrices and their corresponding q and time axes.
  The `...figure2b...` file contains the four 7x3 heatmap arrays for the different states of charge. Note that this file contains the *absolute* intensity values; the plotted data was normalized by the 'Start' state.

* How to Access:
  # --- Access data from Figure 2a ---
  li2s_df_fig2 = pd.read_csv('figure2_data_li2s_intensity.csv')
  print("Figure 2 Li2S Intensity:\n", li2s_df_fig2.head())

  waxs_maps_fig2a = np.load('figure2_data_waxs_heatmaps.npz')
  print("\nArrays in Figure 2a WAXS file:", list(waxs_maps_fig2a.keys()))
  anode_intensity = waxs_maps_fig2a['anode_intensity']
  waxs_time_axis = waxs_maps_fig2a['waxs_time_hours']
  print("Shape of anode intensity matrix:", anode_intensity.shape)


  # --- Access data from Figure 2b ---
  heatmap_data_fig2b = np.load('figure2b_data_heatmap_data.npz')
  print("\nArrays in Figure 2b heatmap file:", list(heatmap_data_fig2b.keys()))
  start_map = heatmap_data_fig2b['Start']
  # To reproduce the plotted data, you can normalize by the start state:
  # relative_discharge_map = heatmap_data_fig2b['First_Discharge'] / start_map
  print("Shape of 'Start' state heatmap:", start_map.shape)

--------------------------------------------------------------------------------

--- Figure 3 Data ---

Figure 3 contains electrochemistry, crystallite size with error, and time-resolved SAXS data.

* Files:
  `figure3_data_electrochemistry.csv`
  `figure3_data_crystallite_size.csv`
  `figure3_data_saxs_data.npz`

* Description:
  The two `.csv` files contain the data for the electrochemistry and crystallite size line plots.
  The `.npz` file contains the time-resolved SAXS data (q-axis, time-axis, and the 2D intensity matrix) as well as the reference spectra for the carbon and cathode backgrounds.

* How to Access:
  cryst_df_fig3 = pd.read_csv('figure3_data_crystallite_size.csv')
  print("Figure 3 Crystallite Size:\n", cryst_df_fig3.head())

  saxs_data_fig3 = np.load('figure3_data_saxs_data.npz')
  print("\nArrays in Figure 3 SAXS file:", list(saxs_data_fig3.keys()))
  time_resolved_saxs = saxs_data_fig3['time_resolved_intensity']
  carbon_background = saxs_data_fig3['reference_carbon_background']
  print("Shape of time-resolved SAXS matrix:", time_resolved_saxs.shape)

--------------------------------------------------------------------------------

--- Figure 4 Data ---

Figure 4 combines electrochemistry with large SAXS and WAXS heatmaps (4a) and a set of smaller SAXS/WAXS heatmaps showing integrated intensity (4b).

* Files:
  `figure4a_data_electrochemistry.csv`
  `figure4a_data_scattering_maps.npz`
  `figure4b_saxs_data_heatmap_data.npz`
  `figure4b_waxs_data_heatmap_data.npz`

* Description:
  The `.csv` file contains the electrochemistry for Figure 4a.
  The `...scattering_maps.npz` file contains the large SAXS and WAXS heatmaps for Figure 4a.
  The two `...figure4b...` files contain the 2D arrays for the smaller integrated intensity heatmaps (SAXS and WAXS, respectively).

* How to Access:
  # --- Access data from Figure 4a ---
  scattering_maps_fig4a = np.load('figure4a_data_scattering_maps.npz')
  print("Arrays in Figure 4a scattering file:", list(scattering_maps_fig4a.keys()))
  waxs_map_fig4a = scattering_maps_fig4a['waxs_relative_intensity']
  print("Shape of Figure 4a WAXS map:", waxs_map_fig4a.shape)


  # --- Access data from Figure 4b ---
  saxs_heatmaps_fig4b = np.load('figure4b_saxs_data_heatmap_data.npz')
  waxs_heatmaps_fig4b = np.load('figure4b_waxs_data_heatmap_data.npz')
  print("\nArrays in Figure 4b SAXS file:", list(saxs_heatmaps_fig4b.keys()))
  saxs_sodc_0_map = saxs_heatmaps_fig4b['0_pct_SODC']
  print("Shape of Figure 4b SAXS 0% SODC map:", saxs_sodc_0_map.shape)

--------------------------------------------------------------------------------
--- Supplementary Figures ---
--------------------------------------------------------------------------------

--- Figure S1 Data ---

*Description: This figure contains data for an additional cell, with panels analogous to those in the main figures.*

-- Figure S1a (similar to Fig. 2a) --

* Files:
  `figureS1a_electrochemistry.csv`
  `figureS1a_li2s_intensity.csv`
  `figureS1a_waxs_heatmaps.npz`

* How to Access:
  # Access data for Figure S1a
  waxs_maps_figS1a = np.load('figureS1a_waxs_heatmaps.npz')
  print("\nArrays in Figure S1a WAXS file:", list(waxs_maps_figS1a.keys()))


-- Figure S1b (similar to Fig. 2b) --

* Files:
  `figureS1b_heatmap_data.npz`

* How to Access:
  # Access data for Figure S1b
  heatmap_data_figS1b = np.load('figureS1b_heatmap_data.npz')
  print("\nArrays in Figure S1b heatmap file:", list(heatmap_data_figS1b.keys()))


-- Figure S1c (similar to Fig. 3) --

* Files:
  `figureS1c_electrochemistry.csv`
  `figureS1c_crystallite_size.csv`
  `figureS1c_saxs_data.npz`

* How to Access:
  # Access data for Figure S1c
  cryst_df_figS1c = pd.read_csv('figureS1c_crystallite_size.csv')
  print("\nFigure S1c Crystallite Size:\n", cryst_df_figS1c.head())

  saxs_data_figS1c = np.load('figureS1c_saxs_data.npz')
  print("\nArrays in Figure S1c SAXS file:", list(saxs_data_figS1c.keys()))

--------------------------------------------------------------------------------

If you have any questions, please contact christian.prehal@plus.ac.at