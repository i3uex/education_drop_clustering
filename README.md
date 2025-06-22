# An empirical evaluation of clustering processes for early detection of university dropout
The elevated rates of dropout within academic institutions have prompted the use of Artificial Intelligence (AI) to tackle this issue. These efforts often rely mainly on administrative and academic data, lacking personal information about students. In a previous study, we explored machine learning models to leverage this data and harness their knowledge-extraction capabilities. However, a critical factor, the availability of labeled data, was not addressed. Obtaining these data may be challenging due to their distribution across different systems or the considerable time required to collect them, especially when new degrees are being implemented. The lack of labeled data is a major obstacle for institutions that do not possess them so that they are unable to take advantage of the full potential of AI for their purposes. Clustering algorithms have conventionally been employed to uncover latent patterns within unlabeled data. These unsupervised algorithms may reduce the need for data labeling; nonetheless, it necessitates rigorous validation of the resulting clusters, particularly when dealing with datasets encompassing numerical and categorical attributes. This paper introduces a comparison of various clustering algorithms to discern the most appropriate technique for uncovering the underlying factors contributing to university student attrition, employing unlabeled data. The novelty lies not only in the algorithmic comparison but also in their integration with diverse data preprocessing methodologies, streamlining the selection of the optimal combination including advanced data transformations for the harmonization of numerical and categorical information. It is illustrated through a real-world case utilizing academic data from a Spanish university, providing empirical validation for the proposed methodology. The insights gained can be extrapolated to analogous experiments where social or economic data is scarce, and most of the available attributes are academic in nature.

## Data
The original data from this study are not available because they are private data. However, in order that this study can be replicated, we indicate below the structure of the 3 main datasets used to carry out the study. If the user wants to reproduce it easily, he can generate a synthetic dataset with this structure.

__Enrolment data:__
| Feature                        | Description                                                                             | Class Description                                                                                     | # Class |
| ------------------------------ | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------- |
| Id                             | Student ID                                                                              | Numerical Values                                                                                      | 1718    |
| Degree ID                      | Unique Degree Identifier                                                                | Numerical Values                                                                                      | 16      |
| Degree Name                    | Degree Name                                                                             | Categorical: Computer Science Engineering, Civil Engineering, Telecommunication Engineering...        | 16      |
| Enrolment Year                 | First Academic Year of Studies                                                          | Categorical: 2007-08, 2008-09...                                                                      | 14      |
| Closed                         | Indicate whether the record is closed                                                   | Binary: Y, N                                                                                          | 2       |
| Transferred                    | Indicate whether the record is transferred to other institution                         | Binary: Y, N                                                                                          | 2       |
| TransferType                   | Indicates the reason for the transfer of a record                                      | Categorical: Internal, External, Simultaneous                                                          | 3       |
| Blocked                        | Indicate whether the record is blocked                                                  | Binary: Y, N                                                                                          | 2       |
| Call                           | Call for Access                                                                         | Categorical: June, September...                                                                       | 8       |
| Call Year                      | Year of the Call for Access                                                             | Categorical: 2007-08, 2008-09...                                                                      | 14      |
| Access ID                      | Access Type Unique Identifier                                                           | Numerical Value                                                                                       | –       |
| Access Description             | Access Type Description                                                                 | Categorical: University Entrance Exam, Transferred, 25 years of age or older, validated diploma...    | 11      |
| SubAccess ID                   | Subaccess Type Unique Identifier                                                        | Numerical Value                                                                                       | –       |
| SubAccess Description          | Subaccess Type Description                                                              | Categorical: LOE, LOGSE, LOMCE...                                                                     | 7       |
| Marks                          | University Entrance Exam                                                                | Numerical Value between 0 and 14                                                                       | –       |
| Origin Educational Institution | Origin Educational Institution                                                          | Categorical: List of names of the origin High Schools                                                 | 137     |
| Gender                         | Student's gender                                                                        | Categorical: H, M                                                                                     | 2       |
| Birth                          | Date of Birth                                                                           | Date                                                                                                  | –       |
| Province ID                    | Province ID                                                                             | Numerical Value                                                                                       | –       |
| Province Name                  | Province Name                                                                           | Categorical: Salamanca, Toledo, Sevilla, Alicante...                                                  | 50      |
| Municipality ID                | Municipality ID                                                                         | Numerical Value                                                                                       | –       |
| Municipality Name              | Municipality Name                                                                       | Categorical: Sevilla, Madrid, Salamanca, Toledo...                                                    | 434     |
| Dropout                        | Indicates if the student has dropped out                                                | Binary: Y, N                                                                                          | 2       |

__Qualifications data:__
| Feature                  | Description                                                       | Class Description                                                                                     | # Class |
| ------------------------ | ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------- |
| Id                       | Student ID                                                        | Numerical Values                                                                                      | 1718    |
| Degree ID                | Unique Degree Identifier                                          | Numerical Values                                                                                      | 16      |
| Degree Name              | Degree Name                                                       | Categorical: Computer Science Engineering, Civil Engineering, Telecommunication Engineering...        | 16      |
| Subject ID               | Unique Subject Identifier                                         | Numerical Values                                                                                      | –       |
| Subject Name             | Name of the Subject                                               | Categorical: Physics, Linear Algebra, Data Structures and Algorithms, Calculus, Economics and Business… | 332     |
| Year                     | Year                                                              | Numerical Values between 1 and 4                                                                       | –       |
| Semester                 | Semester of the Academic Year                                     | Categorical: 1S, 2S, Annual                                                                           | 3       |
| Subject Type ID          | Subject Type Unique Identifier                                    | Categorical: B, T, O, P, C, E                                                                         | 6       |
| Subject Type Description | Subject Type Description                                          | Categorical: Core, Compulsory, Optional, Internship…                                                   | 6       |
| Academic Year            | Academic Year                                                     | Categorical: 2007-08, 2008-09...                                                                      | 14      |
| Call                     | Call of Subject Examination                                       | Categorical: June, September, February...                                                             | 8       |
| Mark                     | Mark                                                              | Categorical: Not Taken, Fail, Compensation, Sufficient, Very Good, Outstanding, With Honours          | 7       |
| Numerical Mark           | Mark in Numerical Format                                          | Numerical Values from 0 to 10                                                                          | –       |
| Attempt                  | Attempt Number                                                    | Numerical Values from 1 to 6                                                                           | –       |

__Scolarship data:__

| Feature          | Description                                                      | Class Description                                            | # Class |
| ---------------- | ---------------------------------------------------------------- | ------------------------------------------------------------ | ------- |
| Id               | Student ID                                                       | Numerical Values                                             | 1718    |
| Academic Year    | Academic Year                                                    | Categorical: 2007-08, 2008-09...                             | 14      |
| Degree ID        | Unique Degree Identifier                                         | Numerical Values                                             | 16      |
| Degree Name      | Degree Name                                                      | Categorical: Computer Science Engineering, Civil Engineering, Telecommunication Engineering… | 16      |
| Scholarship      | Indicates if the student has a scholarship                       | Binary: Y, N                                                 | 2       |


## License
This project is licensed under the [MIT License](https://github.com/apitepuex/education_drop_clustering/blob/main/LICENSE)


## Project structure:
This project is based on the framework defined by [MD4DSPRR Utils](https://github.com/i3uex/apitep_utils). 

This framework defines the structure of a data science project divided into the following phases:
- __ETL__: Extract Transform and Load data tasks
- __Feature Engineering__: process of creating or transforming features to enhance model performance.
- __Analysis and Modelling__: process of analysing data using machine learning models or other techniques.

Furthermore, in our case, using the ETL class, we will implement an additional phase called __Fetch Data__, which will allow us to give a common format to the raw data of the project.

Based on this framework, the structure of this project is as follows:
- __Data__:
    - __Raw__: raw originally data.
    - __Interim__: data with common format.
    - __Processed__: data resulting from the application of the ETL phase
    - __For_analyisis_and_modeling__: data resulting from the application of the Feature Engineering phase.
- __Code__:
  - __data_acquisition_and_understanding__: 
    - __fetch_data__: Data capture and formatting into a common format.
    - __etl__:  Data that may provide noisy information to the models are eliminated, mainly due to being incomplete or not providing correct information.
  - __feature_engineering__: features creation, elimination and fusion for personal access data and for course data.
  - __analysis_and_modeling__: notebooks with different experiments based on clustering algorithms: K-Means, Agglomerative, Gaussian Mixture, K-Modes and COOLCCAT.

## Prerequisites

- **Python 3.10** (virtual environment recommended)
- **Operating System:** Linux (or Windows Subsystem for Linux)
- **Dependencies:** All packages listed in `requirements.txt`
- **R 4.3.2** (For ROCK and COOLCAT Algorithms)

## Setup

1. Create and activate a virtual environment:
   ```bash
   python3.10 -m venv .venv
   source .venv/bin/activate
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Running the Pipeline

To execute the phases: Fetch data, ETL and Feature Engineering with DVC, run:

```bash
 dvc repro
```
This will sequentially perform:

1. **fetch data**
2. **ETL**
3. **feature engineering**
The analysis and modelling phase has been implemented using Jupyer notebooks and .R files.

## Launching Clustering Models

- **Python-based models:** Open the corresponding Jupyter notebooks and run each cell in order.
- **ROCK & COOLCAT algorithms:** Open and execute the provided `.R` scripts.
