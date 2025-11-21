# Hybrid Bot Solution: Einstein Bot + Agentforce Agent

A reference implementation for the **Hybrid Bot solution** on Salesforce. [cite_start]This project demonstrates how to integrate Einstein Enhanced Bots for high-volume triage with Agentforce Service Agents for adaptive, deep-context resolution[cite: 3, 6].

## Architecture
![Hybrid Bot Architecture](assets/architecture_diagram.png)

[cite_start]*Figure 1: The Hybrid Bot Architecture where Einstein Classic triages transactions and routes complex knowledge queries to an Agentforce Agent[cite: 21].*

## Let's Explore the Solution
Let’s explore how to implement this dual-strategy architecture using a real-world scenario. [cite_start]In this guide, we follow the use case of **QuantumConnect**, an organization aiming to achieve unified, intelligent customer service[cite: 9]. [cite_start]Their goal is to efficiently streamline high-frequency inquiries (like **Log Case** and **Status Check**) using an initial Einstein Bot, while ensuring that complex, knowledge-based questions are immediately handed off to a dedicated **Agentforce Agent**[cite: 10, 11].

---

## Configuration

### Prerequisites
[cite_start]**Assumption:** An active **Einstein Enhanced Bot** is already configured to handle standard, rule-based inquiries (such as 'Log a Case' or 'Status Check')[cite: 4, 10]. [cite_start]If a new bot instance is required, refer to the standard Salesforce documentation to build the initial framework before proceeding[cite: 336].

### Step 1: Configure the Agentforce Service Agent
To enable the advanced handling of complex queries, the Agentforce Service Agent must first be configured with the necessary knowledge base.

1.  [cite_start]**Create Data Library:** Create an Agentforce Data Library, set the Data Type to **'file'**, and upload the support policy and FAQ PDF documents[cite: 23].
2.  [cite_start]**Create Agent:** Create a new Agentforce Service Agent (e.g., 'Unified Resolution Agent')[cite: 53].
3.  **Assign Actions:** Configure the agent by adding the Data Library, Topics, and Instructions. [cite_start]Finally, assign the **'Answer Questions with Knowledge'** agent action to it[cite: 54, 55].

### Step 2: Configure the Transfer Logic (Omni-Channel Flow)
[cite_start]A specific "Outbound" Omni-Channel flow is required to bridge the existing Einstein Bot and the new Agentforce Agent[cite: 157].

1.  **Create a Fallback Queue:** Navigate to **Setup -> Queues**. [cite_start]Create a queue (e.g., "GPO Fallback") and add the Agentforce Service Agent user to it[cite: 158, 160].
2.  [cite_start]**Create the Flow:** Create a new Flow of type **Omni-Channel Flow**[cite: 161].
3.  **Route Work:** Add a **"Route Work"** element with the following settings:
    * [cite_start]**Service Channel:** Select "LiveMessage"[cite: 162].
    * [cite_start]**Route To:** Select "Agentforce Service Agent" and choose the specific agent created in Step 1 (e.g., 'Unified Resolution Agent')[cite: 162].
    * [cite_start]**Fallback:** Select the Queue created in the previous step (e.g., "GPO Fallback")[cite: 162].
4.  [cite_start]**Activate:** Save and activate the flow[cite: 163].

### Step 3: Update the Einstein Bot to Trigger Handoff
[cite_start]The final step involves modifying the existing bot to hand off the conversation when a specific user intent is detected[cite: 176].

1.  **Set Outbound Flow:** In the Einstein Bot Builder, navigate to the **Overview** tab. [cite_start]Locate **"Outbound Omni-Channel Flow"** and select the flow created in Step 2 (e.g., "Route to Unified Resolution Agent")[cite: 177].
2.  **Configure the Dialog Rule:** Open the Dialog intended for complex issues (e.g., "Talk to an Expert") and add a **Rule** action:
    * [cite_start]**Routing Type:** Set to "Omni-Channel Flow"[cite: 190].
    * [cite_start]**Route Destination:** Select the specific flow (e.g., "Route to Unified Resolution Agent")[cite: 190].
3.  [cite_start]**Transfer Action:** Add a **"Transfer"** rule action and set the destination variable to the `OmnichannelFlowId` created in the previous step[cite: 191].

---

## Conclusion
[cite_start]This hybrid bot solution uses a choice-driven approach to guide the customer journey[cite: 329]. [cite_start]Its architecture effectively segments service based on the user's need and intent[cite: 330]. 

* [cite_start]**Einstein Bot Classic** ensures speed and predictability for straightforward needs[cite: 331, 332].
* [cite_start]**Agentforce Agents** leverage deep context and autonomous action to provide personalized, human-like resolution for high-value interactions[cite: 334].

## Documentation
For a full step-by-step walkthrough including screenshots, please refer to the included PDF guide.

[![Read the PDF Guide](assets/pdf_cover_screenshot.png)](assets/Integrating_Einstein_Enhanced_Bot.pdf)

[📄 Download Full Implementation Guide (PDF)](assets/Integrating_Einstein_Enhanced_Bot.pdf)
