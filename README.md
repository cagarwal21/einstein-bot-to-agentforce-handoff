# The Seamless Handoff: Integrating Einstein Enhanced Bot with Agentforce Agent

This repository documents the strategic fusion of **Einstein Bot's** rule-based triage with **Agentforce AI's** adaptive intelligence. The "Hybrid Bot" solution ensures high-volume inquiries are handled efficiently while complex issues are resolved by an autonomous agent with deep context.

## Overview

**The Problem:** Achieving unified, intelligent customer service that balances efficiency with personalized resolution.

**The Solution:**
1.  **Einstein Bot Classic:** Streamlines high-frequency inquiries (e.g., Log Case, Status Check).
2.  **Agentforce Agent:** Handles specialized knowledge-based questions and complex multi-step actions using LLMs.

### Architecture
The architecture routes user input through an Inbound Omni-Channel Flow to the Einstein Bot. Simple requests are handled via Flow/Apex, while complex queries are transferred via an Outbound Omni-Channel Flow to the Agentforce Agent.

![Hybrid Bot Architecture](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image1.png)
*Figure 1: Hybrid Bot Architecture showing the flow between Einstein Bot and Agentforce Agent.*

---

## Configuration Guide

### Step 1: Configure Agentforce Service Agent

1.  **Create Data Library:** Create an Agentforce Data Library, set the Data Type to 'file', and upload support policy/FAQ PDF documents.

![Agentforce Data Library Setup](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image2.png)
*Figure 2: Configuring the Agentforce Data Library.*

2.  **Create Agent:** Create a "Unified Resolution Agent".
3.  **Configure Agent:** Add the Data Library, define Topics/Instructions, and assign the 'Answer Questions with Knowledge' action.

![Agentforce Builder Testing](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image3.png)
*Figure 3: Testing the Agentforce Agent's ability to retrieve warranty policy from the library.*

### Step 2: Configure Einstein Enhanced Bot ("Astro Case Resolution")

Create a new Enhanced Bot named **Astro Case Resolution**.

**1. Case Status Dialog:**
* Add a question to get the user's email.
* Add an Action to run the "Get Case Details" flow.
* Add a Message component to display the status.

![Case Status Dialog](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image4.png)
*Figure 4: Case Status Dialog Configuration.*

**2. Log a Case Dialog:**
* Collect Email and Problem Statement via Question components.
* Call the "Create a case flow".
* Display the generated Case Number.

![Log a Case Dialog](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image5.png)
*Figure 5: Log a Case Dialog Configuration.*

**3. Talk to an Expert Dialog:**
* Set the Next Step to "Transfer to Agent".

![Talk to an Expert Dialog](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image6.png)
*Figure 6: Talk to an Expert Dialog Configuration.*

### Step 3: Configure Omni-Channel Routing

To enable the handoff, you must configure the Omni-Channel flow.

1.  **Create Queue:** Create a queue (e.g., "GPO Fallback") and add the Agentforce Service Agent user to it.
2.  **Create Omni-Channel Flow:** Create a "Route Work" step that routes to the **Agentforce Service Agent**.

![Omni-Channel Flow](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image7.png)
*Figure 7: Omni-Channel flow transferring chat to Unified Resolution Agent.*

3.  **Bot Overview Settings:** In the Einstein Bot Overview, set the **Outbound Omni-Channel Flow** to the flow created above.

![Bot Overview Settings](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image8.png)
*Figure 8: Setting the Outbound Omni-Channel flow.*

4.  **Transfer Dialog Rules:** In the "Transfer To Agent" dialog, add a Rule Action to set the Route Destination to the "Route to Unified Resolution Agent" flow.

![Transfer To Agent Dialog](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image9.png)
*Figure 9: Configuring the Transfer To Agent dialog rules.*

### Step 4: Deploy to Experience Cloud

**1. Inbound Omni-Channel Flow:**
Ensure the system-generated Inbound Omni-Channel flow falls back to the "GPO Fallback" queue.

![Inbound Omni-Channel Flow](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image10.png)
*Figure 10: Inbound Omni-Channel flow configuration.*

Review the bot's overview to confirm the connection.

![Bot Overview Inbound Flow](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image11.png)
*Figure 11: Inbound Omni-Channel Flow verification.*

**2. Create Messaging Channel:**
In Setup, create a new **Enhanced Chat** channel (Messaging for In-App and Web). Set the routing type to "Omni-flow" pointing to the *Inbound* flow.

![Messaging Settings](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image12.png)
*Figure 12: Messaging for In-App and Web configuration.*

**3. Embedded Service Deployment:**
This is automatically created when defining the Messaging Channel.

![Embedded Service Deployment](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image13.png)
*Figure 13: Embedded Service Deployment Settings.*

**4. Experience Cloud Setup:**
Drag the **Embedded Messaging** component onto your Experience Cloud site and link it to the web deployment.

![Experience Cloud Component](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image14.png)
*Figure 14: Embedded Messaging component on the site.*

---

## Testing the Hybrid Bot

**Scenario A: Standard Transaction (Einstein Bot)**
The user initiates a chat and selects **Case Status**. The Einstein Bot collects the email and returns the status via the flow.

![Test: Menu Selection](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image15.png)
*Figure 15: User selecting Case Status from the menu.*

![Test: Case Status Result](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image16.png)
*Figure 16: Bot providing case number and status.*

**Scenario B: Complex Inquiry Handoff (Agentforce)**
The user selects **Talk to an expert**. The chat is transferred to the Unified Resolution Agent, which answers a warranty question using the knowledge base.

![Test: Agentforce Handoff](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image17.png)
*Figure 17: Conversation transferred from Astro Bot to Unified Resolution Agent.*

---

## Conclusion
This architecture allows companies to redefine service by achieving the efficiency of automation for routine tasks while guaranteeing sophisticated resolution for complex interactions.

### Authors
* **Chandan Agarwal**: Lead Member of Technical Staff at Salesforce.
* **Ishita Saxena**: Senior Solution Consultant at Salesforce.
