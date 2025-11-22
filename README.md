# The Seamless Handoff: Integrating Einstein Enhanced Bot with Agentforce Agent

The Hybrid Bot solution is the strategic fusion of Einstein Bot's rule-based triage with Agentforce AI's adaptive intelligence for better user experience. Einstein Bot Classic handles high-volume, repetitive inquiries with speed and consistency using its defined flows. Agentforce agents step in for complexity, leveraging Large Language Models (LLMs) to understand deep context, execute multi-step actions autonomously, and provide personalized, human-like resolution.

This blog will explore how this dual-strategy approach allows companies to redefine service: achieving the efficiency of automation while guaranteeing sophisticated, contextual resolution for every customer interaction. Learn how a Hybrid Bot maximizes efficiency and elevates customer satisfaction by deploying the right type of intelligence at the perfect moment.

## Use Case

QuantumConnect aims to achieve unified, intelligent customer service by ensuring the following:

* **Efficient transaction handling:** Quickly streamline high-frequency customer inquiries (Log Case and Status Check) using the initial bot (Einstein Bot Classic).
* **Specialized knowledge handoff:** Ensure all knowledge-based questions, regardless of complexity, are immediately handled by a dedicated, advanced agent (Agentforce Agent).

![Hybrid Bot Architecture: Einstein Classic triages transactions (Log/Status) and routes complex knowledge to Agentforce Agent.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image1.png?raw=true)

## Configure Agentforce Service Agent

Create an Agentforce Data Library, set the Data Type to 'file', and upload the support policy and FAQ PDF documents to it.

![Image shows how to set up the Agentforce Data library.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image2.png?raw=true)

Create a new Agentforce Service Agent named 'Unified Resolution Agent'. Once created, configure it by adding the Data Library, Topic, and Instruction. Finally, assign the 'Answer Questions with Knowledge' agent action to it.

![Agentforce Builder testing shows the AI accurately retrieves and grounds the warranty policy based on the user prompt from the knowledge base.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image3.png?raw=true)

## Configure Einstein Enhance Bot

### Step 1: Create a new Einstein Enhanced Bot

* Navigate to Setup => Einstein Bot, Select a type of bot = Enhanced Bot, click next.
* Select Start from Scratch.
* Give the bot name as “ Astro Case Resolution” and Primary Language as “English”, click Next.
* Keep the welcome message as default and add the Menu Item 1 = Case Status , Menu Item 2 = Log a Case , Menu Item 3 = Talk to an expert.
* Keep Outbound Omni-channel flow as blank. Will configure this in later steps. Click next and then click proceed.

### Step 2: Configure the “Case Status” Dialog

* Add the first component Question and ask the user to provide the email address.
* For Case Status dialogue add component flow and select an existing flow “Get Case Details”.
* Flow will query the case object and return the status of the case.
* Add the message component to show the status of the case.

![image shows the case status dialog configuration.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image4.png?raw=true)

### Step 3: Configure the “Log a Case” Dialog

* Add the first component Question and ask the user to provide the email address.
* Add the second component Question and ask the user to provide the Problem statement.
* Add the component to call the flow “Create a case flow”.
* Add a message component to provide the case number to the user.

![image shows the Log a case dialog configuration.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image5.png?raw=true)

### Step 4: Configure the “Talk to an expert” Dialog

Set the next step as “Transfer to Agent”.

![image shows the “Talk to an expert” dialog configuration.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image6.png?raw=true)

### Step 5: Configure the Omni-Channel flow for seamless chat transfer from the Einstein Bot to the Agentforce Service Agent.

* Create a queue , Setup -> Queue , give any name to the queue.
* In this case I am using the name as “GPO Fallback”.
* Add the Einstein Service Agent created as part of Agentforce Service Agent user in this queue.
* Create a flow of type Omni Channel flow.
* Add the step “Route Work” . Select the service channel as “LiveMessage”, route to as “Agentforce Service Agent” and select the “Unified Resolution Agent” and select the Fallback Queue as “GPO Fallback”.
* Save and activate the flow.

![Image shows the omni channel flow configuration to transfer the chat to “Unified Resolution Agent”.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image7.png?raw=true)

### Step 6: Configure the Einstein bot “Transfer To Agent” dialog.

Go to overview and set the Outbound Omni-Channel flow as “Route to Unified Resolution Agent”.

![Image shows how to set the Outbound Omni-Channel flow for Einstein Enhanced Bot.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image8.png?raw=true)

* Add the component Rules and select the Routing Type as “Omni-Channel” flow and set the Route Destination as “Route to Unified Resolution Agent”.
* Add another rule action “Transfer” and set the destination variable as “OmnichannelFlowId” created in the previous step.

![Image shows the “Transfer To Agent” dialog configuration.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image9.png?raw=true)

## Deploy the bot to the Experience Cloud site

### Step 1: Inbound Omni Channel Flow Configuration

When we create the enhanced bot, system will automatically create the Inbound Omni channel flow. Set the fall back queue that we created earlier “GPO Fallback and save activate the flow.

![Image shows the omni channel flow configuration to transfer the chat to “Astro Case Resolution” Einstein enhanced bot.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image10.png?raw=true)

Review the Einstein enhanced bot's Overview -> Inbound Omni-Channel Flows section to ensure correct configuration.

![Image shows how to set the Inbound Omni-Channel flow for Einstein Enhanced Bot.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image11.png?raw=true)

### Step 2: Create the Channel (Messaging for In-App and Web)

* In Salesforce Setup, search for and select Messaging Settings. Click New Channel.
* Click Start Select “Enhanced Chat”. Give the channel name “Astro case resolution web channel”.
* Select Deployment Type as “Web”.
* Give the domain url of your Experience cloud site without “https://”.
* Click next and select the routing type as “Omni-flow”. Flow definition as “Route to Astro Case Resolution” and Fallback Queue as “GPO Fallback”.
* Click save.

![Image shows the configuration for Messaging for In-App and Web channel](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image12.png?raw=true)

### Step 3: Create the Embedded Service Deployment

Creating the Messaging Channel automatically sets up the embedding service deployment.

![Image shows the embedding service deployment configuration screen.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image13.png?raw=true)

### Step 4: Experience Cloud Site configuration.

In the Experience Builder, open the components panel and Search for and drag the Embedded Messaging component onto your page. Set the Embedded Web Deployment as “Astro_case_resolution_web_channel”.

![Image shows the Embedded Messaging component set up on Experience cloud site.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image14.png?raw=true)

## Test the hybrid bot

**Case status :** User initiates chat on Experience Site; Astro Bot offers options, user selects case status, and the bot provides the details.

![The image depicts a user checking case status with the Astro Case Resolution Bot.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image15.png?raw=true)

![The image shows the bot receiving the user's email and responding with the case number and status.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image16.png?raw=true)

**Talk to an expert :** User selects "Talk to an expert," and the Astro Bot transfers the chat to the Agentforce Service Agent (Unified Resolution Agent).

![The image illustrates the chat handoff initiated by the user selecting "Talk to an expert," transferring the conversation from Astro Bot to the Unified Resolution Agent.](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image17.png?raw=true)

## Conclusion

This hybrid bot solution uses a choice-driven approach to guide the customer journey. Its architecture, which combines Einstein Bot Classic and Agentforce agent, effectively segments service based on the user's need and intent. Customers first encounter the Einstein Bot Classic for straightforward needs (e.g., checking invoices, tracking packages, logging/checking case status). Users select these direct, rule-based flows for immediate, reliable resolution, ensuring speed and predictability at scale. For complex queries, customers are offered the option to " Talk to an Expert ." This immediately deploys the LLM-driven Agentforce agent. By leveraging deep context and autonomous action, this agent provides personalized, human-like resolution for high-value interactions, bypassing the live agent queue.

## Resources

* Documentation: [Set Up Enhanced Bots](https://help.salesforce.com/s/articleView?id=service.bots_service_enhanced.htm&type=5)
* Documentation: [Advanced Routing with Omni-Channel Flows](https://help.salesforce.com/s/articleView?id=service.omnichannel_flows.htm&type=5)
* Documentation: [Transfer Conversations from an Enhanced Bot to an Agentforce Service Agent](https://help.salesforce.com/s/articleView?id=service.bots_service_asa_transfer_conversation.htm&type=5)
* Documentation: [Embedded Messaging](https://help.salesforce.com/s/articleView?language=en_US&id=experience.rss_embedded_messaging.htm&type=5)
* Documentation: [Build the Future with Agentforce](https://developer.salesforce.com/agentforce-workshop)

