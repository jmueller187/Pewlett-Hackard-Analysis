# Pewlett-Hackard-Analysis

## Analysis Overview:
The purpose of this analysis was to help the management team at Pewlett-Hackard prepare for the "Silver Tsunami", as a large portion of their workforce prepares to move towards retirement. We were able to provide data on the number of retiring employees in each division based on their title as well as identify employees who would be eligible to participate in the company's proposed mentorship program to help new employees transision successfully into their positions.

## Results:
1) The first table we created incorporated employee number, the employee's first amd last name, title amd employment start and end dates from two previously configured tables - Employees and Titles. This data was then filtered to retrieve employees born between 1952 and 1955 to show eligibile retirees by title, orderd by employee number. Retirees by Title (showing first ten entries):

![Retirement_Titles_Image](https://github.com/jmueller187/Pewlett-Hackard-Analysis/blob/main/Resources/Retirement_Titles_Image.png)

2) Because some employees had switched roles over the years of their employment the first table contained duplicate employee entries with multiple titles. The second table we  created eliminated the duplicate entires to show only the most recent title of each employee. Retirees by most recent title (showing first ten entries):

![Unique_Title_Image](https://github.com/jmueller187/Pewlett-Hackard-Analysis/blob/main/Resources/Unique_Titles_Image.png)

3) In order to provide management with a count of employees in the "Silver Tsunami", the third table we created showed the total number of employees ready to retire broken down by their job title. Total counts of retirees by title:

![Retiring_Titles_Image](https://github.com/jmueller187/Pewlett-Hackard-Analysis/blob/main/Resources/Retiring_Titles_Image.png)

4) The final table we created included the employees eligible for the company's proposed mentorship program. This program would be used by management to enlist those experienced and successfull retiring employees to work as a mentor to the incoming new hires on a part-time basis. Employees eligible for mentorship program (showing first ten entries):

![Mentorship_Eligibility_Image](https://github.com/jmueller187/Pewlett-Hackard-Analysis/blob/main/Resources/Mentorship_Eligibility_Image.png)


## Analysis Summary:

### How many roles will need to be filled as the "Silver Tsunami" begins to make an impact?
Our third summary showed that if all the eligible employees took their retirement, there would be a total of 90,398 positions that will need to be filled.

### Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
Our fourth summary showed us that a total of 1.549 employees would be eligible for the mentorship program. This is a significantly smaller number compared to the potential number of positions that may become available. If all eligible employees retire around the same time, this would result in about one mentor per 58 new hires coming into the company. One was to increase the number of mentors would be to adjust the range of employee birthdates to include a range from 1960 to 1965 as included in the following query:

SELECT DISTINCT ON (e.emp_no) e.emp_no,/n
	e.first_name,/n
	e.last_name,/n
	e.birth_date,/n
	de.from_date,/n
	de.to_date,/n
	t.title/n
INTO mentorship_eligibility_expanded
FROM employees AS e
INNER JOIN dept_emp AS de
ON (e.emp_no = de.emp_no)
INNER JOIN titles AS t
ON (e.emp_no = t.emp_no)
WHERE (de.to_date = '9999-01-01')
AND (e.birth_date BETWEEN '1960-01-01' AND '1965-12-31')
ORDER BY emp_no;

This would increase the number of potential mentors to over 117,000 people.
