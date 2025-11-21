# [cite_start]The Seamless Handoff: Integrating Einstein Enhanced Bot with Agentforce Agent [cite: 1]

[cite_start]The Hybrid Bot solution is the strategic fusion of Einstein Bot's rule-based triage with Agentforce AI's adaptive intelligence for better user experience. [cite: 2] [cite_start]Einstein Bot Classic handles high-volume, repetitive inquiries with speed and consistency using its defined flows. [cite: 3] [cite_start]Agentforce agents step in for complexity, leveraging Large Language Models (LLMs) to understand deep context, execute multi-step actions autonomously, and provide personalized, human-like resolution. [cite: 4]

[cite_start]This blog will explore how this dual-strategy approach allows companies to redefine service: achieving the efficiency of automation while guaranteeing sophisticated, contextual resolution for every customer interaction. [cite: 5] [cite_start]Learn how a Hybrid Bot maximizes efficiency and elevates customer satisfaction by deploying the right type of intelligence at the perfect moment. [cite: 6]

## [cite_start]Use Case [cite: 7]

[cite_start]QuantumConnect aims to achieve unified, intelligent customer service by ensuring the following: [cite: 8]

* [cite_start]**Efficient transaction handling:** Quickly streamline high-frequency customer inquiries (Log Case and Status Check) using the initial bot (Einstein Bot Classic). [cite: 9]
* [cite_start]**Specialized knowledge handoff:** Ensure all knowledge-based questions, regardless of complexity, are immediately handled by a dedicated, advanced agent (Agentforce Agent). [cite: 10]

[cite_start]![Hybrid Bot Architecture: Einstein Classic triages transactions (Log/Status) and routes complex knowledge to Agentforce Agent. [cite: 11]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image1.png?raw=true)

## [cite_start]Configure Agentforce Service Agent [cite: 12]

[cite_start]Create an Agentforce Data Library, set the Data Type to 'file', and upload the support policy and FAQ PDF documents to it. [cite: 13]

[cite_start]![Image shows how to set up the Agentforce Data library. [cite: 14]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image2.png?raw=true)

[cite_start]Create a new Agentforce Service Agent named 'Unified Resolution Agent'. [cite: 15] [cite_start]Once created, configure it by adding the Data Library, Topic, and Instruction. [cite: 16] [cite_start]Finally, assign the 'Answer Questions with Knowledge' agent action to it. [cite: 17]

[cite_start]![Agentforce Builder testing shows the AI accurately retrieves and grounds the warranty policy based on the user prompt from the knowledge base. [cite: 18]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image3.png?raw=true)

## [cite_start]Configure Einstein Enhance Bot [cite: 19]

### [cite_start]Step 1: Create a new Einstein Enhanced Bot [cite: 20]

* [cite_start]Navigate to Setup => Einstein Bot, Select a type of bot = Enhanced Bot, click next. [cite: 21]
* [cite_start]Select Start from Scratch. [cite: 22]
* [cite_start]Give the bot name as “ Astro Case Resolution” and Primary Language as “English”, click Next. [cite: 23]
* [cite_start]Keep the welcome message as default and add the Menu Item 1 = Case Status , Menu Item 2 = Log a Case , Menu Item 3 = Talk to an expert. [cite: 24]
* Keep Outbound Omni-channel flow as blank. Will configure this in later steps. [cite_start]Click next and then click proceed. [cite: 25]

### [cite_start]Step 2: Configure the “Case Status” Dialog [cite: 26]

* [cite_start]Add the first component Question and ask the user to provide the email address. [cite: 27]
* [cite_start]For Case Status dialogue add component flow and select an existing flow “Get Case Details”. [cite: 28]
* [cite_start]Flow will query the case object and return the status of the case. [cite: 29]
* [cite_start]Add the message component to show the status of the case. [cite: 30]

[cite_start]![image shows the case status dialog configuration. [cite: 31]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image4.png?raw=true)

### [cite_start]Step 3: Configure the “Log a Case” Dialog [cite: 32]

* [cite_start]Add the first component Question and ask the user to provide the email address. [cite: 33]
* [cite_start]Add the second component Question and ask the user to provide the Problem statement. [cite: 34]
* [cite_start]Add the component to call the flow “Create a case flow”. [cite: 35]
* [cite_start]Add a message component to provide the case number to the user. [cite: 36]

[cite_start]![image shows the Log a case dialog configuration. [cite: 37]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image5.png?raw=true)

### [cite_start]Step 4: Configure the “Talk to an expert” Dialog [cite: 38]

[cite_start]Set the next step as “Transfer to Agent”. [cite: 39]

[cite_start]![image shows the “Talk to an expert” dialog configuration. [cite: 40]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image6.png?raw=true)

### [cite_start]Step 5: Configure the Omni-Channel flow for seamless chat transfer from the Einstein Bot to the Agentforce Service Agent. [cite: 41]

* [cite_start]Create a queue , Setup -> Queue , give any name to the queue. [cite: 42]
* [cite_start]In this case I am using the name as “GPO Fallback”. [cite: 43]
* [cite_start]Add the Einstein Service Agent created as part of Agentforce Service Agent user in this queue. [cite: 44]
* [cite_start]Create a flow of type Omni Channel flow. [cite: 45]
* Add the step “Route Work” . [cite_start]Select the service channel as “LiveMessage”, route to as “Agentforce Service Agent” and select the “Unified Resolution Agent” and select the Fallback Queue as “GPO Fallback”. [cite: 46]
* [cite_start]Save and activate the flow. [cite: 47]

[cite_start]![Image shows the omni channel flow configuration to transfer the chat to “Unified Resolution Agent”. [cite: 48]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image7.png?raw=true)

### [cite_start]Step 6: Configure the Einstein bot “Transfer To Agent” dialog. [cite: 49]

[cite_start]Go to overview and set the Outbound Omni-Channel flow as “Route to Unified Resolution Agent”. [cite: 50]

[cite_start]![Image shows how to set the Outbound Omni-Channel flow for Einstein Enhanced Bot. [cite: 51]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image8.png?raw=true)

* [cite_start]Add the component Rules and select the Routing Type as “Omni-Channel” flow and set the Route Destination as “Route to Unified Resolution Agent”. [cite: 52]
* [cite_start]Add another rule action “Transfer” and set the destination variable as “OmnichannelFlowId” created in the previous step. [cite: 53]

[cite_start]![Image shows the “Transfer To Agent” dialog configuration. [cite: 54]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image9.png?raw=true)

## [cite_start]Deploy the bot to the Experience Cloud site [cite: 55]

### [cite_start]Step 1: Inbound Omni Channel Flow Configuration [cite: 56]

[cite_start]When we create the enhanced bot, system will automatically create the Inbound Omni channel flow. [cite: 57] [cite_start]Set the fall back queue that we created earlier “GPO Fallback and save activate the flow. [cite: 58]

[cite_start]![Image shows the omni channel flow configuration to transfer the chat to “Astro Case Resolution” Einstein enhanced bot. [cite: 59]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image10.png?raw=true)

[cite_start]Review the Einstein enhanced bot's Overview -> Inbound Omni-Channel Flows section to ensure correct configuration. [cite: 60]

[cite_start]![Image shows how to set the Inbound Omni-Channel flow for Einstein Enhanced Bot. [cite: 61]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image11.png?raw=true)

### [cite_start]Step 2: Create the Channel (Messaging for In-App and Web) [cite: 62]

* In Salesforce Setup, search for and select Messaging Settings. [cite_start]Click New Channel. [cite: 63]
* Click Start Select “Enhanced Chat”. [cite_start]Give the channel name “Astro case resolution web channel”. [cite: 64]
* [cite_start]Select Deployment Type as “Web”. [cite: 65]
* [cite_start]Give the domain url of your Experience cloud site without “https://”. [cite: 66]
* Click next and select the routing type as “Omni-flow”. [cite_start]Flow definition as “Route to Astro Case Resolution” and Fallback Queue as “GPO Fallback”. [cite: 67]
* [cite_start]Click save. [cite: 68]

[cite_start]![Image shows the configuration for Messaging for In-App and Web channel [cite: 69]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image12.png?raw=true)

### [cite_start]Step 3: Create the Embedded Service Deployment [cite: 70]

[cite_start]Creating the Messaging Channel automatically sets up the embedding service deployment. [cite: 71]

[cite_start]![Image shows the embedding service deployment configuration screen. [cite: 72]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image13.png?raw=true)

### [cite_start]Step 4: Experience Cloud Site configuration. [cite: 73]

[cite_start]In the Experience Builder, open the components panel and Search for and drag the Embedded Messaging component onto your page. [cite: 74] [cite_start]Set the Embedded Web Deployment as “Astro_case_resolution_web_channel”. [cite: 75]

[cite_start]![Image shows the Embedded Messaging component set up on Experience cloud site. [cite: 76]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image14.png?raw=true)

## [cite_start]Test the hybrid bot [cite: 77]

[cite_start]**Case status :** User initiates chat on Experience Site; [cite: 78] [cite_start]Astro Bot offers options, user selects case status, and the bot provides the details. [cite: 79]

[cite_start]![The image depicts a user checking case status with the Astro Case Resolution Bot. [cite: 80]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image15.png?raw=true)

[cite_start]![The image shows the bot receiving the user's email and responding with the case number and status. [cite: 81]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image16.png?raw=true)

[cite_start]**Talk to an expert :** User selects "Talk to an expert," and the Astro Bot transfers the chat to the Agentforce Service Agent (Unified Resolution Agent). [cite: 82]

[cite_start]![The image illustrates the chat handoff initiated by the user selecting "Talk to an expert," transferring the conversation from Astro Bot to the Unified Resolution Agent. [cite: 83]](https://github.com/cagarwal21/einstein-bot-to-agentforce-handoff/blob/main/Images/Image17.png?raw=true)

## [cite_start]Conclusion [cite: 84]

[cite_start]This hybrid bot solution uses a choice-driven approach to guide the customer journey. [cite: 85] [cite_start]Its architecture, which combines Einstein Bot Classic and Agentforce agent, effectively segments service based on the user's need and intent. [cite: 86] [cite_start]Customers first encounter the Einstein Bot Classic for straightforward needs (e.g., checking invoices, tracking packages, logging/checking case status). [cite: 87] [cite_start]Users select these direct, rule-based flows for immediate, reliable resolution, ensuring speed and predictability at scale. [cite: 88] [cite_start]For complex queries, customers are offered the option to " Talk to an Expert ." [cite: 89] This immediately deploys the LLM-driven Agentforce agent. [cite_start]By leveraging deep context and autonomous action, this agent provides personalized, human-like resolution for high-value interactions, bypassing the live agent queue. [cite: 90]

## [cite_start]Resources [cite: 91]

* [cite_start]Documentation: Set Up Enhanced Bots [cite: 92]
* [cite_start]Documentation: Advanced Routing with Omni-Channel Flows [cite: 93]
* [cite_start]Documentation: Transfer Conversations from an Enhanced Bot to an Agentforce Service Agent [cite: 94]
* [cite_start]Documentation: Embedded Messaging [cite: 95]
* [cite_start]Documentation: Build the Future with Agentforce [cite: 96]

## [cite_start]About the authors [cite: 97]

* **Chandan Agarwal** is a Lead Member of Technical Staff at Salesforce. [cite_start]You can find him on LinkedIn. [cite: 98]

* **Ishita Saxena** is a Senior Solution Consultant at Salesforce. [cite_start]You can find her on LinkedIn. [cite: 99]
