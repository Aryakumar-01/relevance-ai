# relevance-ai
Important insights:
- to scrape content, "Extract Webpage Content" tool performs best
- to add knowledge base,go to knowledge>add file>>in main prompt type "{{" and select  required knowledge base from drop down.
- <img width="925" height="710" alt="image" src="https://github.com/user-attachments/assets/7f05cafc-21a7-49fb-8cdc-f58459e7e6c8" />
- for performing googlee search,use"Perform Google Search" tool.
- to post wordpress draft use this code:
```plaintext
import requests
from requests.auth import HTTPBasicAuth
import urllib3
import markdown

# Disable warnings about unverified HTTPS requests (for development only)
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Configuration for a self-hosted WordPress site:
ROOT_URL = "endzoneleadership.com"  # Your site's domain (without protocol)
USER = "Quantaltech"            # Your WordPress username
PASSWORD = "ARYA KU1F LEej Aw78 fjgL omNM"  # Your Application Password

# Define headers for the POST request
headers = {
    "Content-Type": "application/x-www-form-urlencoded",
}

def get_blog_list():
    # Endpoint for retrieving posts from a self-hosted WordPress REST API
    url = f"https://{ROOT_URL}/wp-json/wp/v2/posts"
    response = requests.get(url, headers=headers, auth=HTTPBasicAuth(USER, PASSWORD), verify=False)
    if response.status_code == 200:
        all_blogs = response.json()
        pages = [blog["title"]["rendered"] for blog in all_blogs]
        return pages
    else:
        return ("Error:", response.status_code, "Response content:", response.text)

def create_blog(title, content):
    # Data for the new post
    html_content = markdown.markdown(content)
    data = {
        "title": title,
        "content": html_content,
        "status": "draft",  # Change to "publish" if you want to publish immediately
    }
    # Endpoint for creating posts on a self-hosted site
    url = f"https://{ROOT_URL}/wp-json/wp/v2/posts"
    response = requests.post(url, data=data, headers=headers, auth=HTTPBasicAuth(USER, PASSWORD), verify=False)
    if response.status_code == 201:
        new_post = response.json()
        return f"New post ID: {new_post['id']} title: {title}"
    else:
        return ("Error:", response.status_code, "Response content:", response.text)


if ROOT_URL == "yourdomain":
    print("Please edit Wordpress toolkit, and change the url & authorization_token to your own wordpress credential first")
else:
    if params["options"] == "list all existing blogs":
        articles = get_blog_list()
        print(articles)
    elif params["options"] == "create new blog":
        create_result = create_blog(params["title"], params["content"])
        print(create_result)

  
```

  - ### if we wanna give/add additonal  input and want i should fill those concidering the response obtained from past tool(eg:Hubspot API Call)
  - then step 1:add inputs on going to that tool by >select congiure>select any of input type(eg text,json,etc..)>
  - <img width="1031" height="60" alt="image" src="https://github.com/user-attachments/assets/0510bd46-c113-40a5-8089-8db8b17f77ee" />
  - <img width="1102" height="240" alt="image" src="https://github.com/user-attachments/assets/019d9958-d67c-4900-8f87-65e34a795af4" />
   for safer side also remind ageent tin main prompt.
### Integrating to 3rd party service(eg hubspot,linkedin,etc...)
- normally on such problem statements we counter problems with API request.
- go to that party's api services for our expectation with that service,
- obtain credential if required
- add python IDE,& copy-paste python code for respective(get,post,etc..)api request,


