# DATA 606: Capstone Project in Data Science

## 1. Title and Author
**Project Title:** Parking Space Predictor

**Prepared for:** UMBC Data Science Master Degree Capstone by Dr. Chaojie (Jay) Wang

**Author Name:** Viral Harishkumar Jani

**Link to the GitHub profile:** [Viral Github](https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral)

**Link to the LinkedIn profile:** [Viral LinkedIn](https://www.linkedin.com/in/viral-jani-8137081a2/)

**Link to the Youtube Video:** [Project_Video_Presentation]()

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
- The data for this project will be Image data of the parking lots. There are more than 10K+ images from which we can predict if the slot will be occuiped or free.

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

## 4. Exploratory Data Analysis (EDA)

To gain insights into the parking space availability, we performed an exploratory data analysis on a subset of the data. The EDA process involved examining general statistics, identifying missing values, and analyzing the distribution of occupancy, both by camera and over time.

#### General Statistics

Our dataset contains images captured from two unique cameras labeled 'A' and 'B,' with the majority of images coming from camera 'B'. All data is from the year 2015. We have information on 184 unique parking slots, indicating a substantial parking area under surveillance. Here's a brief overview of the general statistics:

- **Camera**: 'A' and 'B' with predominant data from 'B'
- **Year**: 2015
- **Occupancy**: Approximately 67% occupancy rate
- **Slots**: 184 unique parking slots

#### Missing Values

We noticed that the `occupant_changed` column has 4,183 missing entries. This could indicate the absence of prior snapshot comparisons or an issue with data capture.

#### Distribution of Occupancy
<img width="271" alt="image" src="https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral/assets/143745173/6ee42a1d-ef11-40d3-af09-60ac67751c6c">

The analysis of occupancy distribution revealed that occupied parking slots outnumber free slots, indicating a high demand for parking space within the sampled data range.

#### Occupancy by Camera
<img width="275" alt="image" src="https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral/assets/143745173/ccf31739-f005-491f-990b-9fa6080e7657">

When comparing the occupancy rates across the two cameras:

- **Camera A**: Showed a near-even distribution between free and occupied parking slots.
- **Camera B**: Demonstrated a higher proportion of occupied slots, suggesting varying parking patterns or possibly a higher utilization rate of the parking area it monitors.

#### Occupancy Over Time
<img width="324" alt="image" src="https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral/assets/143745173/c742c135-ab25-4729-8863-30bfb6b1a159">

Observing the hourly distribution of parking occupancy, we discovered patterns that align with typical urban commuting behaviors:

- **Morning (7-10 AM)**: Occupancy is slightly higher than availability, hinting at early morning commuters securing parking spots.
- **Mid-day (10 AM-3 PM)**: A significant peak in occupancy suggests a concentration of activities around these hours, with more slots being occupied.
- **Afternoon (3-6 PM)**: Although occupancy starts to decline, there remains a higher occupancy than availability, which may ease off as people leave the area.

This trend suggests the busiest period in the parking area is around mid-day, likely influenced by standard office hours, shopping, or local events.

The visualizations and data points discussed in this section are crucial for understanding the dynamics of parking space usage and will inform the subsequent modeling efforts.

## 5. Machine Learning Model

#### Initial Approach with ResNet50

The project's initial phase involved preprocessing image data into 'Free' and 'Busy' categories using the OpenCV library, which facilitated the exploration of the image distribution. Following this, the ResNet50 model, implemented using TensorFlow and Keras, was applied to the processed data. However, the model exhibited signs of overfitting, as indicated by perfect training accuracy contrasted with a constant validation accuracy of approximately 61.70%. Moreover, a steadily increasing validation loss suggested that the model was not generalizing well to unseen data.

<img width="532" alt="image" src="https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral/assets/143745173/4e509485-1cac-420a-bb3a-dc8c03002364">

#### Transition to MobileNet

Given the limitations of ResNet50, the MobileNet model was adopted due to its lighter architecture. With the introduction of data augmentation, dropout layers, L2 regularization, and implementation of early stopping and learning rate reduction strategies, the MobileNet model demonstrated more balanced results. Training accuracy remained high without reaching 100%, and validation accuracy improved to around 76.60%, indicating better generalization.

<img width="548" alt="image" src="https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral/assets/143745173/47e09d48-197b-4f73-9691-8e1bea948c12">

#### Refinement and Fine-Tuning

Further refinement of the MobileNet model, including enhanced data augmentation and fine-tuning of the last few layers, yielded significant improvements. The training accuracy reached approximately 93.16%, and validation accuracy saw peaks at 100%, with a more stable and reduced validation loss. Early stopping ensured the prevention of overfitting, halting the training process when no improvement was observed for a set number of epochs.

<img width="565" alt="image" src="https://github.com/DATA-606-2023-FALL-MONDAY/Jani_Viral/assets/143745173/463c9bea-9bbc-41a4-8dd1-094300dadf99">

#### Adoption of YOLOv5

Despite the advancements with MobileNet, YOLOv5 was identified as a more suitable model for the project's objectives due to its fast and accurate detection capabilities. YOLOv5's ability to process images in real-time and provide precise bounding boxes significantly enhanced the detection of parking space occupancy.

#### Implementation and Results with YOLOv5:

- **Accuracy**: YOLOv5 achieved high accuracy in detecting parked cars, a critical requirement for the project.
- **Speed**: The model's real-time processing capability was crucial for detecting dynamic changes in parking space occupancy.
- **Precision**: The bounding boxes around the cars were precise, aiding in the clear distinction between occupied and free parking spaces.
- **Adaptability**: Training YOLOv5 on a custom dataset ensured the model was well-tuned for the specific conditions of the parking lot.

In the final demonstration, the YOLOv5 model's efficacy was showcased through a video where the model accurately identified free parking spaces with green bounding boxes and occupied spaces with red boxes. This visualization highlighted the practical application of the model in a real-world scenario.

#### Conclusion of Machine Learning Implementation

The evolution of the machine learning approach in this project underscored the importance of selecting the right model and refining it to match the data characteristics. YOLOv5 emerged as the best-performing model, aligning with the project's need for accuracy and real-time detection in parking space occupancy.

[Link to the demonstration video](https://youtu.be/UxVQqHXkRXM)

## 6. Conclusion

This capstone project embarked on the ambitious goal of developing a system to predict real-time parking space availability. The journey began with a clear understanding of the urban challenges posed by parking and progressed through various stages of data collection, exploratory data analysis, and machine learning model implementation.

The exploratory data analysis provided valuable insights into parking lot occupancy patterns, revealing peak times and potential influences on parking space availability. However, the true crux of the project lay in the development and refinement of a predictive model capable of discerning between occupied and free parking spaces.

Initial modeling attempts with ResNet50 highlighted the common pitfalls of machine learning, such as overfitting and the challenge of generalization to new data. The subsequent transition to MobileNet marked a significant turning point, leading to improved validation accuracy and more stable loss metrics, thanks to strategic data augmentation, regularization, and a revised learning rate schedule.

The final foray into the realm of YOLOv5 brought the project to its zenith. YOLOv5's robust performance in terms of accuracy, speed, and precision demonstrated the model's superiority in handling the real-time detection tasks essential for the project's success. The accompanying demonstration video serves as a testament to the model's capabilities, showcasing the practical applicability of the system in live scenarios.

The implications of this project extend beyond the technical achievement of model development. The potential for this system to contribute to smart city initiatives, reduce environmental impact, and alleviate urban congestion speaks to the broader societal benefits of data science and artificial intelligence.

As we look to the future, there are several paths this project could take. Continued refinement of the model, expansion to a wider array of parking environments, and integration with city infrastructure could all enhance the system's effectiveness and reach. There is also the exciting potential to incorporate emerging technologies, such as IoT devices and more advanced neural network architectures, to further elevate the system's capabilities.

In conclusion, the Parking Space Predictor stands as a prime example of how data science can provide tangible solutions to everyday problems, driving innovation that marries technical prowess with real-world impact.

**Author Name:** Viral Harishkumar Jani

**Semester:** Fall 2023

**Acknowledgements:** I would like to express my sincere gratitude to Dr. Chaojie (Jay) Wang for his invaluable guidance and support throughout this capstone project. I am also thankful to the UMBC Data Science program for providing the resources and environment conducive to learning and innovation.

