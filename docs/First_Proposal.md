# DATA 606: Capstone Project in Data Science

## 1. Title and Author
**Project Title:** Parking Space Predictor

**Prepared for:** UMBC Data Science Master Degree Capstone by Dr. Chaojie (Jay) Wang

**Author Name:** Viral Harishkumar Jani

**Link to the author's GitHub profile:** [Viral Github](https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral)

**Link to the author's LinkedIn profile:** [Viral LinkedIn](https://www.linkedin.com/in/viral-jani-8137081a2/)

## 2. Background
**Why choose this project?**

Parking in urban areas is increasingly becoming a challenge due to the growing number of vehicles and limited space. The ability to predict parking availability can significantly reduce the time drivers spend searching for parking, leading to reduced congestion and carbon emissions.

**What is it about?**

The project aims to develop a model that predicts parking space availability in real-time, using data from parking lot sensors and other external factors like events, traffic data, and historical parking trends.

**Why does it matter?**

Such a predictive system can:
- Save time for drivers.
- Reduce fuel consumption and emissions.
- Aid city planners in understanding parking demand.
- Support the development of smart city initiatives.

**Research Questions:**

- Can we accurately predict parking availability in real-time?
- Which factors most influence parking availability?
- How does the prediction accuracy vary by time of day, day of the week, or specific events?

## 3. Data
- The data for this project will be mostly Image data of the parking lots. There are more than 10K+ images from which we can predict if the slot will be occuiped or free.

**Data sources:**
- Parking lot: https://web.inf.ufpr.br/vri/databases/parking-lot-database/

- CNRPark: http://cnrpark.it/dataset/CNRPark-Patches-150x150.zip

- CNR-EXT: http://cnrpark.it/dataset/CNR-EXT-Patches-150x150.zip

**Data size:** Approximately 3+ GB

**Data shape:**  157449 rows x 12 columns

**What does each row represent?**

1. The CNRPark+EXT.csv dataset consists of the following columns:

- **camera:** The camera that took the photo.
- **datetime:** The timestamp when the photo was taken.
- **day:** Day of the month.
- **hour:** Hour of the day.
- **image_url:** URL of the image.
- **minute:** Minute of the hour.
- **month:** Month of the year.
- **occupancy:** Whether the parking slot is occupied (1) or free (0).
- **slot_id:** The ID of the parking slot.
- **weather:** Weather condition at the time the photo was taken.
- **year:** Year when the photo was taken.
- **occupant_changed:** Indicates if the occupant changed compared to the previous snapshot 

2. **CNRPark** dataset has segmented images (patches) of parking spaces belonging to the CNRPark preliminary subset.
- Files follow this organization:
  - CAMERA/CLASS/YYYYMMDD_HHMM_SLOT_ID.jpg, where:
    - CAMERA can be "A" or "B",
    - CLASS can be "free" or "busy",
    - YYYYMMDD_HHMM is the zero-padded 24-hour capture datetime,
    - SLOT_ID is a local ID given to the slot for that particular camera

3. **CNR-EXT** dataset has segmented images (patches) of parking spaces belonging to the CNR-EXT subset.
- Files follow this organization:
  - PATCHES/WEATHER/CAPTURE_DATE/cameraCAM_ID/W_ID_CAPTURE_DATE_CAPTURE_TIME_C0CAM_ID_SLOT_ID.jpg,
where:
    - WEATHER can be "SUNNY", "OVERCAST" or "RAINY",
    - CAPTURE_DATE is the zero-padded YYYY-MM-DD formatted capture date,
    - CAM_ID is the number of the camera, ranging 1-9,
    - W_ID is a weather identifier, that can be "S", "O" or "R",
    - CAPTURE_TIME is the zero-padded 24-hour HH.MM formatted capture time,
    - SLOT_ID is a global ID given to the monitored slot; this can be used to uniquely identify a slot in the CNR-EXT dataset.
  - The LABELS folder contains a list file for each split of the dataset used in our experiments. Each line in list files follow this format: <IMAGE_PATH> <LABEL>, where:
    - IMAGE_PATH is the path to a slot image,
    - LABEL is 0 for free, 1 for busy.
   
4. **CNR-EXT_FULL_IMAGE** dataset has full frames of the cameras belonging to the CNR-EXT subset. Images have been downsampled from 2592x1944 to 1000x750 due to privacy issues.
- Files follow this organization:
  - FULL_IMAGE_1000x750/<WEATHER>/<CAPTURE_DATE>/camera<CAM_ID>/<CAPTURE_DATE>_<CAPTURE_TIME>.jpg,
where:
    - WEATHER can be SUNNY, OVERCAST or RAINY,
    - CAPTURE_DATE is the zero-padded YYYY-MM-DD formatted capture date,
    - CAM_ID is the number of the camera, ranging 1-9,
    - CAPTURE_TIME is the zero-padded 24-hour HHMM formatted capture time.
