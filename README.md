# Dynamic Voting Protocol: A Decentralized Decision-Making System Based on Thematic Reputation, Vote Delegation, and Bridging Strategies

**Juan José Albán**  
*jalban.arq@gmail.com*  
*j.alban@uniandes.edu.co*  
*Revision: 2025-02-24 A*  

## Abstract

The Dynamic Voting Protocol is a decentralized system designed to enhance collective decision-making by rewarding informed participation and penalizing manipulation. Built on three core pillars—dynamic voting weight based on thematic reputation, weighted vote delegation, and consensus-driven bridging strategies—this protocol leverages blockchain technology to ensure transparency, auditability, and resistance to abuse. It aims to create a fairer, more representative voting system where expertise and diverse consensus shape outcomes, ultimately fostering trust and empowerment in decision-making processes.

---

## Contents

1. [Background](#1-background)
2. [Protocol Overview](#2-protocol-overview)
3. [Main Components](#3-main-components)
   1. [Voter Profiles](#31-voter-profiles)
   2. [Reputation Assessments](#32-reputation-assessments)
   3. [Vote Delegation](#33-vote-delegation)
   4. [Bridging Strategies](#34-bridging-strategies)
   5. [Verifications](#35-verifications)
   6. [Connections](#36-connections)
   7. [Decentralized Network](#37-decentralized-network)
   8. [Participants](#38-participants)
      1. [Voters (End-Users)](#381-voters-end-users)
      2. [Storers](#382-storers)
      3. [Nodes (Miners)](#383-nodes-miners)
      4. [Retrievers](#384-retrievers)
   9. [Incentives](#39-incentives)
      1. [Overview](#391-overview)
      2. [Motivators](#392-motivators)
   10. [Governance](#310-governance)
4. [Vote Weight Calculation](#4-vote-weight-calculation)
   1. [Formula](#41-formula)
   2. [Reputation Dynamics](#42-reputation-dynamics)
5. [Privacy, Authentication, and Encryption](#5-privacy-authentication-and-encryption)
   1. [Privacy](#51-privacy)
   2. [Encryption and Authentication](#52-encryption-and-authentication)
6. [Data Structures](#6-data-structures)
   1. [Account](#61-account)
   2. [Profile](#62-profile)
   3. [Reputation Record](#63-reputation-record)
   4. [Delegation](#64-delegation)
   5. [Vote](#65-vote)
7. [Protocol Sketch](#7-protocol-sketch)
   1. [Storer Cycle](#71-storer-cycle)
   2. [Node Cycle](#72-node-cycle)
   3. [Retriever Cycle](#73-retriever-cycle)
8. [Rewards for Nodes (Miners)](#8-rewards-for-nodes-miners)
9. [Blockchain Technology](#9-blockchain-technology)
10. [Protection Against Abuse and Manipulation](#10-protection-against-abuse-and-manipulation)
    1. [Reputation](#101-reputation)
    2. [Verifications](#102-verifications)
    3. [Incentives](#103-incentives)
    4. [Quality Scores](#104-quality-scores)
11. [Applications](#11-applications)
    1. [Improvements for Existing Use Cases](#111-improvements-for-existing-use-cases)
    2. [Potential New Use Cases](#112-potential-new-use-cases)
12. [Open Questions and Ongoing Work](#12-open-questions-and-ongoing-work)
13. [Related Work](#13-related-work)
14. [Acknowledgments](#14-acknowledgments)
15. [References](#15-references)

---

## 1. Background

## 1. Background

Collective decision-making has historically been a cornerstone of organized societies, yet it has perpetually grappled with challenges such as manipulation by uninformed or coordinated factions, opacity in process, and the exclusion of diverse perspectives. For centuries, decisions rested with centralized authorities, often rendering outcomes inefficient and unrepresentative. The advent of democratic systems, rooted in the Greek ideal of *dēmokratía* ("rule of the people"), promised broader participation, but traditional mechanisms like simple majority rule frequently sidelined expertise and marginalized minority voices (Liddell & Scott, 1889). The 20th and 21st centuries introduced digital platforms that amplified these issues—social media polls and corporate decision tools often prioritized engagement over substance, deepening divisions and eroding trust (Ovadya, 2022). Blockchain technology, pioneered by systems like Bitcoin (Nakamoto, 2008) and Ethereum (Buterin, 2013), offered a transformative solution through immutable, transparent ledgers, yet its application alone does not inherently ensure informed participation or bridge societal divides.

Significant strides in decentralized systems provide a foundation for addressing these gaps. The *Torre Protocol* (Torrenegra, 2018) emerged as a pioneering effort to liberate professional reputation from the silos of centralized platforms like LinkedIn, Uber, and Upwork. These platforms, while facilitating socioeconomic mobility through networks of recommendations, restricted data portability—LinkedIn, for instance, pursued legal action against entities accessing user-authorized data (Conger, 2016), and freelancing marketplaces prevented users from transferring earned reputations, forcing them to restart upon switching services (Torrenegra, 2018). Torre countered this by proposing a blockchain-based, decentralized reputation network where individuals controlled their curricula vitae and recommendations. Its novel recommendation weight system, inspired by PageRank (Page, 1998), assigned greater influence to endorsements from highly recommended individuals, ensuring trustworthiness through scarcity and public verifications. While Torre focused on professional mobility, its principles of weighted credibility and decentralization laid crucial groundwork for broader decision-making applications.

Parallel innovations in voting systems further inform this evolution. The *Google Votes* experiment (Hardt & Lopes, 2015), conducted within Google’s internal Google+ network from March 2012 to February 2015, tested liquid democracy—a hybrid of direct and representative democracy where voters could delegate their votes to trusted peers. Over three years, 20,000 Googlers engaged with the system, creating 370 issues and casting over 87,000 votes, including delegated ones. Food-related decisions dominated, with 150 issues and 73,000 votes, reflecting high engagement due to their universal appeal within Google’s culture. Notably, 3.6% of votes were delegated, a modest yet significant uptake for a workforce new to liquid democracy. A standout case was the 2013 Mountain View Microkitchen Food Fair, where 4,600 Googlers cast 62,000 votes across 25 snack categories, with 4.7% delegated—a higher proportion than the average—demonstrating delegation’s potential in large-scale, practical settings. The experiment’s success, evidenced by 175,000 pageviews and adoption of results in microkitchen stocking, underscored liquid democracy’s scalability when paired with social networking tools, though it highlighted challenges like initial user education and limited mobile engagement (8.5% of votes) (Hardt & Lopes, 2015).

The *Dynamic Voting Protocol* synthesizes these advancements, extending Torre’s reputation weighting and Google Votes’ delegation into a comprehensive decision-making framework. It aligns with the Technology and Public Purpose (TAPP) Project principles, which, though not formally affiliated, resonate deeply:

1. **Technology’s advance is inevitable, and it often brings progress for some.** Yet, progress for all demands proactive solutions to dilemmas like uninformed voting or polarized outcomes, as seen in traditional systems and early digital experiments.
2. **There is no silver bullet.** Effective governance requires blending tech-sector innovation—like Torre’s blockchain approach and Google Votes’ social integration—with regulatory oversight, fostering trust through transparency and collaboration.
3. **Public purpose-driven innovation relies on inspiring tech leaders.** This protocol builds on Torre’s empowerment ethos and Google Votes’ practical insights to equip future stewards with tools for sustainable, inclusive decisions.

Unlike Torre’s focus on professional reputation or Google Votes’ corporate scope, the *Dynamic Voting Protocol* targets collective governance across domains—DAOs, public consultations, and beyond. It introduces dynamic voting weights based on thematic expertise, flexible delegation inspired by liquid democracy, and bridging strategies to ensure consensus across diverse groups, aiming for a more equitable and effective decision-making paradigm in a decentralized era.



---

## 2. Protocol Overview

The Dynamic Voting Protocol is a decentralized decision-making system that empowers voters to participate in collective choices with weights dynamically adjusted based on their thematic reputation, allows vote delegation to trusted experts, and employs bridging strategies to foster consensus among diverse groups. Leveraging blockchain, it ensures transparency and integrity while enabling applications like DAO governance, public consultations, and community debates.

---

## 3. Main Components

### 3.1. Voter Profiles

Voter profiles are structured records containing thematic reputation scores, voting history, and connections, serving as the foundation for weighted participation.

### 3.2. Reputation Assessments

Reputation is assessed through peer evaluations, verified contributions, and past voting accuracy, ensuring that expertise influences voting weight.

### 3.3. Vote Delegation

Users can delegate their votes to others with higher thematic reputation, with weights adjusted proportionally to maintain balance.

### 3.4. Bridging Strategies

Bridging algorithms identify diverse voter groups and enhance vote weights for decisions supported across these groups, promoting inclusivity.

### 3.5. Verifications

Crowdsourced, public verifications prevent fake accounts and ensure participant authenticity.

### 3.6. Connections

Voters can form reciprocal connections, creating a network that informs reputation and delegation dynamics.

### 3.7. Decentralized Network

The protocol operates on a blockchain, ensuring data integrity and transparency while enabling permissionless innovation.

### 3.8. Participants

#### 3.8.1. Voters (End-Users)

Voters create profiles, cast votes, delegate voting power, and authorize data access.

#### 3.8.2. Storers

Storers interface between voters and the blockchain, adding and updating data.

#### 3.8.3. Nodes (Miners)

Nodes maintain the ledger, calculate vote weights, and process transactions, earning rewards.

#### 3.8.4. Retrievers

Retrievers access and publish voter data, enabling applications to utilize the protocol.

### 3.9. Incentives

#### 3.9.1. Overview

Incentives encourage honest participation and network maintenance through tokens and reputation gains.

#### 3.9.2. Motivators

Voters are motivated by control over their influence, while nodes earn tokens for computational efforts.

### 3.10. Governance

Governance is split between token holders and active voters, with decisions made via weighted voting.

---

## 4. Vote Weight Calculation

### 4.1. Formula

The weight of a vote (\( W_v \)) is calculated as:

\[ W_v = R_t \times D \times B \times Q \]

- \( R_t \): Thematic reputation (0 to 1), capped to prevent dominance.
- \( D \): Delegation factor (0 to 1), reflecting delegated vote weight.
- \( B \): Bridging factor (0 to 1), enhancing consensus across groups.
- \( Q \): Quality score (0 to 1), based on justification rigor.

### 4.2. Reputation Dynamics

Reputation decays over time unless validated by new contributions, ensuring ongoing engagement.

---

## 5. Privacy, Authentication, and Encryption

### 5.1. Privacy

Public data enhances transparency, while sensitive information is encrypted.

### 5.2. Encryption and Authentication

Users manage public-private key pairs for authentication and data protection, supported by protocol-specific wallets.

---

## 6. Data Structures

### 6.1. Account

- **Plain Text**: ID, Name, Verified Status
- **Encrypted**: Key History

### 6.2. Profile

- **Plain Text**: Account ID, Thematic Reputation
- **Encrypted**: Contact Details

### 6.3. Reputation Record

- **Plain Text**: Evaluator ID, Evaluated ID, Theme, Score

### 6.4. Delegation

- **Plain Text**: Delegator ID, Delegate ID, Theme, Weight

### 6.5. Vote

- **Plain Text**: Vote ID, Voter ID, Decision, Weight

---

## 7. Protocol Sketch

### 7.1. Storer Cycle

Storers create accounts, update profiles, and submit votes or delegations.

### 7.2. Node Cycle

Nodes validate transactions, calculate weights, and update the ledger.

### 7.3. Retriever Cycle

Retrievers monitor the ledger and publish data for applications.

---

## 8. Rewards for Nodes (Miners)

Nodes earn tokens based on transaction complexity and storer quality, ensuring a free service for users.

---

## 9. Blockchain Technology

A dual-blockchain approach separates data storage and token management, optimizing scalability and liquidity.

---

## 10. Protection Against Abuse and Manipulation

### 10.1. Reputation

Reputation is seeded through verified users and capped to prevent monopolies.

### 10.2. Verifications

Public verifications ensure authenticity, with retractable but indelible records.

### 10.3. Incentives

Intrinsic motivators dominate, with tokens reserved for nodes.

### 10.4. Quality Scores

Storers with poor scores face request limits, deterring spam.

---

## 11. Applications

### 11.1. Improvements for Existing Use Cases

- **DAO Governance**: Fairer voting with expert influence.
- **Public Consultations**: Transparent, representative outcomes.

### 11.2. Potential New Use Cases

- **Community Debates**: Highlighting informed consensus.
- **Policy Development**: Bridging diverse stakeholder input.

---

## 12. Open Questions and Ongoing Work

- How to optimize bridging for large-scale consensus?
- What safeguards prevent coercion in vote delegation?
- Can the protocol scale to millions of voters efficiently?

---

## 13. Related Work

- Aragon, DAOstack: Blockchain voting systems.
- Bloom, uPort: Decentralized reputation frameworks.

---

## 14. Acknowledgments

Thanks to contributors for their valuable feedback.

---

## 15. References

- Nakamoto, S., 2008. Bitcoin: A Peer-to-Peer Electronic Cash System.
- Buterin, V., 2013. Ethereum Whitepaper.
- Ovadya, A., 2022. How Platform Recommendation Systems Might Reduce Division and Strengthen Democracy

---

© Dynamic Voting Labs
