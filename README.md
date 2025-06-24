MIAW Setup Guide
Setting Up Messaging for In-App and Web (MIAW)

1. Enable Messaging Settings
From Setup, enable Messaging Settings and assign the Service Cloud license to the agent.

2. Create and Assign Permission Set
Create a new Permission Set.
Go to App Permissions and enable Messaging for In-App and Web.
Assign this permission set to the agent.

3. Set Up Omni-Channel
Configure Omni-Channel to manage agent availability and routing.

4. Create a Messaging Channel
•From Setup, create a new Messaging Channel.
•Set Routing Type to Omni-Flow, and select the MIAW-Omni Flow (explained in the Flows section below).
•Activate the Messaging Channel.

5. Create an Embedded Service Deployment
•Choose MIAW as the channel type.
•Enter your domain name as the URL (e.g., [your-scratch-org].c.scratch.vf.force.com if testing on Visualforce).
•Select the Messaging Channel created in the previous step.

6. Add Enhanced Conversation Component
On the Messaging Session record detail page, add the Enhanced Conversation component.

7. Update Trusted URLs
Make sure all trusted URLs are updated and reflect your deployment environment.

Flows
1. MIAW-Omni Flow

This flow checks agent availability and routes conversations accordingly.

Use the Check Availability for Routing standard flow component to check if agents are available.
Add a Decision Element to branch logic based on agent availability.
If agents are online (Alpha path):
Use Update Record to link the Messaging Session ID.
Pass pre-chat information using custom variables.
Use Create Record to create a Case.
Use Assignment to store the Case in a variable.
Use another Update Record to map pre-chat data to the Messaging Session.
Use Route Work to assign it to the Alpha bot.
If agents are offline (Beta path):
Similar steps as above: update Messaging Session ID and variables.
Use Route Work to assign the session to the Beta bot.
2. MIAW-Outbound Flow

Handles routing from the Alpha Bot to a live agent when agents are online.

Eisenstein Bots
Two bots are required to manage different outcomes from the MIAW-Omni Flow:

Alpha Bot
Engages customers when agents are available.
Uses the outbound Omni-Flow to route chats to agents.
Can be customized to handle queries as per business needs.
Beta Bot
Informs users when agents are offline.
Prompts the customer to create a case.
If the customer agrees, the bot creates a Case using pre-chat info and responds with the Case ID.
