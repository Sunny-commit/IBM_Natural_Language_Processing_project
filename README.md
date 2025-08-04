# IBM_Natural_Language_Understanding_project
This is a Task in the AICTE Internship conducted by IBM cloud under the partnership of Edunet foundation .
IBM Watson Natural Language Understanding Script
This project contains a simple Python script to perform advanced text analysis on a publicly accessible URL using the IBM Watson Natural Language Understanding API.

The script demonstrates how to extract key insights from a webpage's content, including sentiment, categories, concepts, entities, and keywords. This is a powerful tool for quickly understanding the core themes and tone of any online article.

Key Features
Comprehensive Analysis: Extracts a variety of metadata, including sentiment, categories, concepts, entities, and keywords.

Python-based: A single, self-contained Python script that is easy to understand and modify.

API-Driven: Demonstrates the correct method for authenticating and sending requests to the IBM Watson API.

Configured for Windows: The instructions and example code are tailored for a Windows environment.

Prerequisites
To get started with this project, you will need:

An IBM Cloud Account: You must have an active Natural Language Understanding service instance.

Service Credentials: You'll need the API Key and the unique URL for your NLU service instance.

Python: Version 3.6 or newer.

requests library: Install it using pip: pip install requests.

How to Use
Clone this repository to your local machine:

Bash

git clone https://github.com/Sunny-commit/IBM_Text_To_Speak_Project.git
cd IBM_Text_To_Speak_Project
Update the script:
Open main.py in a text editor. Replace the placeholder values in the analyze_text function with your actual IBM Cloud credentials:

Python

# These are placeholders. Replace them with your actual values.
api_key = "YOUR_NLU_API_KEY"
url = "YOUR_NLU_URL"
Choose a URL to analyze:
The script is currently configured to analyze the IBM NLU product page. To analyze a different page, simply change the value of the document_url variable inside the script.

Run the script from your terminal:

Bash

python main.py
The script will print the complete JSON analysis directly to your console.

The Python Code
The core script is provided below. It is a more robust and readable version of the curl command that correctly handles the JSON data and authentication.

Python

import requests
import json

def analyze_text(api_key, url, document_url):
    """
    Analyzes a given URL using the IBM Watson Natural Language Understanding API.

    Args:
        api_key (str): Your IBM Watson API key.
        url (str): The IBM Watson NLU service URL.
        document_url (str): The URL of the webpage to be analyzed.
    """
    headers = {
        "Content-Type": "application/json"
    }
    
    # Define the features you want to extract from the document
    features = {
        "sentiment": {},
        "categories": {},
        "concepts": {},
        "entities": {},
        "keywords": {}
    }

    # The payload is a dictionary containing the URL to analyze and the features
    payload = {
        "url": document_url,
        "features": features
    }

    # The full URL for the API endpoint
    full_url = f"{url}/v1/analyze?version=2019-07-12"

    print(f"Analyzing content at: {document_url}...")

    try:
        # Send the POST request with Basic Authentication
        response = requests.post(
            full_url,
            headers=headers,
            json=payload,
            auth=requests.auth.HTTPBasicAuth('apikey', api_key)
        )
        response.raise_for_status()  # Raise an HTTPError for bad responses

        # Print the response in a nicely formatted JSON
        analysis_results = response.json()
        print(json.dumps(analysis_results, indent=2))

    except requests.exceptions.RequestException as e:
        print(f"An error occurred during the API call: {e}")
        if response is not None:
            print(f"Status Code: {response.status_code}")
            print(f"Response Body: {response.text}")

if __name__ == '__main__':
    # --- YOUR CREDENTIALS AND SETTINGS ---
    # Replace these placeholder values with your actual API key and URL.
    # Do not share these credentials publicly.
    api_key = "YOUR_NLU_API_KEY"
    url = "YOUR_NLU_URL"
    document_url = "https://www.ibm.com/products/natural-language-understanding"

    # --- RUN THE ANALYSIS ---
    analyze_text(api_key, url, document_url)
