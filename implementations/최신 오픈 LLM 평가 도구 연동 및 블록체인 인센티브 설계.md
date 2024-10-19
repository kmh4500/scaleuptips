
# Design Document: Chatbot Evaluation Platform

---

## Problem Statement

### LLM Evaluation
Currently, there is no platform in South Korea that effectively evaluates Large Language Models (LLMs). For example, the Open Ko-LLM leaderboard by Upstage fosters models optimized for scores, regardless of actual chatbot performance. This leads to a fundamental issue where developers, let alone the general public, cannot easily assess which models are superior.

### Data Needs
There is a significant shortage of data reflecting Korean human preferences. This is a critical factor behind the suboptimal performance of Korean LLMs like HyperCLOVA-X and AiDot. Various companies are now hiring human labelers to collect human preference data, but high-quality data is becoming increasingly scarce.

### ANIA Platform Issues
Currently, users lack reasons to consistently engage with the ANIA platform, resulting in low traffic. There is a pressing need to provide AI/ML enthusiasts with compelling reasons to engage with the ANIA ecosystem.

---

## Background

### Lm-sys - Chatbot Arena  
Lm-sys Chatbot Arena (https://chat.lmsys.org/) uses a crowdsourced voting mechanism (qualitative assessment) to evaluate chatbots. It has become one of the most trusted leaderboards, addressing the shortcomings of the HuggingFace leaderboard. Many AI experts participate, contributing and retrieving valuable information.

### Korean Chatbot Arena  
A Korean version of Chatbot Arena (https://elo.instruct.kr/) exists, but as of May 16, 2024, the server is down, reflecting underlying issues:
- **Limited data**: As of April 11, 2024, only 3,000 interactions have been processed.
- **Resource scarcity**: Insufficient GPU resources lead to unstable operation.
- **Poor UI/UX**: User experience is unfriendly and discourages engagement.
- **Low discoverability**: Users have difficulty finding the platform, even via search engines.
- **Need for diversified qualitative evaluation**: Current ratings are limited to a single Elo score, which does not account for the nuanced strengths of different chatbot models.
    - For example, RAG-based chatbots should be assessed based on context-based reasoning.
    - Emotion/persona-based chatbots should be evaluated on natural conversation and empathy.
    - Domain-specific chatbots should be rated based on their internal knowledge.

---

## Requirements: Chatbot Arena

### Open Platform for LLM Evaluation
- **Crowdsourced LLM Evaluation**: The platform will facilitate anonymous, randomized head-to-head comparisons of LLM-generated responses to user questions.
- **User Voting**: Users will vote on which LLM provided a better response.
- **Data Collection**: User prompt data and voting results will be collected to rank LLMs.
- **Elo Rating System**: An Elo or Bradley-Terry model will be used to calculate model rankings.
- **Leaderboard**: The results will be visualized on a public leaderboard, displaying key statistics.

---

## System Architecture

### Component 1: Arena

- **User Interaction**: Users submit questions, and two randomly selected LLMs respond anonymously.
- **Voting**: After viewing both responses, the user votes for the better answer. The options are:
  - Model A, Model B, Tie, or No preference.
- **Model Reveal**: After voting, the user is informed of which models they evaluated.
- **Data Collection**: The system collects diverse user prompt data for further analysis.

---

### Component 2: Leaderboard

- **Data Storage**: Chat logs and voting data will be stored using Firebase, in JSON format.
- **Statistical Analysis**: Model rankings will be predicted using an Elo or Bradley-Terry system, based on the voting results.
- **Leaderboard Structure**:
  - **Rank**: Model rank.
  - **Model**: Name of the model.
  - **Elo Score**: Model’s Elo or Bradley-Terry rating.
  - **95% CI**: 95% confidence interval.
  - **Votes**: Total number of votes received.
  - **Organization**: The entity responsible for the model.
  - **License**: License type of the model.
  - **Knowledge Cutoff**: Date of the model’s knowledge cutoff.

---

### Component 3: AIN Credit

- **Credit Distribution**:
  - **Initial Proof of Concept (PoC)**: A total of ₩1,000,000 worth of AIN Credits will be allocated.
  - **Basic Credit**: An average of ₩100 worth of AIN Credit will be provided for each query evaluation.
  - **Variable Credit**: Credit will be adjusted based on the quality and rarity of the question/answer.
  
- **Abuse Detection**: If abuse is detected, no credits will be given, and users will be restricted.
  
- **Credit Weighting**: More credit will be allocated for unique and high-value feedback, especially in underrepresented evaluation categories like creativity, coding ability, sentiment analysis, etc.
  
- **Contribution Scoring System**:
  - The contribution score (0 to 1) quantifies how much a user's question or feedback contributed to LLM evaluation.
  - AIN Credit will be distributed based on the final contribution score.

- **User Ranking and Rewards**: Optional ranking for users based on accumulated credits, with additional rewards like badges, NFTs, and event-based challenges.

---

## Tech Stack

- **Backend**: FastAPI, Firebase
- **Frontend**: Next.js 14

---
