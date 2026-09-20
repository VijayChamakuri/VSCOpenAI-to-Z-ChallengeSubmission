# OpenAI to Z Challenge: LiDAR Anomaly Screening in the Colombian Amazon

Kaggle competition submission. A two-stage screening pipeline that flags terrain anomalies in a LiDAR-derived digital elevation model and then asks a vision model whether each flagged pattern looks natural or built. This is a competition entry and a methods demonstration, not validated archaeological research.

**Question.** Can terrain anomalies in a bare-earth DEM be screened quickly enough to tell a survey team which locations are not worth visiting?

**Data.** `colombia_aoi_dem.tif`, the competition's pre-processed digital elevation model for an area of interest in the Colombian Amazon. No field survey, excavation or ground truth is included.

**Method.**

1. Scan the DEM for slope and local elevation deviations and flag candidate points ([`01_Recon_and_EDA.ipynb`](01_Recon_and_EDA.ipynb)).
2. Plot the candidates on an interactive wide-area map ([`fullscreen_anomaly_map.html`](fullscreen_anomaly_map.html), [`wide_area_map.png`](wide_area_map.png)).
3. Select three candidates by visual inspection ([site 1](site_1.png), [site 2](site_2_linear_feature.png), [site 3](site_3_river_pattern.png)).
4. Send each candidate image to an OpenAI vision model with a fixed prompt asking it to separate riverine and geological explanations from signs of construction.

**Result.** The model read all three candidates as natural riverine and geological formations, not anthropogenic features: the patterns follow meander paths and lack the geometric regularity of built structures. The write-up is in [`final_report.md`](final_report.md). The honest headline is a negative result. No site was identified.

**Run it.** Open `01_Recon_and_EDA.ipynb` with the DEM file in the same directory. The vision-model step needs your own OpenAI API key; the notebook's recorded outputs show what was returned during the competition run.

**Limitations.** The classification rests on one vision-model judgment per site with no labeled validation set, no inter-rater comparison and no accuracy measurement, so its error rate is unknown. Candidate selection from the anomaly map was manual and therefore subjective. Anomaly detection uses slope and elevation only, with no multispectral, vegetation or historical-map evidence. A negative reading from this pipeline is a triage signal for where to look next, not evidence that a location holds nothing.
