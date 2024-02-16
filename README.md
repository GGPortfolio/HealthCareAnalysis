# Health Care Analysis (Case Study)
<p><a href="https://app.powerbi.com/view?r=eyJrIjoiNThlYjI1OGEtZWE2OC00Y2ZkLWFhNDMtMTdmZWY3ZDgzMzJhIiwidCI6Ijk5YjY0NTFkLTRmY2QtNDE1Zi1iNGJlLWQ5N2ZhZGJjZGI5ZiJ9">View Interactive Dashboard</a></p>

## About this Case Study 
In healthcare, improving efficiency while maintaining high-quality patient care is a top priority. In this Power BI Case study, I've explored a real-world health care dataset to uncover hospital efficiency insights for a fictional consulting company called HealthStat. The dataset contains information about inpatient stays in New York State. 
I analyzed attributes impacting the patient length of stay (LOS) and cost and worked to identify factors contributing to hospital differences. Leveraging my DAX skills I created measures and generated insightful visualizations. To finish off, I brought it all together in a sophisticated business dashboard to communicate insights for the HealthStat team. This case study gave me a chance to practice a range of Power BI skills, working with real-world data.
The dataset, Hospital_Data.csv, contains 26,594 rows among 30 columns. 
<p>Source: <a href="https://assets.datacamp.com/production/repositories/6258/datasets/1c2296146603afb24cc12332c71dd82a6d8e26ec/Metadata%20-%20Case%20study_%20Analyzing%20Healthcare%20data%20in%20Power%20BI.pdf">Hospital Discharges</a></p>
<p></p>https://health.ny.gov/statistics/</p>


## 1. Purpose of this Case Study

<ol style="list-style-type: upper-alpha;">
<li>Create a powerful dashboard report that enables an understanding of the key impacts on average LOS and cost for hospitals across the state of New York.</li>
<li>Using insights to inform on where targeted quality improvements can be made to both improve the hospital's operational efficiency as well as the patient experience</li>
</ol>

## Insights Explored

<ol style="list-style-type: upper-alpha;">
<li>Which hospitals stand out with the highest cost and LOS (length of stay) relative to the state average?</li>
<li>Which hospitals stand out as the biggest outliers overall?</li>
<li>Does larger surgical program size impact LOS and cost?</li>
<li>Root cause analysis: What factors influence LOS and cost the most?</li>
</ol>

## 2. Key DAX Measures Created

```
% VAR Average LOS Days = DIVIDE(([Average LOS Days]-[Average LOS Days ALL]),[Average LOS Days ALL])
```
```
% Var Avg Cost / Discharge = DIVIDE(([AVG Cost / Discharge]-[AVG Cost / Discharge ALL]),[AVG Cost / Discharge ALL])
```
```
Average LOS Days = AVERAGE(Hospital_Data[length_of_stay])
```
```
AVG Cost / Discharge = DIVIDE(SUM(Hospital_Data[total_costs]),[Total Discharges])
```
```
Total Surgeons = DISTINCTCOUNT(Hospital_Data[operating_provider_license_number])
```
## 3. New Table
Used a DAX function, SUMMARIZECOLUMNS(), to create a new table called surgical_program_volume_summary. The purpose of creating a new table was to account for surgical program size as a variable. The source data did not explicitly state the surgical program size, so a proxy was required. The new table summarized total discharges and surgeons by hospital and was joined to the master data table to continue analysis. 

```
Surgical_program_volume_summary = SUMMARIZECOLUMNS(Hospital_Data[facility_name],"Total Discharges",[Total Discharges],"Total Surgeons",[Total Surgeons])
```
```
Surgical Program Size = SWITCH(
                                TRUE(),
                                Surgical_program_volume_summary[Total Discharges (bins)] =0 ,"<200",
                                Surgical_program_volume_summary[Total Discharges (bins)]= 200 , "200-399",
                                Surgical_program_volume_summary[Total Discharges (bins)]= 400 , "400-599",
                                ">=600"
```

![Hospital Model](https://github.com/GGPortfolio/HealthCareAnalysis/assets/159342547/7c0ab869-86fc-467a-9848-30d1809eec74)

## 4. Dashboard 

### Key Insights:
<ol style="list-style-type: upper-alpha;">
<li>Average LOS is 2.65 days&nbsp;</li>
<li>Average Cost of Discharging is $21,000</li>
<li>The top 2 factors that result in an increase in LOS and Cost are Severity of Ilness and Risk of Mortality</li>
<li>The report further allows us to analyze each hospitals performance against the state average.</li>
</ol>
   

<p><span style="color: #0000ff;"><strong>CLICK&nbsp;on the image to interact with the visual!&nbsp;</strong></span></p>

[![Health_Care_Dashboard](https://github.com/GGPortfolio/HealthCareAnalysis/assets/159342547/bbbb5309-7e2f-40a4-9f63-7430671fe5b8)](https://app.powerbi.com/view?r=eyJrIjoiNThlYjI1OGEtZWE2OC00Y2ZkLWFhNDMtMTdmZWY3ZDgzMzJhIiwidCI6Ijk5YjY0NTFkLTRmY2QtNDE1Zi1iNGJlLWQ5N2ZhZGJjZGI5ZiJ9)

