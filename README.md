# Course_Scraper
Course Scraper for Indian Colleges
Introduction
This document explains the Python script used to scrape the list of courses offered by different colleges in India. The script takes either the name of the college or the URL of the college's course page as input and returns a list of all courses offered by that college.
Requirements
The script requires the following Python libraries:
•	1. requests
•	2. beautifulsoup4
Installation
Install the required libraries using pip:
pip install requests beautifulsoup4
Script Explanation
The script consists of a function named `get_courses` that takes the URL of the college's course page as an input and returns a list of courses offered by the college.
Code

import requests
from bs4 import BeautifulSoup

def get_courses(college_url):
    try:
        headers = {'User-Agent': 'Mozilla/5.0'}
        response = requests.get(college_url, headers=headers)
        
        if response.status_code != 200:
            raise Exception(f"Failed to fetch the page. Status code: {response.status_code}")
        
        soup = BeautifulSoup(response.text, 'html.parser')
        courses = [course.get_text(strip=True) for course in soup.find_all('li') if course.get_text(strip=True)]
        
        if not courses:
            print("No courses found on the page.")
        return courses

    except Exception as e:
        print(f"An error occurred: {e}")
        return []

# Example usage
college_url = "https://www.ststephens.edu/courses/"  # Replace with the actual course page URL
courses = get_courses(college_url)

if courses:
    print("Courses offered:")
    for i, course in enumerate(courses, start=1):
        print(f"{i}. {course}")
    else:
        print("No courses found or an error occurred.")
    
Example Usage
To run the script, copy the code into a Python file (e.g., `course_scraper.py`) and run it from the command line or an IDE.
Command to run the script:
python course_scraper.py
Output
The script will output a list of courses offered by the college. The output will be printed in the console.
Example output:

Courses offered:
1. Bachelor of Arts (Honours) in English
2. Bachelor of Arts (Honours) in History
3. Bachelor of Science (Honours) in Physics
4. ...and so on.

Conclusion
This script is a simple yet effective tool for scraping course information from college websites. It can be adapted to work with different websites by adjusting the HTML parsing logic.
 

