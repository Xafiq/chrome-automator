lets create a command called "followup-next.py --list=4ga-list " that when called fetches the following API endpoint:

GET  @https://brevo-webhook.replit.app/api/followups/4ga-lost?status=PENDING 

Retrieves the first contact from that list and tries to send a follow-up using the agent automation. The process is as follows:

1. **Fetch Pending Contacts:**  
   The script calls the API endpoint to get all contacts with status `PENDING` for the specified list (e.g., `4ga-lost`).

2. **Process the First Contact:**  
   - If a contact is found, it checks for required fields (like phone number).
   - It loads the YAML configuration for the list, which defines the agent’s name and tasks.
   - It processes the tasks, replacing template variables with contact data and message templates.

3. **Run the Agent:**  
   - The agent executes the tasks (such as sending a message or performing browser automation).
   - The agent’s completion handler updates the contact’s status to `COMPLETE`, `INCOMPLETE`, or `ERROR` based on the outcome.

4. **Update Contact Status:**  
   - The contact’s status and a message are updated via a PUT request to the API.

5. **Wait and Repeat:**  
   - The script waits a random interval (3–6 minutes) before processing the next contact.

**Command Example:**
```bash
python src/followup-next.py --list=4ga-lost
```

**Requirements:**
- The list configuration YAML must exist in `src/followup-list/`.
- The API endpoints must be accessible.
- Required Python packages: `requests`, `pyyaml`, `python-dotenv`.