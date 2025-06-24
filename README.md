<h1>MIAW Setup Guide</h1>

<h2>Setting Up Messaging for In-App and Web (MIAW)</h2>

1. Enable Messaging Settings
• From Setup, enable Messaging Settings and assign the Service Cloud license to the agent.

2. Create and Assign Permission Set
• Create a new Permission Set.
• Go to App Permissions and enable Messaging for In-App and Web.
• Assign this permission set to the agent.

3. Set Up Omni-Channel
• Configure Omni-Channel to manage agent availability and routing.

4. Create a Messaging Channel
•From Setup, create a new Messaging Channel.
•Set Routing Type to Omni-Flow, and select the MIAW-Omni Flow (explained in the Flows section below).
•Activate the Messaging Channel.

5. Create an Embedded Service Deployment
• Choose MIAW as the channel type.
• Enter your domain name as the URL (e.g., [your-scratch-org].c.scratch.vf.force.com if testing on Visualforce).
• Select the Messaging Channel created in the previous step.

6. Add Enhanced Conversation Component
• On the Messaging Session record detail page, add the Enhanced Conversation component.

7. Update Trusted URLs
• Make sure all trusted URLs are updated and reflect your deployment environment.

<h2>Flows</h2>

**Go throgh the metadata file for reference of the flow.**

**1. MIAW-Omni Flow**

This flow checks agent availability and routes conversations accordingly.


<img width="959" alt="MIAW Omni" src="https://github.com/user-attachments/assets/8822d7a1-0b81-4ae1-a279-f0a52eb6e59f" />


• Use the Check Availability for Routing standard flow component to check if agents are available.

• Add a Decision Element to branch logic based on agent availability.


---**If agents are online:**
   
   • Use Update Record to link the Messaging Session ID.
   
   • Pass pre-chat information using custom variables.
   
   • Use Create Record to create a Case.
   
   • Use Assignment to store the Case in a variable.
   
   • Use another Update Record to map pre-chat data to the Messaging Session.
   
   • Use Route Work to assign it to the Alpha bot.


---**If agents are offline:**

   • Similar steps as above: update Messaging Session ID and variables.
   
   • Use Route Work to assign the session to the Beta bot.
   


**2. MIAW-Outbound Flow**

Handles routing from the Alpha Bot to a live agent when agents are online.


<img width="959" alt="MIAW Outbound" src="https://github.com/user-attachments/assets/58c9ad56-62aa-4b17-9e0d-87e4f79c53e9" />



<h2>Eisenstein Bots</h2> 

**1. Alpha Bot**


• Engages customers when agents are available.

• Uses the outbound Omni-Flow to route chats to agents.

• Can be customized to handle queries as per business needs.


<img width="957" alt="Alpha" src="https://github.com/user-attachments/assets/246c29ce-11d1-4204-a806-4ebfa2c0efb3" />



**2. Beta Bot**

• Informs users when agents are offline.

• Prompts the customer to create a case.

• If the customer agrees, the bot creates a Case using pre-chat info and responds with the Case ID.


<img width="959" alt="Beta" src="https://github.com/user-attachments/assets/35939099-b592-44e5-a7a6-8fe771fad4ea" />


Reference articles which wold help to create these bots: 

[Article 1](https://help.salesforce.com/s/articleView?id=service.bots_service_create.htm&type=5)

[Article 2](https://help.salesforce.com/s/articleView?id=service.bots_service_setup_dialog_action.htm&type=5)

[Trailhead 1](https://trailhead.salesforce.com/content/learn/modules/einstein-bots-project-planning/build-and-implement-your-bot)

[Traihead 2](https://trailhead.salesforce.com/content/learn/modules/service_bots_basics)



