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
3.  **Configure Agent:** Add the Data Library, define Topics/Instructions, and assign the 'Answer Questions with Knowledge' action
