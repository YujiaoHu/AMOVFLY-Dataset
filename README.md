This dataset contains wind condition and flight process data totaling over 46 hours from 270 flights involving three unmanned aerial vehicles (UAVs). The dataset covers flight data under various scenario settings, including constant altitude and speed, constant altitude with variable speed, variable altitude with constant speed, variable altitude with variable speed , random flight, and multi-UAV flight in same time. This dataset holds significant value for researching the adaptability of UAVs in changing scenarios and tasks, as well as key AI issues such as sim-2-real transfer. If this dataset is useful for your work, please cite our paper.

# Flight Data
## Flight Data Statistics
We categorize and store various flight data in different folders according to different flight scenarios. Specifically, the FAFS folder contains data from drones flying at a fixed altitude and speed; the FAVS folder stores data from drones flying at a fixed altitude but with varying speeds; the VAFS folder holds data from drones flying at varying altitudes but with a fixed speed; the VAVS folder preserves data from drones flying at varying altitudes and speeds; and the Random folder keeps data from drones flying at random varying altitudes and speeds under manual control. Table below presents statistical data on the proportion of data from different scenarios, the aircraft used, flight durations, and other relevant information within the entire dataset.

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
In this work, we keep the raw unprocessed acquisition data and the ready data that are directly used for the study after merging the wind speeds, which are saved in the subfolder raw_data and the subfolder with the same name as the parent folder, respectively. We summarise where these raw and ready data are saved, the naming convention, and the contents therein in in table below.

| Folder       | Sub-Folder | File | Content |
|----------------|----------|----------|----------|
|Scenarios name|raw\_data| \[UAVcolor\]\_Wind\_\[PayloadParameter\]\[AltitudeParameter\]\[SpeedParameter\]\_\[FlightNumber\]\.csv |Raw wind speed and wind angle data|
|Scenarios name|raw\_data| \[UAVcolor\]\_\[PayloadParameter\]\[AltitudeParameter\]\[SpeedParameter\]\_date\[MMDDHHMM\]\_b\[BatteryCode\]\_\[Collector\]\.csv|Raw flight data|
|Scenarios name|Scenarios name| Uav\[UAVcolor\]\_\[PayloadParameter\]AltitudeParameter\]\[SpeedParameter\]\_\[Flight Number\]\.csv|**Ready Data**:flight data combined wind speed and wind angle |
## Ready Data Contents and Acquisition Methods
This subsection describes all the information contained in the readiness data and how this information is obtained, as shown in table below.
| Variable           | Unit   | Description                                                    | Data Source                                                 |
|--------------------|--------|----------------------------------------------------------------|-------------------------------------------------------------|
| time               | s      | Time elapsed during flight                                   | `rostopic:/mavros/imu/data`                                  |
| wind_speed         | m/s    | Wind speed relative to the drone's flight                      | HY-SA256 Anemometer USB Serial Port                          |
| wind_angle         | deg    | Wind angle relative to the direction of drone's flight         | HY-SA256 Anemometer USB Serial Port                          |
| air_pressure       | Pa     | Realtime air pressure during flight                           | `rostopic:/mavros/imu/static_pressure`                       |
| battery_voltage    | V      | System voltage measured immediately after the battery         | `rostopic:/mavros/battery`                                  |
| battery_current    | A      | System current measured immediately after the battery           | `rostopic:/mavros/battery`                                  |
| battery_remain     | %      | Remaining battery level                                     | `rostopic:/mavros/battery`                                  |
| gps_x;y            | m      | Position relative to the takeoff point                    | `rostopic:/mavros/local_position/pose`                       |
| gps_z              | m      | Altitude above the ground                                 | `rostopic:/mavros/local_position/pose`                       |
| real_lat;_long     | deg    | Longitude/Latitude of the actual trajectory                     | `rostopic:/mavros/global_position/raw/fix`                   |
| aim_lat;_long      | deg    | Longitude/Latitude of the reference trajectory                  | republish `rostopic:/current_waypoint`|
| o_x; _y; _z; _w    | quaternion | Aircraft orientation                                          | `rostopic:/mavros/imu/data`                                  |
| v_x; _y; _z        | m/s    | Ground speed                                                  | `rostopic:/mavros/local_position/velocity_local`             |
| la_x; _y; _z       | m/s²   | Ground acceleration                                           | `rostopic:/mavros/local_position/velocity_local` (check if correct topic for acceleration) |
| power              | W      | UAV battery output power (calculated as battery_voltage * battery_current). | Calculated from `battery_voltage` and `battery_current` values |

# Flight Information
In Flight_info.csv, we have provided supplementary explanations of the flight settings for each flight. This file records all external information related to the flight, including the scene setting for each flight (which is also the name of the folder containing the data files), takeoff time, flight route, data file name, UAV used, flight duration, battery number used, power consumption, total flight power, local wind speed, measured wind speed at the collection points, local atmospheric pressure, measured atmospheric pressure at the collection points, air density at the collection points, local temperature, local weather, and data collectors. The column name, descriptionand, and data source of each piece of information in the file are shown in the table below.
| Column name | Description | Data Source |
|--------|----------------------------------------------------------------|-------------------------------------------------------------|
| Data Dir    | The folder name containing the flight data (file name corresponds to the flight scene) | Parsed from raw flight data name |
| Date time   | The date and time when the flight started | Parsed from raw flight data name |
| Route       | The reference flight route for this flight | Parsed from raw flight data name |
| FlightName  | The file name of the flight data | Manually entered |
| Uav         | The UAV used for this flight | Parsed from raw flight data name |
| Length(s)   | The flight duration for this flight | Parsed from ready flight data file (the absolute difference between the first and last values in the "time" column for this flight) |
| BatteryName | The battery number used for this flight | Parsed from raw flight data name |
| BatteryCost | The total power consumption for this flight | Parsed from ready flight data file  (the difference between the first and last power values for this flight) |
| AllPower    | The total power used during this flight | Parsed from ready flight data file  (the sum of all power data for this flight) |
| WindSpeed_station | Wind speed observation data from the nearest weather station at the corresponding time | Data requested from Visual Crossing Weather web API |
| WindSpeed_test | The average of the UAV's measured absolute wind speed data on the day | Average of the middle 50% of wind speed data in the corresponding date's wind speed file in the "wind" folder|
| AirPressure_station | Atmospheric pressure observation data from the nearest weather station at the corresponding time | Data requested from Visual Crossing Weather web API |
| AirPressure_test | The average atmospheric pressure during this flight | Parsed from ready flight data |
| Air Density   | Air density | Calculated from AirPressure_station and WindSpeed_station data |
| Temperature | Temperature observation data from the nearest weather station at the corresponding time | Data requested from Visual Crossing Weather web API |
| Weather     | Weather observation data from the nearest weather station at the corresponding time | Data requested from Visual Crossing Weather web API |
| Pick Man    | The data collector for this flight | Manually entered |

# Multi-UAV Information
The Multi-UAV_infosheet.csv file records the corresponding data file names and takeoff times for each UAV during multi-UAV flights.The column name, and descriptionand in the file are shown in the table below.
| Column Name | Description |
| --- | --- |
| Uav1 | Name of the first UAV in multi-UAV flight |
| Uav1_time | Takeoff time of the first UAV |
| Uav2 | Name of the second UAV in multi-UAV flight |
| Uav2_time | Takeoff time of the second UAV |
| Uav3 | Name of the third UAV in multi-UAV flight |
| Uav3_time | Takeoff time of the third UAV |

# Flight Route
This dataset's flights involve a total of five different routes, and the aerial views and 3D simulations of these routes are stored in the "Route" folder.

# Absolute Wind
In the "wind" folder, we have recorded the absolute wind condition information for the collection days, providing users with real-world environmental references. This is distinct from the relative wind condition information in the data files, which was collected during the UAV's flight along the reference trajectory at different speeds. Absolute wind conditions refer to wind data collected while the UAV is hovering at a fixed altitude. In this folder, we differentiate the absolute wind condition data from different collection days using the naming convention: \[UAV Name\]\_wind\_\[Collection Time\]_\[Collection Altitude\].csv. The "Collection Altitude" indicates the height at which the UAV hovered during data collection. For example, "102040" signifies that the UAV hovered at 10m, 20m, and 40m, while "20" indicates that the UAV only hovered at 20m to collect wind conditions.

# Collector Information
The existing 270 flight data entries in this dataset were collected by five individuals, and their full names, email addresses, and organizations are presented in the following table.
| Collector (Pick man) | Full name | Email | Organization |
| --- | --- |--- | --- |
| lmj or mj  | Mengjie Lee | lmj1023@mail.nwpu.edu.cn | PhD candidates, Northwestern Polytechnical University  |
| hfh | Fanghao Han | FhHan996@163.com | Master candidates, Northwestern Polytechnical University |
| ly | Yi Liu | roryliu@mail.nwpu.edu.cn | Master candidates, Northwestern Polytechnical University |
| rcc | Chuncheng Ran | rcc@mail.nwpu.edu.cn | Master candidates, Northwestern Polytechnical University |
| ltc | Tianci Li | 2188342623@qq.com |  /  |
