# RFC: Dynamic Voting Protocol: A Decentralized Decision-Making System Based on Thematic Reputation, Vote Delegation, and Bridging Strategies
Category: Experimental                                         
                                                               **Juan José Albán**  
                                                               *jalban.arq@gmail.com*  
                                                               *j.alban@uniandes.edu.co*  
                                                               Febrary 2025    
Request for Comments: P/1    
Obsoletes: P/0

## Status of this memo
   This document specifies a experimental system for decision-making through internet, and requests discussion and suggestions for improvements. 
   
   Distribution of this memo is unlimited.

## Abstract

The Dynamic Voting Protocol is a decentralized system designed to enhance collective decision-making by rewarding informed participation and penalizing manipulation. Built on three core pillars—dynamic voting weight based on thematic reputation, weighted vote delegation, and consensus-driven bridging strategies—this protocol leverages blockchain technology to ensure transparency, auditability, and resistance to abuse. It aims to create a fairer, more representative voting system where expertise and diverse consensus shape outcomes, ultimately fostering trust and empowerment in decision-making processes.

This protocol is intended to be implementable across all political viewpoints or in all kind of organizations!!
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

The *Dynamic Voting Protocol* is a decentralized, blockchain-based framework designed to revolutionize collective decision-making by addressing the limitations of traditional democratic systems and early digital experiments. It empowers participants to engage in governance processes—spanning decentralized autonomous organizations (DAOs), public consultations, community debates, and beyond—with a system that ensures decisions are informed, representative, and resistant to manipulation. Drawing inspiration from the *Torre Protocol*’s emphasis on reputation weighting (Torrenegra, 2018) and the *Google Votes* experiment’s practical application of liquid democracy (Hardt & Lopes, 2015), this protocol introduces a novel synthesis of three core pillars: dynamic voting weight based on thematic reputation, weighted vote delegation, and bridging strategies for consensus across diverse groups. These elements are seamlessly integrated into a transparent, auditable platform that leverages blockchain technology to foster trust and scalability.

At its heart, the protocol reimagines voting power as a reflection of expertise rather than sheer numbers. Each participant’s vote is assigned a weight dynamically calculated from their *thematic reputation*—a measure of their demonstrated knowledge and credibility in specific domains (e.g., technology, policy, or community welfare). Unlike static reputation systems, this weight evolves through peer evaluations, verified contributions, and the accuracy of past decisions, ensuring that influence aligns with competence. Building on the *Torre Protocol*’s PageRank-inspired recommendation weights, which prioritized endorsements from credible sources (Torrenegra, 2018), thematic reputation in this protocol is both domain-specific and decay-adjusted, requiring ongoing engagement to maintain influence. This approach mitigates the risk of entrenched power—seen in representative democracy’s election cycles (Hirst, 1990)—while rewarding meritocratic participation, a concept validated by the *Google Votes* experiment where delegated votes flowed to trusted experts (Hardt & Lopes, 2015).

The second pillar, *weighted vote delegation*, extends the liquid democracy model tested in *Google Votes*, where 3.6% of 87,000 votes over three years were delegated, with peaks like the 4.7% in the 2013 Food Fair demonstrating scalability (Hardt & Lopes, 2015). Participants may delegate their voting power to others with higher thematic reputation in a given domain, enhancing flexibility for those lacking time or expertise. Unlike traditional representative systems, delegation here is modular, revocable, and transitive—votes can cascade through multiple delegates—yet weighted to prevent disproportionate power accumulation. A delegate’s influence is capped and proportional to their reputation, ensuring that delegation amplifies expertise without replicating the rigid hierarchies of elected representation. This fluidity eliminates election-cycle distortions, as seen in *Google Votes* where delegation advertisements fostered real-time trust networks, and empowers participants to adapt their proxies dynamically.

The third pillar, *bridging strategies*, addresses a critical gap in prior systems: the need for consensus across diverse perspectives. Inspired by Ovadya’s (2022) concept of bridging-based ranking to reduce societal division, the protocol employs algorithms that identify heterogeneous voter groups—based on voting patterns, affiliations, or demographics—and enhance the weight of decisions supported across these divides. This counters the homogeneous majority bias observed in traditional voting and even in *Google Votes*, where food-related issues dominated due to universal appeal (Hardt & Lopes, 2015). By rewarding votes that bridge gaps, the protocol ensures outcomes reflect a broader societal good, not just the loudest voices. For instance, a policy decision might gain weight if endorsed by technologists, policymakers, and community advocates alike, fostering inclusivity over polarization.

Blockchain underpins this system, providing a decentralized ledger for transparency and integrity akin to *Torre Protocol*’s approach (Torrenegra, 2018). All votes, delegations, and reputation assessments are recorded immutably, with participants authorizing applications (storers and retrievers) to interact with their data. This mirrors *Google Votes*’ integration with Google+ for identity and discussion (Hardt & Lopes, 2015), but extends it with cryptographic security and auditability. Nodes (miners) maintain the network, calculating weights and processing transactions, while tokens incentivize their efforts without compromising voter autonomy—unlike *Torre Protocol*, where tokens also governed the network, here they primarily reward infrastructure support.

The protocol’s practical applications are vast. In DAOs, it enables governance where technical experts guide code updates while community voices shape broader goals. In public consultations, it ensures policies reflect diverse stakeholder input with expert validation. In community platforms, it elevates informed debates over populist noise. Early experiments like *Google Votes*—with 20,000 users and 370 issues—proved liquid democracy’s viability within a corporate social network (Hardt & Lopes, 2015), while *Torre Protocol* demonstrated reputation portability’s empowerment potential (Torrenegra, 2018). The *Dynamic Voting Protocol* combines these strengths, adding bridging to scale decision-making across larger, more varied groups. Its ultimate goal is to empower participants with control over their influence, ensure decisions serve the collective good, and establish a meritocratic, inclusive framework for the decentralized era.

---

## 3. Main Components

### 3.1. Voter Profiles

Voter profiles form the foundational data structure of the *Dynamic Voting Protocol*, encapsulating each participant’s identity, thematic reputation, voting history, and delegation preferences within a decentralized, blockchain-based framework. These profiles enable the protocol to assign dynamic voting weights, facilitate weighted delegation, and support bridging strategies, all while adhering to privacy requirements such as those in Colombia, where votes must remain secret despite the need to link voter identity to votes for delegation purposes. Drawing from the *Torre Protocol*’s structured bios (Torrenegra, 2018) and *Google Votes*’ voter-centric dashboards (Hardt & Lopes, 2015), voter profiles balance transparency, auditability, and confidentiality through cryptographic techniques and modular design.

Each voter profile is uniquely identified by a cryptographic account ID, ensuring that identity is verifiable yet pseudonymized on the public ledger. This mirrors *Torre Protocol*’s use of account IDs tied to public keys (Torrenegra, 2018), but extends it to accommodate voting-specific needs. The profile contains several key components:

- **Thematic Reputation Scores**: A set of domain-specific reputation values (e.g., technology, governance, social policy), calculated from peer evaluations, verified contributions, and past voting accuracy. These scores, ranging from 0 to 1 with a cap to prevent dominance, determine the base weight of a voter’s influence in a given domain. Inspired by *Torre Protocol*’s recommendation weights, which prioritized endorsements from credible sources (Torrenegra, 2018), reputation here decays over time unless refreshed by active participation, ensuring ongoing meritocracy.
  
- **Voting History**: A record of votes cast or delegated, stored in an encrypted form to comply with Colombia’s secret voting mandate. Unlike *Google Votes*, where all votes were visible to Googlers for transparency (Hardt & Lopes, 2015), this protocol uses zero-knowledge proofs (ZKPs) to pair a voter’s identity with their vote without revealing the vote’s content publicly. This allows delegates to verify delegated voting power while preserving ballot secrecy.

- **Delegation Preferences**: A list of delegates per thematic category (e.g., “policy” or “technology”), specifying to whom a voter has delegated their vote and under what conditions (e.g., revocable, category-specific). This builds on *Google Votes*’ category-based delegation—where 3.6% of 87,000 votes were delegated, peaking at 4.7% in the 2013 Food Fair (Hardt & Lopes, 2015)—but enhances flexibility with weighted, transitive delegation capped to maintain balance.

- **Connections**: Reciprocal relationships with other voters, akin to *Torre Protocol*’s connections (Torrenegra, 2018), forming a trust network that informs reputation assessments and delegation chains. These connections are optional but can amplify a voter’s influence through transitive delegation paths.

To reconcile Colombia’s secret voting requirement with delegation, the protocol employs a hybrid privacy model inspired by the *Google Votes* "Golden Rule of Liquid Democracy" (Hardt & Lopes, 2015), adapted for stricter confidentiality. Votes are encrypted using the voter’s public key, with only the voter and their chosen delegate (if any) able to decrypt the vote via a shared secret or ZKP-based verification. This ensures that:

- **Secrecy**: The public ledger records only the encrypted vote and its weight, not its direction (e.g., "yes" or "no"), satisfying Colombian legal standards.
- **Delegation**: Delegates can verify the voter’s identity and weight contribution without accessing the vote’s content unless explicitly authorized, enabling transitive delegation chains (e.g., Voter A → Voter B → Voter C) while preserving privacy.
- **Auditability**: Zero-knowledge proofs allow nodes to confirm that votes are valid and linked to verified identities without revealing sensitive data, maintaining the blockchain’s integrity.

For example, consider a voter, Ana, participating in a DAO governance vote on a technical upgrade. Her profile lists a thematic reputation of 0.8 in "technology" based on prior contributions, encrypted votes from past decisions, and a delegation to Carlos (reputation 0.9) for technical issues. Ana’s vote is encrypted and recorded on the blockchain with a ZKP proving her identity and weight (0.8 if direct, or delegated to Carlos with a proportional adjustment). Carlos, as her delegate, sees only that he receives Ana’s weighted contribution (e.g., 0.64, assuming an 80% delegation factor), not her specific choice, unless she opts for transparency. This preserves Ana’s ballot secrecy while enabling Carlos to aggregate her influence into his vote, which may further delegate to another expert.

Voter profiles are managed through storers—applications authorized by users to update data on the blockchain—mirroring *Torre Protocol*’s storer role (Torrenegra, 2018). Updates to reputation, delegations, or connections are signed with the voter’s private key, ensuring authenticity. The profile’s modular structure allows flexibility: new thematic categories can be added, reputations recalibrated, and delegations adjusted dynamically, supporting the protocol’s adaptability across contexts like DAOs, public policy, or community governance. By pairing identity with votes cryptographically, the *Dynamic Voting Protocol* upholds Colombia’s privacy standards while unlocking the power of liquid democracy, ensuring that expertise drives decisions without compromising voter autonomy or trust.

### 3.2. Reputation Assessments

Reputation assessments are the cornerstone of the *Dynamic Voting Protocol*, providing the mechanism to calculate thematic reputation scores that determine each voter’s dynamic voting weight. These assessments ensure that influence in decision-making reflects expertise, credibility, and active contribution within specific domains (e.g., technology, governance, community welfare), fostering a meritocratic system. Drawing from the *Torre Protocol*’s recommendation weight system (Torrenegra, 2018) and the delegation-driven trust networks of *Google Votes* (Hardt & Lopes, 2015), this protocol refines reputation evaluation to balance accuracy, transparency, and privacy, while incorporating safeguards against abuse and aligning with Colombia’s requirement for secret voting.

Thematic reputation is a composite score, ranging from 0 to 1, calculated for each voter across distinct categories relevant to the voting context. The assessment process integrates three primary inputs, each weighted and verified to ensure reliability:

- **Peer Evaluations**: Voters can assess others’ expertise in specific domains, submitting ratings (e.g., 0 to 1) accompanied by justifications, such as references to past contributions or decisions. Inspired by *Torre Protocol*’s public recommendations (Torrenegra, 2018), these evaluations are recorded on the blockchain, but unlike Torre’s fully public model, they are encrypted to protect voter privacy—only the evaluated voter and authorized delegates (if any) can decrypt them using zero-knowledge proofs (ZKPs). A voter’s peer evaluation score is the average of received ratings, weighted by the evaluators’ own reputation in the same domain, ensuring credibility cascades through the network. For example, if Ana (reputation 0.8) rates Carlos (reputation 0.9) at 0.85 in "technology," Carlos’s score benefits more than if rated by a novice (reputation 0.2).

- **Verified Contributions**: Objective records of a voter’s tangible contributions—such as code commits in a DAO, policy proposals in a consultation, or community initiatives—enhance reputation. These are akin to *Torre Protocol*’s verified experiences (Torrenegra, 2018), where shared professional history bolstered credibility. Contributions are submitted via storers, validated by nodes through predefined criteria (e.g., impact metrics, peer endorsements), and assigned a contribution score (0 to 1). For instance, a voter who authored a successful DAO upgrade might earn a 0.7 in "technology," verified by community consensus without revealing vote-specific details, preserving secrecy.

- **Past Voting Accuracy**: The protocol assesses the alignment of a voter’s past decisions with successful outcomes, a novel metric absent in *Torre Protocol* but echoing *Google Votes*’ meritocratic delegation trends (Hardt & Lopes, 2015). Accuracy is measured by comparing encrypted votes to objective results (e.g., a DAO proposal’s implementation success), using ZKPs to maintain ballot secrecy while proving congruence. A voter consistently supporting effective decisions earns a higher accuracy score (0 to 1), calculated as a rolling average over a defined period (e.g., 12 months). This incentivizes informed participation without disclosing individual votes publicly.

The composite reputation score \( Rt \) for a theme \( t \) is computed as:

![image](https://github.com/user-attachments/assets/22e679e4-32d2-4d21-a493-27b7522d5074)


Where:
- Rt: Thematic reputation score for a specific theme ( t ) (ranges from 0 to 1).
- Et: Peer evaluation score for theme ( t ), calculated as the weighted average of ratings received from peers, where each rating is weighted by the evaluator’s reputation in ( t ) (ranges from 0 to 1).
- Ct: Contribution score for theme ( t ), derived from the sum of verified contributions in ( t ) (ranges from 0 to 1).
- At: Accuracy score for theme ( t ), based on the alignment of past encrypted votes with successful outcomes, computed as a rolling average (ranges from 0 to 1).
- w1,w2+,w3: Configurable weights for peer evaluations, contributions, and accuracy, respectively, summing to 1 (e.g., 

To prevent stagnation, reputation decays over time (e.g., 5% monthly) unless refreshed by new evaluations, contributions, or votes, mirroring *Torre Protocol*’s scarcity principle (Torrenegra, 2018). A cap (e.g., 0.9) limits dominance, ensuring no single voter monopolizes influence—a lesson from *Google Votes*, where delegation concentrated power among trusted experts (Hardt & Lopes, 2015).

**Privacy and Delegation Compatibility**: In Colombia, ballot secrecy mandates that vote content remain confidential. Reputation assessments comply by encrypting all inputs—evaluations, contributions, and voting records—on the blockchain. ZKPs allow nodes to verify these inputs’ validity (e.g., that Ana rated Carlos, or Carlos voted) without exposing specifics, enabling delegates to aggregate weights (e.g., Ana’s 0.8 contributes to Carlos’s total) while preserving secrecy. This adapts *Google Votes*’ "Golden Rule" (Hardt & Lopes, 2015)—where voters saw delegated actions—into a privacy-first model where only the voter and delegate access relevant data.

**Safeguards Against Manipulation**: To counter Sybil attacks or inflated ratings, the protocol:
- Requires verifications (similar to *Torre Protocol*’s three-verifier rule) for initial reputation seeding.
- Applies a reputation-weighted dampening factor to peer evaluations, reducing the impact of low-reputation voters.
- Uses anomaly detection (e.g., clustering algorithms) to flag coordinated rating schemes, penalizing offenders with temporary reputation reductions.

For example, Juan, a new DAO voter, earns an initial "technology" reputation of 0.3 from verified code commits. Peers with reputations of 0.7 and 0.5 rate him 0.8 and 0.6, yielding an \( E_t \) of 0.73 (weighted average). His accuracy \( A_t \) is 0.5 based on past votes, and with weights \( w_1 = 0.4 \), \( w_2 = 0.3 \), \( w_3 = 0.3 \), his \( R_t = 0.4 \cdot 0.73 + 0.3 \cdot 0.3 + 0.3 \cdot 0.5 = 0.592 \). Over time, Juan’s score decays unless he contributes further, ensuring active engagement.

Reputation assessments thus empower the protocol to elevate expertise, support delegation, and maintain trust, all while respecting privacy constraints like Colombia’s. They bridge *Torre Protocol*’s professional credibility with *Google Votes*’ practical delegation, creating a robust, scalable system for informed collective governance.

### 3.3. Vote Delegation

Vote delegation is a transformative feature of the *Dynamic Voting Protocol*, empowering participants to transfer their voting power to others with greater expertise or alignment, thereby enhancing scalability and flexibility in collective decision-making. This mechanism allows voters to delegate their votes either globally across all decisions or selectively for specific policy domains (e.g., technology, governance, social welfare), blending the fluidity of liquid democracy with thematic precision. Drawing from *Google Votes*’ category-based delegation—where 3.6% of 87,000 votes were delegated, peaking at 4.7% in the 2013 Food Fair (Hardt & Lopes, 2015)—and *Torre Protocol*’s trust-based recommendation networks (Torrenegra, 2018), this protocol refines delegation to balance voter autonomy, meritocracy, and adaptability within a blockchain framework, suitable for diverse global contexts.

The delegation process is modular, revocable, and transitive, enabling votes to flow through multiple delegates while maintaining a scalable design that accommodates varying network sizes—from small communities to entire nations. Voters specify delegates via their profiles, with two primary options:

- **Global Delegation**: Assigning all voting power to a single delegate across all decisions, ideal for participants seeking comprehensive representation. For example, Ana might delegate globally to Carlos, trusting his judgment universally.
- **Domain-Specific Delegation**: Assigning voting power to different delegates for distinct policy domains, leveraging thematic reputation scores. Ana could delegate "technology" votes to Carlos (reputation 0.9) and "social welfare" votes to Maria (reputation 0.85), optimizing influence by expertise.

**Delegation Mechanics**:  
Delegation is recorded on the blockchain as a directed link from delegator to delegate, annotated with scope (global or domain-specific) and a delegation factor \( D \) (0 to 1), which adjusts the transferred weight. The effective weight delegated is calculated as:

\[ W_{\text{delegated}} = R_t \cdot D \]

Where:
- \( R_t \): The delegator’s thematic reputation in the relevant domain (or average across domains for global delegation), ranging from 0 to 1.
- \( D \): Delegation factor, defaulting to 0.8 (configurable by governance), ensuring a portion of influence remains with the delegator to encourage active participation.

A delegate’s total voting weight combines their own reputation with delegated contributions:

\[ W_{\text{effective}} = R_t + \sum W_{\text{delegated}} \]

To prevent excessive power concentration—unlike *Google Votes*’ uncapped delegation (Hardt & Lopes, 2015)—a maximum effective weight (e.g., 2.0) is enforced, adjustable by governance to suit community needs.

**Privacy and Transparency Flexibility**:  
The protocol offers a universal approach to privacy, accommodating diverse global standards. Votes and delegation records can be:
- *Fully Transparent*: Visible to all participants, as in *Google Votes* (Hardt & Lopes, 2015), fostering trust through openness.
- *Partially Private*: Visible only to the delegator and delegate, using encryption and zero-knowledge proofs (ZKPs) to verify weights without revealing vote content, inspired by *Torre Protocol*’s public-yet-secure data model (Torrenegra, 2018).
- *Configurable*: Communities can set privacy levels via governance, balancing transparency (e.g., for accountability in DAOs) with confidentiality (e.g., for sensitive public consultations).

For instance, Ana delegates "technology" votes to Carlos. Her vote is encrypted, and Carlos receives a weight certificate (e.g., \( 0.8 \cdot 0.8 = 0.64 \)) via ZKP, aggregating it into his vote without necessarily seeing her choice, unless the community opts for full transparency. Voters can override delegations by voting directly, nullifying the delegate’s action for that issue, with the override logged accordingly.

**Process Steps**:  
1. **Initiation**: A voter selects a delegate via their profile, specifying scope (global or domain-specific) and signing the delegation with their private key.
2. **Recording**: Storers submit the delegation to the blockchain, where nodes validate the voter’s identity and reputation, applying the chosen privacy model.
3. **Execution**: For an issue (e.g., a governance proposal), the delegate casts a vote, incorporating delegated weights unless overridden. Nodes compute the effective weight, ensuring accuracy.
4. **Revocation or Adjustment**: Voters can revoke or reassign delegation anytime, with changes recorded immutably, echoing *Google Votes*’ real-time adaptability (Hardt & Lopes, 2015).
5. **Feedback**: Delegates receive notifications of aggregated weights, and delegators access logs of their influence (encrypted or public, per settings), reinforcing trust.

**Safeguards**:  
- *Adaptive Transitivity Limits*: Delegation chains are capped dynamically based on network size and density (e.g., 3 hops for small groups, scaling to 5-6 for national populations), set by governance to ensure broad representation while controlling complexity. This adapts *Torre Protocol*’s open-ended trust model (Torrenegra, 2018) to larger scales, covering millions with hubs reachable within 5 hops (Watts & Strogatz, 1998).
- *Sybil Resistance*: Delegates must have verified profiles with minimum reputation thresholds, ensuring credibility.
- *Rate Limits*: Frequent delegation changes incur cooldowns to deter gaming, enhancing stability.

For example, in a national DAO with 50 million voters, Juan (reputation 0.6 in "finance") delegates globally to Sofia (reputation 0.9). Governance sets a 5-hop limit, connecting Juan to Sofia via intermediaries if needed (e.g., Juan → B → C → D → Sofia), yielding \( 0.9 + 0.6 \cdot 0.8 = 1.38 \), capped at 2.0. Juan can override specific votes, retaining control. This scalable design extends *Google Votes*’ 20,000-user success (Hardt & Lopes, 2015) to global contexts, empowering voters universally.

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

Intellectual Property

   This work has not been validated or claimed as a novelty, all of the
   Intellectual Property Rights or other rights that might be claimed to
   pertain to the implementation or use of the technology described in
   this document or the extent to which any license under such rights
   might or might not be available; nor does it represent that it has
   made any independent effort to identify any such rights.  Information
   on the procedures with respect to rights in RFC documents can be
   found in BCP 78 and BCP 79 of the Internet Research Task Force.

   The writers invites any interested party to bring to its attention any
   copyrights, patents or patent applications, or other proprietary
   rights that may cover technology that may be required to implement
   this standard.  Please address the information to jalban.arq@gmail.com
