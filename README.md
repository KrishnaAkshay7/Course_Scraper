import requests
from bs4 import BeautifulSoup

def get_courses(college_url):
    try:
        # Set headers to mimic a browser visit
        headers = {'User-Agent': 'Mozilla/5.0'}
        
        # Send a request to the college course page
        response = requests.get(college_url, headers=headers)
        
        # Check if the request was successful
        if response.status_code != 200:
            raise Exception(f"Failed to fetch the page. Status code: {response.status_code}")
        
        # Parse the HTML content using BeautifulSoup
        soup = BeautifulSoup(response.text, 'html.parser')
        
        # Extract courses (this part may vary depending on the actual structure of the website)
        # Example assumes courses are listed in <li> elements within a <ul> with a specific class
        courses = []
        for course in soup.find_all('li'):  # Adjust 'li' to match the actual HTML structure
            course_name = course.get_text(strip=True)
            if course_name:  # Only add non-empty course names
                courses.append(course_name)
        
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
