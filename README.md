# Writeback Testing Guide for Retell Bot QA

This guide outlines the process for testing writebacks after creating a bot in Retell.

## Prerequisites

Before starting, ensure you have:
- Access to the agency admin portal
- Test candidate credentials provided by the agency
- A configured Retell bot ID (you can get it from lowcoder)
- Required API credentials and endpoint access

## Step 1: Trigger the Voice Bot API

Execute the following API request to initiate the voice bot trigger:

```bash
curl --location 'https://<agency_name>.sensehq.com/api/v1/voice-bot/trigger' \
--header 'accept: application/json' \
--header 'sec-ch-ua-platform: "macOS"' \
--header 'sec-fetch-dest: empty' \
--header 'sec-fetch-mode: cors' \
--header 'sec-fetch-site: same-origin' \
--header 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36' \
--header 'x-api-key: <ask>' \
--header 'Content-Type: application/json' \
--header 'Cookie: sosense=b6bd0a78-4797-4a4e-8185-e82b8eada601; sosense-agency-location=multientity.sensehq.com; sosense=b6bd0a78-4797-4a4e-8185-e82b8eada601; sosense-agency-location=multientity.sensehq.com; sosense=b6bd0a78-4797-4a4e-8185-e82b8eada601; sosense-agency-location=multientity.sensehq.com' \
--data '{
    "agency_id": "3384364471276985052",
    "is_debug": false,
    "from_number": "+16056675826",
    "to_number": "+16282224591",
    "prompt_replacements": {
        "Candidate/Full_Name": "N P Pragashri",
        "Candidate/First_Name": "Pragashri",
        "Candidate/Discipline": "RN",
        "Candidate/Specialities": "Nurse",
        "Job_Submission/Candidate/First_Name": "Madhu",
        "Job_Submission/Candidate/Full_Name": "Madhu Babu",
        "Job_Submission/JobOrder/Title": "2nd Shift Assembly Technician",
        "Job_submission/JobOrder/State": "Virginia",
        "Job_submission/JobOrder/City": "Richmond",
        "Job_Submission/JobOrder/Worksite_Option": "Charlton,MA",
        "Job_Submission/JobOrder/Description": "<body><table border=0 cellspacing=2 style=font-size:12pt;font-family:Arial><tr><td><p>CoWorx Staffing is seeking an Assembly Technician on 2nd shift for our client located in the Charlton, MA area.[br] The Assembly Technician performs a variety of manual tasks to assemble complex fiber components into draw units that support our precision manufacturing processes.[br] Schedule: Monday – Friday, 2:00PM 10:30PM **requires training on either 1st or 2nd shift</p></td></tr><tr><td><p><b>Responsibilities:</b></p><p>[ul] [li]Assemble small and delicate components with precision to meet quality and customer requirements[/li] [li]Work with engineering teams on special product and project builds[/li] [li]Select appropriate materials, tools, and instructions needed for each assembly[/li] [li]Complete all necessary steps in the assembly process to ensure high-quality output[/li] [li]Accurately document production information and maintain records[/li] [li]Follow all safety procedures and use proper protective equipment[/li] [li]Read and interpret routing sheets and process documentation[/li] [li]Perform other related tasks as assigned[/li] [/ul]</p></td></tr><tr><td><p><b>Desired Background/Skills:</b></p><p>[ul] [li]High school diploma or equivalent education required[/li] [li]Demonstrated history of consistent employment and dependability[/li] [li]Previous experience in assembly within a manufacturing setting is a plus[/li] [li]Comfortable handling small and delicate parts[/li] [li]Capable of following detailed instructions to assemble complex products[/li] [li]Experience with microscopes or precision inspection instruments is beneficial[/li] [li]Proficient in English (speaking, reading, writing, and comprehension) to effectively carry out job responsibilities[/li] [li]Excellent hand-eye coordination, fine motor skills, and strong visual accuracy[/li] [li]Must be able to lift, carry, and transport items weighing up to 50 pounds[/li] [li]Dependable transportation to and from work is essential[/li] [/ul]</p></td></tr><tr><td><p><b>Other Information:</b></p><p>Don't miss out on this excellent opportunity to join a hardworking, supportive team - apply with us today to get started![br] CoWorx is an equal opportunity employer dedicated to fostering a diverse and inclusive team. We believe that a varied workforce enhances our business outcomes and contributes to a brighter future for our internal teams, Field Talent, customers, and communities. We are committed to considering all qualified applicants without regard to race, color, religion, sex, sexual orientation, gender identity, age, national origin, or veteran status, and we do not discriminate based on disability.[br] If you are a person with a disability and require assistance during the recruitment process, please reach out to us.</p></td></tr><tr><td><p>Interested candidates please reference job code 232901 when responding to this ad.</p></td></tr></table></body>,offered pay rate: 30$ per"
    },
    "anchor_entity_id": "9a255b3a-dcf2-442f-8070-0db6c6e8522b",
    "anchor_entity_type": "bh_job_submission",
    "recipient_entity_id": "f088ac64-eaa9-49f0-a916-0701fa009500",
    "recipient_entity_type": "bh_candidate",
    "service_provider": "retell",
    "retell_bot_id": "11957767906079068398",
    "workflow_name": "Madhu - Test - NEW1",
    "node_name": "#A0",
    "consent_type": "Implied Consent",
    "max_concurrency_limit": "10",
    "recipient_name": "",
    "metadata": {
        "workflow_id": "4243",
        "task_group_id": "9431",
        "secondary_entity_id": "",
        "automation_tracking_id": "4243__9a255b3a-dcf2-442f-8070-0db6c6e8522b__0__0",
        "state_machine_id": "586684",
        "state_machine_audit_id": "2051313",
        "source": "automation",
        "entity_id": "9a255b3a-dcf2-442f-8070-0db6c6e8522b",
        "swimlane_id": "4239",
        "node_type": "task",
        "entity_type": "bh_candidate",
        "recipient_entity_type": "bh_candidate",
        "secondary_entity_type": "",
        "recipient_entity_id": "f088ac64-eaa9-49f0-a916-0701fa009500",
        "node_id": "task:8664",
        "utm_source": "sense_workflows"
    }
}'
```

### Important Configuration Notes

Replace the following values with your agency-specific information:
- `agency_id`: Your agency identifier (change from multientity to your agency name)
- `to_number`: Your test phone number
- `prompt_replacements`: Update with appropriate candidate and job submission data
- `anchor_entity_id`: Your specific entity ID
- `anchor_entity_type`: The entity type of the anchor entity (e.g., `bh_candidate`, `bh_job_submission`, etc. - check the bot's initial ticket to determine the correct entity type)
- `recipient_entity_id`: Your recipient entity ID
- `recipient_entity_type`: The entity type of the recipient entity (e.g., `bh_candidate`, `bh_job_submission`, etc. - check the bot's initial ticket to determine the correct entity type)
- `retell_bot_id`: Your configured bot ID in Retell

## Step 2: Obtain the Recipient Entity ID

To find the recipient entity ID for your test candidate:

1. Log into your agency admin portal
2. Navigate to All Records
3. Locate and click on the test candidate provided by the agency
4. Copy the entity ID from the URL path following `/candidates/`

![Finding recipient entity ID in URL](https://github.com/user-attachments/assets/a55b7091-beaa-4f5d-b439-daeead01e9ad)

### Determining Entity IDs Based on Entity Type

For candidate entities, both `anchor_entity_id` and `recipient_entity_id` will be the same value. For other entity types such as job submissions, check the associated entity section to determine the correct entity IDs.

![Associated entity reference](https://github.com/user-attachments/assets/1f39d3eb-8118-4ccf-aef5-0947d1b79dca)

## Step 3: Execute the API Call

After configuring all parameters with your agency-specific data, execute the API request. You will receive an incoming call on Zoom. Answer this call to proceed with testing.

## Step 4: Review Conversation Transcript

Once the call completes:

1. Navigate to the conversation transcript
2. Locate the Tool Calls section
3. Find and copy the ID listed under the tools object

## Step 5: Verify Writeback Success

1. Log into the admin portal
2. Navigate to OWB History
3. Paste the tool call ID into the Writeback ID field

![OWB History verification interface](https://github.com/user-attachments/assets/c641fa94-2abb-4189-a161-bdd9b4b23df1)

4. Check the Status column for your entry
5. If the status shows "Succeeded", the writeback is functioning correctly

## Troubleshooting

If the writeback status shows anything other than "Succeeded", review the following:
- Verify all entity IDs are correct and match the actual entities in your system
- Confirm that the API key and authentication credentials are valid
- Check that the prompt replacements contain the appropriate data
- Ensure the Retell bot is properly configured and deployed
- Review API response logs for any error messages or issues
