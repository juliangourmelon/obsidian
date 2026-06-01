Tags: [[AAP]]

Links: [[Ansible Intelligent Assistant Use Case]]; [[Ansible Use Cases]]


# 1. What is the Intelligent Assistant?

The **Ansible Lightspeed Intelligent Assistant** is an AI service integrated into the Ansible Automation Platform (AAP) UI that can:

- Answer questions about your automation environment
- Help install and configure AAP
- Explain failures
- Troubleshoot jobs
- Analyze logs
- Recommend optimizations
- Generate automation content
- Explain Ansible concepts

Instead of generating YAML from scratch, it has access to operational context from the platform.



# 3. Where Does the Knowledge Come From?

The Intelligent Assistant uses several sources.

## A. Product Documentation

Examples:

- Ansible Core docs
- Automation Controller docs
- Automation Hub docs
- Event-Driven Ansible docs
- AAP installation docs

When you ask:

> How do I configure execution environments?

it performs retrieval over indexed documentation before calling the LLM.

---

## B. Platform Metadata

The assistant can inspect:

- inventories
- job templates
- projects
- credentials
- controller settings

For example:

> Explain my inventory structure

The assistant can read the metadata and explain it.

---

## C. Job Execution Data

This is where it becomes interesting.

It can analyze:

- Job status
- stdout
- stderr
- task results
- module outputs

Example:

```
TASK [Install package]fatal: [server1]:FAILED! => {  "msg": "No package matching nginx available"}
```

The assistant can explain:

- what happened
- probable root cause
- suggested fix

---

## D. Event Streams

The assistant can inspect:

- execution events
- workflow events
- controller activity

allowing it to answer:

> Why did the workflow stop after node 3?




# 4. What Happens When a User Asks a Question?

Let's take:

> Why did Job #432 fail?

---

## Step 1

User submits prompt.

```
Why did Job #432 fail?
```

---

## Step 2

Context gathering begins.

The assistant retrieves:

```
Job ID 432stdoutstderrinventoryjob templateexecution environment
```

---

## Step 3

Relevant chunks are created.

Example:

```
TASK [Install nginx]FAILEDNo package matching nginx available
```

---

## Step 4

Prompt Augmentation

The system creates a much larger prompt:

```
You are an Ansible expert.Job Output:TASK [Install nginx]FAILEDNo package matching nginx availableUser Question:Why did Job #432 fail?
```

---

## Step 5

Prompt sent to Granite model.

Typically:

- Granite Code
- Granite Instruct
- watsonx Code Assistant model

depending on deployment.

---

## Step 6

Generated Answer

Example:

```
The target host does not have accessto a repository containing nginx.Possible causes:- Missing repository- Unsupported OS- Package name mismatchRecommended action:run dnf search nginx
```



# 6. AI Models Behind the Assistant

Historically, Red Hat partnered with IBM.

The backend usually relies on:

IBM  
**watsonx.ai**

and

Granite Models

specifically:

- Granite Code 
- Granite Instruct
- Granite 20B variants
- newer Granite generations

depending on the release.

The exact model is less important than the surrounding retrieval architecture.

Most of the intelligence comes from:

```
Context+Documentation+Logs+Events+LLM
```

rather than pure model knowledge.




# 8. Typical Components Required

For a self-hosted deployment you typically need:

### Mandatory

- [Red Hat Ansible Automation Platform](https://www.redhat.com/en/technologies/management/ansible?utm_source=chatgpt.com)
- Intelligent Assistant services
- Granite model endpoint
- Vector database / retrieval layer
- Documentation index

### Optional

- [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai?utm_source=chatgpt.com)
- [IBM watsonx.governance](https://www.ibm.com/products/watsonx-governance?utm_source=chatgpt.com) [[AI_GOVERNANCE]]; [[Governance]]
- Custom enterprise knowledge bases

---

# 9. Resource Requirements

For your platform discussions around OpenShift and MaaS:

A small deployment serving 1–5 concurrent administrators can often work with:

|Component|Typical Size|
|---|---|
|Granite 20B|1–2 H100 or 2–4 L40S|
|Retrieval service|4–8 vCPU|
|Vector database|4–8 vCPU|
|Assistant APIs|2–4 vCPU|

A Granite 20B-class model is usually sufficient because:

- prompts are relatively short
- answers are operational guidance
- code generation is limited
- concurrency is low

For an internal operations assistant with only a handful of users, a 20B model is generally a reasonable starting point.