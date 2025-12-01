# 🤖 Enterprise AI Support Agent — Multi-Agent System with Tools, MCP, A2A, and LLM-Orchestration

A production-ready AI agent that handles **enterprise product support, refunds, and logistics** using **agent tools, external A2A agents, and long-running approvals**.

## 📚 Project Context

This project was developed as part of the **Kaggle — 5-Day AI Agents Intensive Course with Google**.  

This capstone project demonstrates a real-world enterprise workflow agent, integrating multiple concepts from the course:
- Multi-agent orchestration (concierge + enterprise logic)
- Sub-agents via A2A protocol
- Deterministic function tools
- Policy enforcement & conditional decisions
- Structured responses suitable for real deployments

---

## 🌐 Overview

Modern enterprises need support agents that:
- **Know accurate product information** (stock, specs, prices)
- **Understand customer policies and tiers**
- **Follow real business logic** (refund limits, shipping rules)
- **Avoid hallucinations**

This project solves this by using a **multi-agent architecture**:
- A **Support Agent** orchestrates the conversation
- A **Product Catalog Agent (remote)** serves as the source of truth
- Custom business tools perform **refunds, customer lookup, shipping**
- A specialist **Escalation Agent** handles policy violations or exceptions

Instead of a single “chatbot”, the system is a **collaboration of specialized agents**.

---


Key idea:  
👉 **LLM is not doing everything** — it is **orchestrating tools and specialists**.

---

## 🧭 Agent Workflow & Logic

### 1️⃣ Product Queries
- User: “Tell me about the Macbook Pro 14”
- Support Agent → **A2A call** → Product Catalog Agent
- Response built from real catalog info (no guessing)

**Why this matters:** real inventory ≠ hallucinated inventory

---

### 2️⃣ Refund Handling
- Parse: product, customer_id, amount
- Use tools:
  - `get_customer_profile(customer_id)`
  - `get_refund_policy(product)`

Refund flow:

lookup customer tier → read limit → compare amount

| <= limit → approve

| > limit → escalate

This avoids “chatbot shipping” and turns into **workflow automation**.

---

## ⚙️ Technologies Used

**🔹 ADK (Agent Development Kit)**
- Core agent framework
- Built-in tool execution
- Session consistency

**🔹 Gemini (gemini-2.5-flash-lite)**
- LLM brain
- Fast, cost-efficient
- Great for structured instructions

**🔹 A2A Protocol**
- Exposes the product catalog agent as a remote service
- Other agents consume it like an API
- Removes hallucination from product data

**🔹 Function Tools**
- Python business logic functions
- Deterministic responses
- Validated behavior

**🔹 Long-Running Operations**
- Human-in-the-loop approvals
- State preservation
- Real enterprise flows

---

## 🚀 Example Interactions

### 🛒 Product Inquiry
> Tell me about the Macbook Pro 14

Returns:
- Price
- Stock count
- Specs
- Source: Remote Product Agent

Not: “LLM imagined answer”

---

### 💰 Refund
> Refund Macbook Pro 14 for customer 211 amount 18000 INR

Flow:
1. Customer profile → “GOLD”
2. Refund limit → 20,000
3. Amount 18,000 ≤ 20,000 → **Approved**

Clear, traceable, policy-aligned.

---

### 🚚 Shipping
> Ship 12 units of order 9921  
Units > 5 → bulk shipment
> Ship 5 units of order 9921  
Units ≤ 5 → standard shipment

No hallucination.  
No “chatty LLM guesses”.  
Just structured enterprise outputs.


---

## 🛠 Build Summary

- Tools = executable business logic
- Support Agent = orchestrator
- Specialist Agents = expertise boundaries
- No untrusted “LLM imagination”
- Every decision backed by verifiable data
