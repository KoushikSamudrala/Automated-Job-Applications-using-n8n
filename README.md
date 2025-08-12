# Automated-Job-Applications-using-n8n
An independent project for automating the tedious process of Job applications with interactive user interface of n8n.

 The workflow includes:
   - A schedule trigger that runs daily at 9 AM.
   - An HTTP request to LinkedIn to fetch job postings.
   - HTML extraction to parse job details (title, company, location, applyUrl, datePosted).
   - Splitting the array of jobs into individual items.
   - For each job, making an HTTP request to the job URL to get the full description.
   - Extracting the job description from the HTML.
   - Using Google Gemini to generate a cover letter based on the job description and the candidate's resume.
   - Setting the generated cover letter in the workflow data.
   - Splitting out the cover letter for individual processing.
   - Appending or updating rows in a Google Sheet (with two separate Google Sheet nodes).


# Job Applications Automation System

[![n8n](https://img.shields.io/badge/n8n-%23000000.svg?logo=n8n&logoColor=white)](https://n8n.io/)
[![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?logo=google-sheets&logoColor=white)](https://www.google.com/sheets/about/)
[![Gemini](https://img.shields.io/badge/Google_Gemini-4285F4?logo=google&logoColor=white)](https://gemini.google.com/)

Automate your job application process with AI-powered cover letter generation and Google Sheets integration. This n8n workflow fetches computer vision engineering jobs from LinkedIn, generates personalized cover letters using Google Gemini, and tracks applications in a Google Sheet.

## Features

- ⏰ **Scheduled Execution**: Runs daily at 9 AM
- 🔍 **LinkedIn Job Scraping**: Fetches latest job postings
- ✍️ **AI Cover Letters**: Generates tailored cover letters using Google Gemini
- 📊 **Google Sheets Integration**: Tracks applications and cover letters
- 🔄 **Smart Deduplication**: Prevents duplicate applications

## Prerequisites

1. [n8n account](https://n8n.io/) (Cloud or self-hosted)
2. [Google Cloud account](https://cloud.google.com/) with:
   - Gemini API enabled
   - Google Sheets API enabled
3. Google Sheet for tracking (template provided below)
4. LinkedIn account (for job search)

### Setup:  

a. Setting up n8n (local or cloud).

b. Creating a Google Cloud project and enabling the Google Sheets API and Google Gemini API.

c. Creating service account credentials and sharing the Google Sheet with the service account email.

d. Setting up the Google Sheet with the required columns.

e. Setting up LinkedIn credentials (if required, note that the workflow uses HTTP request without authentication? But the node has credentials for httpHeaderAuth).


## Setup Instructions

### 1. Google Cloud Setup
- Enable **Google Sheets API** and **Gemini API**
- Create service account credentials (JSON format)
- Share your Google Sheet with the service account email

### 2. Google Sheet Preparation
Create a Google Sheet with these columns:

| Title | Company | Location | Apply URL | Date Posted | Cover Letter |


 
### 3. Workflow Import
1. In n8n, go to Workflows → Import

2. Upload job_applications_automation.json

3. Update credentials for:

    -Google Sheets

    -Google Gemini API

    -LinkedIn HTTP Request
 ### 5. Configuring Nodes:
  a. Schedule Trigger: Explain the schedule.
    
  b. HTTP Request for LinkedIn: Explain the URL and any parameters. Note that the current URL in the node might need updating (it has two `start` parameters). Also, note the authentication method (httpHeaderAuth) and how to set it up.
  
  c. HTML Extraction: Explain the selectors used.
  
  d. Google Sheets Nodes: Explain the two append/update nodes and the get node. How to set the document ID and sheet name. Also, how to map the fields.
  
  e. Google Gemini Node: Explain the model and the prompt. How to set the credentials.
  
  f. Other nodes: Set, SplitOut, etc.

### 6. Configure Job Search:
```
https://www.linkedin.com/jobs-guest/jobs/api/seeMoreJobPostings/search
?keywords=Computer%20Vision%20Engineer
&location=Germany
&start=0
```

### Workflow Overview
![alt text](http://url/to/img.png)


