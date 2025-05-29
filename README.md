# Numpy Data Analytics on Tech Jobs in Nigeria

## Project Overview

This project uses **NumPy** to simulate, analyze, and extract insights from synthetic data representing tech jobs in Nigeria. It covers aspects like job roles, cities, employment types, experience levels, salary distributions, and gender pay analysis. The goal is to understand salary trends, disparities, and job market characteristics in the Nigerian tech sector.

---

## 📬 Author

**Gbenga Kajola**

[LinkedIn](https://www.linkedin.com/in/kajolagbenga)

[Certified_Data_Scientist](https://www.datacamp.com/certificate/DSA0012312825030)

[Certified_Data_Analyst](https://www.datacamp.com/certificate/DAA0018583322187)

[Certified_SQL_Database_Programmer](https://www.datacamp.com/certificate/SQA0019722049554)


---

## Dataset Simulation

- **Job Titles:** 20 common tech roles (e.g., Data Analyst, Software Engineer, AI/ML Engineer).
- **Cities:** 5 Nigerian cities (Lagos, Abuja, Port Harcourt, Enugu, Ibadan).
- **Employment Types:** Remote, On-site, Hybrid.
- **Experience Levels:** 0-2 yrs, 3-5 yrs, 6-10 yrs, 10+ yrs.
- **Salaries:** Simulated based on realistic salary ranges per job role, randomly assigned to 200 records.

A fixed random seed ensures reproducibility of results.

---

## Code Explanations

### 1. Salary Generation per Job Role

```python
salary = np.array([
    np.random.randint(*salary_ranges[job]) for job in job_role
])
```

- For each job role in `job_role`, randomly generates a salary within its defined range.
- Uses list comprehension to efficiently create a salary array.
- `*salary_ranges[job]` unpacks the low and high range values for `np.random.randint`.
- The resulting `salary` array holds 200 simulated salary values corresponding to each job role.

---

### 2. Average Salary by Job Title

```python
for title in np.unique(job_titles):
    avg_sal = np.mean(salary[job_role == title])
    print(f"{title}: Average Salary = ₦{avg_sal:,.2f}")
```

- Loops over unique job titles.
- Filters salaries corresponding to each title.
- Calculates and prints the average salary formatted with the Naira symbol and two decimals.

---

### 3. Average Salary by Experience Level

```python
for level in np.unique(experience_levels):
    exp_sal = np.mean(salary[experience == level])
    print(f"{level}: Avg Salary = ₦{exp_sal:,.2f}")
```

- Calculates average salary per experience level by filtering salaries where experience matches the level.
- Helps understand how salary grows with experience.

---

### 4. Ordered Experience Level Salary Display

```python
ordered_experience_levels = ['0-2 yrs', '3-5 yrs', '6-10 yrs', '10+ yrs']

for level in ordered_experience_levels:
    exp_sal = np.mean(salary[experience == level])
    print(f"{level:<8}: Average Salary = ₦{exp_sal:,.2f}")
```

- Displays average salary by experience level in a logical ascending order.
- Enhances readability by avoiding unordered default sorting.

---

### 5. Experience Level Salary Sorted Descending

```python
exp_salaries = []
for level in np.unique(experience_levels):
    exp_sal = np.mean(salary[experience == level])
    exp_salaries.append((level, exp_sal))

exp_salaries.sort(key=lambda x: x[1], reverse=True)

for level, sal in exp_salaries:
    print(f"{level}: Avg Salary = ₦{sal:,.2f}")
```

- Collects (experience level, average salary) tuples.
- Sorts these tuples descending by salary.
- Prints experience levels from highest to lowest average salary.

---

### 6. Average Salary by City

```python
for city_name in np.unique(cities):
    city_sal = np.mean(salary[city == city_name])
    print(f"{city_name}: Avg Salary = ₦{city_sal:,.2f}")
```

- Computes and prints average salary for each Nigerian city.
- Reveals geographic salary variations.

---

### 7. Average Salary by Employment Type

```python
for etype in np.unique(emp_type):
    etype_sal = np.mean(salary[emp_type == etype])
    print(f"{etype}: Avg Salary = ₦{etype_sal:,.2f}")
```

- Computes average salaries for Remote, On-site, and Hybrid roles.
- Useful for understanding salary impacts of work arrangements.

---

### 8. High-paying Remote Roles

```python
high_remote = (salary > 500000) & (emp_type == 'Remote')
print("High-paying Remote Roles:")
print(job_role[high_remote])
print(salary[high_remote])
```

- Filters for remote jobs with salary above ₦500,000.
- Prints roles and salaries that qualify as high-paying remote positions.

---

### 9. Roles with Above Industry Average Salary

```python
overall_avg = np.mean(salary)
above_avg = job_role[salary > overall_avg]
unique_roles = np.unique(above_avg)

print("Roles with Salaries Above Industry Average:")
print(unique_roles)
```

- Calculates overall average salary.
- Identifies unique job roles where salaries exceed this average.
- Highlights better-paid job roles in the dataset.

---

### 10. Salary Range (Spread) per Role

```python
for role in np.unique(job_titles):
    role_salaries = salary[job_role == role]
    spread = np.max(role_salaries) - np.min(role_salaries)
    print(f"{role}: Spread = ₦{spread:,}")
```

- Calculates the salary range (max - min) for each job role.
- Shows how widely salaries vary within roles, indicating possible seniority or negotiation differences.

---

### 11. Salary Percentiles by Experience Level

```python
for level in np.unique(experience_levels):
    sal_by_exp = salary[experience == level]
    p25 = np.percentile(sal_by_exp, 25)
    p50 = np.percentile(sal_by_exp, 50)  # median
    p75 = np.percentile(sal_by_exp, 75)
    print(f"{level} → 25th: ₦{p25:,.0f}, 50th (median): ₦{p50:,.0f}, 75th: ₦{p75:,.0f}")
```

- Calculates 25th, 50th (median), and 75th percentiles of salary for each experience level.
- Helps understand salary distribution spread and median compensation.

---

### 12. Average Salary by Job Role (Descending)

```python
job_avg_salaries = []
for role in np.unique(job_role):
    avg = np.mean(salary[job_role == role])
    job_avg_salaries.append((role, avg))

job_avg_salaries.sort(key=lambda x: x[1], reverse=True)

for role, avg in job_avg_salaries:
    print(f"{role}: ₦{avg:,.0f}")
```

- Computes and sorts average salary per job role in descending order.
- Useful for identifying top-paying roles at a glance.

---

### 13. Gender Pay Analysis

```python
genders = np.random.choice(['Male', 'Female'], n)

male_avg = np.mean(salary[genders == 'Male'])
female_avg = np.mean(salary[genders == 'Female'])

pay_gap = male_avg - female_avg
pay_gap_percent = (pay_gap / male_avg) * 100

print("\nGender Pay Analysis:")
print(f"Average Salary (Male): ₦{male_avg:,.2f}")
print(f"Average Salary (Female): ₦{female_avg:,.2f}")
print(f"Pay Gap: ₦{pay_gap:,.2f} ({pay_gap_percent:.2f}% difference)")
```

- Simulates gender data.
- Calculates average salaries by gender.
- Computes absolute and percentage pay gap.
- Reveals gender-based salary disparities.

---

### 14. Salary Category Distribution

```python
low_thresh = 300000
high_thresh = 600000

salary_categories = np.where(salary < low_thresh, 'Low',
                     np.where(salary <= high_thresh, 'Mid', 'High'))

unique, counts = np.unique(salary_categories, return_counts=True)

print("\nSalary Category Distribution:")
for cat, count in zip(unique, counts):
    print(f"{cat}: {count} jobs")
```

- Defines salary thresholds to classify jobs into Low, Mid, and High salary categories.
- Counts how many jobs fall into each category.
- Summarizes salary distribution in clear discrete groups.

---

## Summary

This project demonstrates how **NumPy** can be used for generating synthetic datasets and performing exploratory data analysis on tech jobs salaries in Nigeria. It offers insights into salary trends by job role, experience, location, employment type, and gender — providing valuable knowledge for HR, recruiters, and professionals in the tech sector.

---

