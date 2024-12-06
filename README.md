This dataset contains wind condition and flight process data totaling over 43 hours from 270 flights involving three unmanned aerial vehicles (UAVs). It covers flight data under various scenario settings, including constant altitude and speed, constant altitude with variable speed, variable altitude with constant speed, variable altitude with variable speed (mentioned twice, possibly a repetition), random flight, and multi-UAV flight. This dataset holds significant value for researching the adaptability of UAVs in changing scenarios and tasks, as well as key AI issues such as sim-to-real transfer. If this dataset is useful for your work, please cite our paper.

# Flight Data
## Flight Data Dir and Statistics
We categorize and store various flight data in different folders according to different flight scenarios. Specifically, the FAFS folder contains data from drones flying at a fixed altitude and speed; the FAVS folder stores data from drones flying at a fixed altitude but with varying speeds; the VAFS folder holds data from drones flying at varying altitudes but with a fixed speed; the VAVS folder preserves data from drones flying at varying altitudes and speeds; and the Random folder keeps data from drones flying at random varying altitudes and speeds under manual control. Table 1 presents statistical data on the proportion of data from different scenarios, the aircraft used, flight durations, and other relevant information within the entire dataset.

Attention:The symbol "+" indicates that we will continue to supplement this type of data.
| Flight Scenario | Flight Count | Related Aircraft | Flight Duration | Dataset Proportion |
| --------------- | ------------ | ---------------- | --------------- | ------------------ |
| FAFS            | 33           | UavY             | 318.5 mins      | 12.2%            |
| FAVS            | 164          | UavY, UavR, UavG | 1741.4 mins     | 60.7%             |
| VAFS            | 32+          | UavY, UavR       | 293.5+ mins      | 11.8%              |
| VAVS            | 27+          | UavY, UavR       | 271.1+ mins      | 10.0%             |
| Random          | 14+          | UavY, UavR       | 140.1+ mins      | 5.1%               |
| Multi-UAV       | (25 pairs)+  | (UavR, UavY) (UavY, UavG) | 250.0 mins    | /                |
| Summary         | 270+         | UavR, UavY, UavG | 2764.6+ mins (46.1+ hours) | 100%             |
## Flight File Naming Rules
In this work, we keep the raw unprocessed acquisition data and the ready data that are directly used for the study after merging the wind speeds, which are saved in the subfolder raw_data and the subfolder with the same name as the parent folder, respectively. We summarise where these raw and ready data are saved, the naming convention, and the contents therein in Table 2.

| Folder       | Sub-Folder | File | Content |
|----------------|----------|----------|----------|
| | Row 1, Col 2 | Row 1, Col 3 | Row 1, Col 4 |
|     |          |          |          |
|                | Row 3, Col 2 | Row 3, Col 3 | Row 3, Col 4 |
## Ready Data Contents and Acquisition Methods
This subsection describes all the information contained in the readiness data and how this information is obtained, as shown in Table 3.
