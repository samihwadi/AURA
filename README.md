# AURA - Automated Job Application Workflow

**Automated Unified Recruiting Agent (AURA)** is an n8n workflow designed to automate the process of discovering, evaluating, and tracking job postings. It streamlines the entire workflow from job extraction to tailored resume and cover letter generation, and finally logs the results in Google Sheets.

---

## Features

- **Job Extraction**
  - Scrapes job postings from LinkedIn using Apify actors.
  - Limits the number of extracted jobs per run (configurable).

- **Job Evaluation**
  - Uses Groq’s AI API (LLaMA 3.1) to evaluate how well your profile matches each job.
  - Produces a match score (0–100) for each job.

- **Filtering**
  - Only considers jobs with a match score ≥ 70%.
  - Ensures you focus on high-potential opportunities.

- **Resume & Cover Letter Tailoring**
  - Generates personalized resumes and cover letters for each job using your real experience.
  - Ensures that all placeholders are filled with job-specific details.

- **Job Tracking**
  - Checks Google Sheets to see if a job has already been added.
  - If new, appends the job along with tailored documents to the sheet.
  - Maintains a record of all applications for better tracking.

- **Automation**
  - Runs on a scheduled trigger (e.g., daily at 6 AM) or manually via a trigger node.
  - Fully automated, requiring minimal manual intervention.

---

## Workflow Nodes

1. **Schedule / Manual Trigger** – Start the workflow automatically or on demand.  
2. **Extract Job Postings** – Scrapes jobs from LinkedIn.  
3. **Limit** – Optional batch limiter for extracted jobs.  
4. **Filter and Rate Jobs** – Sends job descriptions and your resume to AI for match scoring.  
5. **Sanitise** – Cleans AI responses for safe parsing.  
6. **>=70% Filter** – Only passes jobs with a match score of 70% or higher.  
7. **Check Job IDs** – Checks Google Sheets for existing job entries.  
8. **If Job not in Sheet** – Branches workflow if the job is new.  
9. **Find Full Job Info** – Retrieves detailed job info.  
10. **Tailor Resume and Cover** – Generates personalized resume and cover letter.  
11. **Merge and Prep** – Prepares the final data for Google Sheets.  
12. **Append Row in Sheet** – Adds new jobs to Google Sheets for tracking.

---

## Requirements

- **n8n** instance (self-hosted or cloud)  
- **Groq API credentials** for AI-based job evaluation and document tailoring  
- **Apify account** to run job scraping actors  
- **Google Sheets OAuth2 credentials** for logging job data  
- Basic knowledge of n8n workflows

---

## Prerequisites

Before running the workflow, prepare a Google Sheets document with the following **minimum required columns** (additional columns may be added as desired):

| Column Name          | Purpose |
|----------------------|------------------------------------------------|
| **Job ID**           | Used to prevent duplicate entries in the sheet |
| **Company**          | Stores the company name for the job posting    |
| **Job Title**        | Stores the job title associated with the posting |
| **URL**              | Direct link to the job posting                 |
| **Tailored Resume**  | Link or reference to the generated tailored resume |
| **Tailored Cover Letter** | Link or reference to the generated tailored cover letter |

> ⚠️ Note: Do not change the column names after connecting the sheet to the workflow, as it may break the automation.

---

## Security

- No API keys or secrets are stored directly in the workflow JSON.  
- All credentials are referenced by n8n credential IDs, keeping sensitive data secure.  
- Users must configure their own credentials within n8n to run the workflow.

---

## Usage

1. Import `AURA.json` into your n8n instance.  
2. Configure credentials:
   - Google Sheets OAuth2
   - Groq API
   - HTTP Header Auth (if required by your scraping actors)
3. Set the workflow schedule or trigger manually.  
4. Watch as AURA automatically extracts, evaluates, and tracks job postings.  

---

## Tips & Recommendations

For an even more efficient job search and application process, combining AURA with tools like the **SpeedyApply browser extension** can significantly speed up your workflow. This setup has been personally effective in automating job discovery, evaluation, and application submission, reducing repetitive tasks and saving time.


## License

This workflow is open-source. Feel free to adapt it to your own job search automation needs.
