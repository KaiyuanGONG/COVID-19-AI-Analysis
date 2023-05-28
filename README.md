# COVID-19-AI-Analysis

- [ ] 台湾 改成 台湾（中国）/ 直接合并数据

# 开源信息
https://www.nature.com/articles/s41597-020-0448-0


We collected data on the following:
- (a) Key dates, which include the date of onset of disease, date of admission to hospital, date of confirmation of infection, and dates of travel. 
- (b) Demographic information about the age and sex of patients/cases.
- (c) Geographic information, at the highest resolution available down to the district level. We excluded information that was at the building level so that cases could not be identified. Geographic information was subdivided into administrative units (admin 0 = country, admin 1 = province, admin 2 = county, admin 3 = city, and where available, specific locations).
- (d) Symptoms
- (e) Any additional information such as exposure to the Huanan seafood market or record of exposure to infected individuals. Summaries of the data are shown in Figs. 1 and 2.

**dataset**：
- ID
    - Unique identifier for reported case. Currently ID is run concurrently for cases reported from Hubei, China and cases reported outside of Hubei, China. ID order does not necessarily reflect epidemiological progression, or reporting date, and should not be used to order cases in temporal progression.

- age
    - Age of the case reported in years. When not reported, N/A is used. Age ranges are recorded as start_age-end_age e.g. 50–59.

- sex
    - Sex of the case. When not reported, N/A is used.

- city
    - Initial generic geographic metadata is reported here. Subsequently standardized via lookup with geographic reference table.

- province
    - Initial entry of name of the first administrative division in which the case is reported. Subsequently standardized via lookup with geographic reference table.

- country
    - Name of country in which the case is reported. Note that imported cases will be assigned to the country in which confirmation occurred
    - this is typically in the arrival country, rather than the site of infection. “Travel_history_location” will describe other locations of travel for such instances.

- wuhan(0)_not_wuhan(1)
    - Binary flag to distinguish cases from Wuhan, Hubei, China, from all other cases.
    - 0 denotes a case is reported in Wuhan,
    - 1 denotes a case reported elsewhere in the world.

- latitude
    - The latitude of the specific location (denoted as “point” in “geo_resolution”) where the case was reported, or the latitude of a representative location (denoted as “admin” in “geo_resolution”) within the administrative unit the case is reported.

- longitude
    - The longitude of the specific location (denoted as “point” in “geo_resolution”) where the case was reported, or the longitude of a representative location (denoted as “admin” in “geo_resolution”) within the administrative unit the case is reported.

- geo_resolution
    - An indicative field in which the spatial representativeness of “latitude” and “longitude” are described. “point” indicates that a specific location is being represented by these coordinates. “admin” denotes that the coordinates are representative of the administrative unit in which coordinates lie. Subsequent “admin3”, “admin2”, “admin1” and corresponding “admin_id” and “shapefile” will allow for a more specific representation to be had.

- date_onset_symptoms
    - Date when the reported case was recorded to have become symptomatic. Specific dates are reported as DD.MM.YYYY.
    - Ranges are recorded as DD.MM.YYYY - DD.MM.YYYY.
    - Ranges with uncertain start or finish dates are recorded as - DD.MM.YYYY and DD.MM.YYYY - respectively.

- date_admission_hospital
    - Date when the reported case was recorded to have been hospitalized. Specific dates are reported as DD.MM.YYYY.
    - Ranges are recorded as DD.MM.YYYY - DD.MM.YYYY.
    - Ranges with uncertain start or finish dates are recorded as - DD.MM.YYYY and DD.MM.YYYY - respectively.

- date_confirmation
    - Date when the reported case was confirmed as having COVID-19 using rt-PCR. Confirmation accuracy is contingent on the data source used. Specific dates are reported as DD.MM.YYYY.
    - Ranges are recorded as DD.MM.YYYY - DD.MM.YYYY.
    - Ranges with uncertain start of finish dates are recorded as - DD.MM.YYYY and DD.MM.YYYY - respectively.

- symptoms
    - List of symptoms recorded in the description of the case.

- lives_in_Wuhan
    - Recorded relationship of patient with city of Wuhan, Hubei, China. “yes” indicates that the case was a resident of Wuhan. “no” indicates that the case is not a resident of Wuhan (residential). No information indicates that no data was available.

- travel_history_dates
    - Recorded travel dates to and from Wuhan. Specific dates are reported as DD.MM.YYYY and indicate date when the individual left Wuhan.
    - Ranges are recorded as DD.MM.YYYY - DD.MM.YYYY when both are available.
    - Ranges with uncertain start of finish dates are recorded as - DD.MM.YYYY and DD.MM.YYYY - respectively.

- travel_history_location
    - An open field describing the recent recorded travel history of the case.

- reported_market_exposure
    - An open field indicating “yes” if there was reported market exposure and “no” if there was not.
    - N/A indicates that no information is provided.

- additional_information
    - Any additional information that may be informative about the case, such as the occupation of the patient, the purpose of their travels, the hospital they were admitted to, etc.

- chronic_disease_binary
    - 0 represents a case that was reported to have no chronic disease and 1 represents cases that reported a chronic disease

- chronic_disease
    - Reported chronic condition(s) of the reported case.

- source
    - URL identifying the source of this information

- sequence_available
    - If there was a genomic sequence available the accession number is inserted here.

- outcome
    - Patients outcome, as either “died” or “discharged” from hospital.

- date_death_or_discharge
    - Reported date of death or discharge in DD.MM.YYYY format.

- location
    - Location of the reported case.

- admin3
     - Administrative unit level 3 (e.g., zip code) of where the case was reported.

- admin2
    - Administrative unit level 2 (e.g., county) of where the case was reported.

- admin1
    - Administrative unit level 1 (e.g., province) of where the case was reported.

- country_new
     - Administrative unit level 0 (e.g., country) of where the case was reported.

- admin_id
    - Administrative unit ID of the lowest level available for the case reported.



参考开源进行数据清理（R）：
https://github.com/beoutbreakprepared/nCoV2019/tree/master/covid19/src
- tools.cleaner.R：这是一个工具脚本，包含用于数据清洗的函数。其他三个R文件（hubei.cleaner.R、outside-hubei.cleaner.R和completeness-tables.R）在执行数据清洗操作时使用了这个脚本。它可以被其他脚本通过source()函数加载和调用。

- hubei.cleaner.R：这个脚本用于清洗名为hubei.csv的原始数据文件。它加载了tools.cleaner.R脚本，并使用其中的函数进行数据清洗。清洗后的数据保存在clean-hubei.csv文件中。

- outside-hubei.cleaner.R：这个脚本用于清洗名为outside-hubei.csv的原始数据文件。它同样加载了tools.cleaner.R脚本，并使用其中的函数进行数据清洗。清洗后的数据保存在clean-outside-hubei.csv文件中。

- completeness-tables.R：这个脚本用于生成描述每个变量具有已知值比例的表格。它依赖于已经进行了数据清洗的数据集文件clean-hubei.csv和clean-outside-hubei.csv。它加载了tools.cleaner.R脚本，并使用其中的函数计算每个变量的完整性。然后，它打印出一个描述变量完整性的表格。

本文件夹中的文件解释：
metadata：
data.json


数据版本：
Github Latestdata

Kaggle：
COVID-19 Literature Clustering




# Data Dictionary

## Variable Names

| Variable                   | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| `id`                       | Unique identifier of case                                                   |
| `case_in_country`          | 随着病例序号增加，除了中国以外的其他国家病例累计个数                             |
| `reporting date`           | 报告时间                                                                     |
| `Unnamed: 3`               | 第三列空白无内容 case                                                         |
| `summary`                  | 大致情况描述，比如：武武汉居民，性别，什什么时间出现在过什么地方信息比较杂         |
| `location`                 | 所在位置（城市名）                                                            |
| `country`                  | 国家                                                                         |
| `gender`                   | 性别                                                                         |
| `age`                      | 年龄                                                                         |
| `symptom_onset`            | 值是一个时间（但是格式不规范要统一化）                                          |
| `If_onset_approximated`    | 发病时间是否为近似值（NA/0/1）                                                 |
| `hosp_visit_date`          | 医院就诊日期                                                                  |
| `exposure_start`           | 接触病毒的起始日期                                                             |
| `exposure_end`             | 接触病毒的结束日期（Na/日期）                                                   |
| `from Wuhan`               | 是否来自武汉（0/1/NA）                                                         |
| `death`                    | 是否死亡（0/1/日期）                                                             |
| `'recovered`               | 是否康复（0/1/日期）                                                             |
| `'symptom`                 | 症状（无数据/fever, abdominal pain, diarrhea等逗号隔开）                                                   |
| `source`                   | 消息来源（值为一些新闻媒体，有中文和英文，无其他文字）                                                   |
| `link`                     | 来源链接（均为URL）                                                   |


## Variable Coding

| Variable                   | Code                                                                           |
|----------------------------|--------------------------------------------------------------------------------|
| `id`                       | Integer                                                                        |
| `age`                      | String: `AGE` or `AGE-AGE` where `AGE` matches `[0-9]{1,2}`                    |
| `sex`                      | String: either `male` or `female`                                              |
| `city`                     | String                                                                         |
| `province`                 | String                                                                         |

## Missing Codes

| Value | Meaning            |
|-------|--------------------|
| NA    | Data not available |

## Data Completeness

| Variable                   | Proportion Complete | Dataset                        |
|----------------------------|---------------------|--------------------------------|
| `id`                       |            1.000000 | `data/clean-hubei.csv`         |
| `id`                       |            1.000000 | `data/clean-outside-hubei.csv` |
| `age`                      |            0.023187 | `data/clean-hubei.csv`         |
| `age`                      |            0.094852 | `data/clean-outside-hubei.csv` |
| `sex`                      |            0.009768 | `data/clean-hubei.csv`         |
| `sex`                      |            0.088418 | `data/clean-outside-hubei.csv` |
| `city`                     |            1.000000 | `data/clean-hubei.csv`         |
