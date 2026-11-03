# AI-assisted job-search automation

Ten numbered n8n workflows, plus one master workflow that runs them every morning. They find jobs, filter and score them against a profile, track them in Notion, and prepare a tailored CV, cover letter and interview notes with Claude.

**Live demo with invented data:** https://YOUR-USER.github.io/job-search-automation/

## How it works
1. **Find jobs:** TheirStack search and LinkedIn alert emails (Gmail).
2. **Filter:** English postings only, location rule, no US work-authorization requirements, company size.
3. **Pre-score:** title, skills, location, language and seniority.
4. **Jobs or Trash Jobs:** strong matches go to Jobs. Weak or incomplete ones wait in Trash Jobs. A nightly workflow moves the ones I rescue back to Jobs.
5. **Claude verdict:** Apply, Reach out first or Skip, with the employer's likely problems.
6. **Application materials:** tailored CV, cover letter and notes in Google Docs, in a dated Drive folder.
7. **Outreach drafts** for contacts and hiring managers, and a **morning briefing** by email.

## Workflows
| File | What it does |
|---|---|
| Job Search_ Daily Run | Master workflow. Runs the others in order at 06:00 |
| 1 Fetch Jobs | TheirStack search, language and quick-score filters, saves new jobs |
| 7 LinkedIn Alerts | Reads alert emails, filters, saves jobs or sends them to Trash Jobs |
| 2 Match Contacts | Links my contacts to jobs by company |
| 3 Score Jobs | Pre-score out of 100 |
| 4 Claude Verdict | Claude reads the posting and gives a verdict |
| 6 Outreach | Drafts LinkedIn messages |
| 5 Application Materials | CV, cover letter and notes from templates |
| 8 Morning Briefing | Daily summary email |
| 9 Error Alert | Emails me when a workflow fails |
| 10 Rescue Trash | Nightly at 23:00, moves rescued Trash jobs to Jobs |

## Built with
n8n Cloud, Claude API, Notion, Gmail, Google Drive and Docs, TheirStack.

## Set up
1. Create the Notion databases: Jobs, Companies, Contacts, Professional Profile, Application Materials, Outreach Log and Trash Jobs.
2. Import each file from `workflows/` into n8n.
3. Replace every `YOUR_...` placeholder with your own ID: database IDs, Drive folder and template IDs, workflow IDs in the master workflow, and the email addresses.
4. Add your own credentials in n8n (Notion, Gmail, Google Drive, Google Docs, TheirStack, Anthropic). No keys are stored in this repo.
5. In workflow 4, replace the sample text in `PROFILE` with your own profile.
6. Set the Error Workflow in each workflow's settings to workflow 9.

## Rules built in
Berlin: any work mode. Elsewhere: remote only. Jobs asking for US work authorization are dropped. Companies under 50 employees go to Trash Jobs for review.
