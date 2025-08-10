# RFC: Dynamic Voting Protocol: A Decentralized Decision-Making System with Adaptive Safeguards

**Category:** Experimental - Draft  
**Obsoletes:** P/1  

## Status of this memo

This document specifies an experimental, adaptive system for decentralized decision-making. It incorporates findings from systemic simulations to address potential failure modes such as meritocratic tyranny. Discussion and suggestions for improvements are encouraged. Distribution of this memo is unlimited.

## Abstract

The Dynamic Voting Protocol is a decentralized system designed to enhance collective decision-making by rewarding informed participation and penalizing manipulation. Initial designs, while promoting meritocracy, were found to be vulnerable to systemic biases that could suppress minority voices, a phenomenon identified as "meritocratic tyranny." This revised specification introduces a fourth core pillar: adaptive safeguards. These mechanisms, including a dynamic reputation floor and a decaying contribution bonus, are governed by on-chain metrics of system health (e.g., the Gini coefficient of reputation distribution). The protocol now aims to create a resilient, fair, and effective voting system that balances merit with inclusion, ensuring that expertise guides outcomes without silencing diverse perspectives.

## Contents

1. Background  
2. Protocol Overview  
3. Main Components  
   3.1. Voter Profiles  
   3.2. Reputation Assessments  
      3.2.1. [NEW] Adaptive Safeguards: The Equity Thermostat  
   3.3. Vote Delegation  
   3.4. Bridging Strategies  
   3.5. Verifications  
   3.6. Connections  
   3.7. Decentralized Network  
   3.8. Participants  
   3.9. Incentives  
   3.10. Governance  
4. Vote Weight and Reputation Dynamics  
   4.1. Formula  
   4.2. [UPDATED] Adaptive Reputation Dynamics  
5. Privacy, Authentication, and Encryption  
6. Data Structures  
7. Protocol Sketch  
8. Rewards for Nodes (Miners)  
9. Blockchain Technology  
10. Protection Against Abuse and Manipulation  
    10.1. [NEW] Systemic Bias and Adaptive Mitigation  
11. Applications  
12. [UPDATED] Open Questions and Governance Challenges  
13. Related Work  
14. Acknowledgments  
15. References  

## 1. Background

Collective decision-making has historically been a cornerstone of organized societies, yet it has perpetually grappled with challenges such as manipulation by uninformed or coordinated factions, opacity in process, and the exclusion of diverse perspectives. For centuries, decisions rested with centralized authorities, often rendering outcomes inefficient and unrepresentative. The advent of democratic systems, rooted in the Greek ideal of dēmokratía ("rule of the people"), promised broader participation, but traditional mechanisms like simple majority rule frequently sidelined expertise and marginalized minority voices (Liddell & Scott, 1889). The 20th and 21st centuries introduced digital platforms that amplified these issues—social media polls and corporate decision tools often prioritized engagement over substance, deepening divisions and eroding trust (Ovadya, 2022). Blockchain technology, pioneered by systems like Bitcoin (Nakamoto, 2008) and Ethereum (Buterin, 2013), offered a transformative solution through immutable, transparent ledgers, yet its application alone does not inherently ensure informed participation or bridge societal divides.

Significant strides in decentralized systems provide a foundation for addressing these gaps. The Torre Protocol (Torrenegra, 2018) emerged as a pioneering effort to liberate professional reputation from the silos of centralized platforms like LinkedIn, Uber, and Upwork. These platforms, while facilitating socioeconomic mobility through networks of recommendations, restricted data portability—LinkedIn, for instance, pursued legal action against entities accessing user-authorized data (Conger, 2016), and freelancing marketplaces prevented users from transferring earned reputations, forcing them to restart upon switching services (Torrenegra, 2018). Torre countered this by proposing a blockchain-based, decentralized reputation network where individuals controlled their curricula vitae and recommendations. Its novel recommendation weight system, inspired by PageRank (Page, 1998), assigned greater influence to endorsements from highly recommended individuals, ensuring trustworthiness through scarcity and public verifications. While Torre focused on professional mobility, its principles of weighted credibility and decentralization laid crucial groundwork for broader decision-making applications.

Parallel innovations in voting systems further inform this evolution. The Google Votes experiment (Hardt & Lopes, 2015), conducted within Google’s internal Google+ network from March 2012 to February 2015, tested liquid democracy—a hybrid of direct and representative democracy where voters could delegate their votes to trusted peers. Over three years, 20,000 Googlers engaged with the system, creating 370 issues and casting over 87,000 votes, including delegated ones. Food-related decisions dominated, with 150 issues and 73,000 votes, reflecting high engagement due to their universal appeal within Google’s culture. Notably, 3.6% of votes were delegated, a modest yet significant uptake for a workforce new to liquid democracy. A standout case was the 2013 Mountain View Microkitchen Food Fair, where 4,600 Googlers cast 62,000 votes across 25 snack categories, with 4.7% delegated—a higher proportion than the average—demonstrating delegation’s potential in large-scale, practical settings. The experiment’s success, evidenced by 175,000 pageviews and adoption of results in microkitchen stocking, underscored liquid democracy’s scalability when paired with social networking tools, though it highlighted challenges like initial user education and limited mobile engagement (8.5% of votes) (Hardt & Lopes, 2015).

The Dynamic Voting Protocol synthesizes these advancements, extending Torre’s reputation weighting and Google Votes’ delegation into a comprehensive decision-making framework. It aligns with the Technology and Public Purpose (TAPP) Project principles, which, though not formally affiliated, resonate deeply:

1. Technology’s advance is inevitable, and it often brings progress for some. Yet, progress for all demands proactive solutions to dilemmas like uninformed voting or polarized outcomes, as seen in traditional systems and early digital experiments.

2. There is no silver bullet. Effective governance requires blending tech-sector innovation—like Torre’s blockchain approach and Google Votes’ social integration—with regulatory oversight, fostering trust through transparency and collaboration.

3. Public purpose-driven innovation relies on inspiring tech leaders. This protocol builds on Torre’s empowerment ethos and Google Votes’ practical insights to equip future stewards with tools for sustainable, inclusive decisions.

Unlike Torre’s focus on professional reputation or Google Votes’ corporate scope, the Dynamic Voting Protocol targets collective governance across domains—DAOs, public consultations, and beyond. It introduces dynamic voting weights based on thematic expertise, flexible delegation inspired by liquid democracy, and bridging strategies to ensure consensus across diverse groups, aiming for a more equitable and effective decision-making paradigm in a decentralized era.

## 2. Protocol Overview

The Dynamic Voting Protocol is a decentralized, blockchain-based framework designed to revolutionize collective decision-making. While initial versions focused on three pillars—thematic reputation, vote delegation, and bridging strategies—simulations revealed a critical vulnerability: a tendency toward meritocratic tyranny, where the self-reinforcing success of a majority can systematically suppress the influence of minority or new participants, regardless of the quality of their contributions. This finding necessitates the introduction of a fourth, crucial pillar: Adaptive Safeguards.

The protocol's core function remains to weight votes based on demonstrated expertise. However, it now incorporates a dynamic "equity thermostat" that continuously monitors the health of the system. Using on-chain metrics like the Gini coefficient of reputation distribution, the protocol automatically adjusts its own rules to prevent both systemic suppression and "equity over-correction"—a state where merit is diluted in the name of fairness. These safeguards ensure the system remains both effective (rewarding expertise) and fair (providing genuine opportunity for all voices to emerge).

This adaptive approach moves beyond a static set of rules to create a resilient, self-regulating ecosystem for governance, aiming to establish a truly meritocratic, inclusive, and robust framework for the decentralized era.

## 3. Main Components

### 3.1. Voter Profiles

Voter profiles form the foundational data structure of the Dynamic Voting Protocol, encapsulating each participant’s identity, thematic reputation, voting history, and delegation preferences within a decentralized, blockchain-based framework. These profiles enable the protocol to assign dynamic voting weights, facilitate weighted delegation, and support bridging strategies, all while adhering to privacy requirements. Drawing from the Torre Protocol’s structured bios (Torrenegra, 2018) and Google Votes’ voter-centric dashboards (Hardt & Lopes, 2015), voter profiles balance transparency, auditability, and confidentiality through cryptographic techniques and modular design.

Each voter profile is uniquely identified by a cryptographic account ID, ensuring that identity is verifiable yet pseudonymized on the public ledger. The profile contains several key components:

* **Thematic Reputation Scores:** A set of domain-specific reputation values (e.g., technology, governance, social policy), calculated from peer evaluations, verified contributions, and past voting accuracy. These scores, ranging from 0 to 1 with a cap to prevent dominance, determine the base weight of a voter’s influence in a given domain.

* **Voting History:** A record of votes cast or delegated, which can be stored in an encrypted form to comply with jurisdictional requirements for ballot secrecy. The protocol supports zero-knowledge proofs (ZKPs) to pair a voter’s identity with their vote without revealing the vote’s content publicly.

* **Delegation Preferences:** A list of delegates per thematic category, specifying to whom a voter has delegated their vote and under what conditions.

* **Connections:** Reciprocal relationships with other voters, forming a trust network that informs reputation assessments and delegation chains.

### 3.2. Reputation Assessments

Reputation assessments are the cornerstone of the protocol, providing the mechanism to calculate thematic reputation scores. The assessment process integrates three primary inputs:

* **Peer Evaluations:** Voters can assess others’ expertise in specific domains. A voter’s peer evaluation score is the average of received ratings, weighted by the evaluators’ own reputation in the same domain.

* **Verified Contributions:** Objective records of a voter’s tangible contributions—such as code commits in a DAO or policy proposals in a consultation—enhance reputation.

* **Past Voting Accuracy:** The protocol assesses the alignment of a voter’s past decisions with successful outcomes, incentivizing informed participation.

#### 3.2.1. Adaptive Safeguards: The Equity Thermostat

To counteract the identified risk of meritocratic tyranny, the protocol implements a set of autonomous, adaptive safeguards. These mechanisms are not static rules but are dynamically controlled by the overall state of the network, functioning as an "equity thermostat" that balances fairness and merit.

1. **Dynamic Reputation Floor (R_min):** All participants are guaranteed a minimum level of reputation. However, this floor is not fixed. Its value is algorithmically tied to a real-time measure of network inequality, such as the Gini coefficient of the total reputation distribution.

   * **Mechanism:** If the Gini coefficient rises above a pre-defined governance threshold (e.g., 0.4), indicating growing inequality, the R_min value automatically increases, providing a stronger safety net for low-reputation participants.

   * **Self-Correction:** If the system becomes too egalitarian (Gini coefficient drops below a lower threshold), the R_min value decreases, allowing for greater differentiation based on merit.

2. **Decaying Contribution Bonus (B_velocity):** To overcome the initial barrier to entry for new participants, the protocol provides a temporary reputation bonus for early contributions. This bonus is designed to decay over time.

   * **Mechanism:** A new participant might receive a 1.5x multiplier on reputation gains for their first three contributions, a 1.2x multiplier for the next five, and so on, until the bonus phases out completely.

   * **Purpose:** This provides a significant but temporary boost, enabling newcomers to become visible without permanently inflating their reputation or devaluing long-term, sustained contributions.

The parameters governing these safeguards (e.g., the Gini threshold, the decay rate of the bonus) are themselves subject to change via the protocol's governance mechanism, ensuring the community can fine-tune the balance between merit and equity as the network evolves.

### 3.3. Vote Delegation

Vote delegation is a transformative feature, empowering participants to transfer their voting power to others with greater expertise or alignment. This mechanism allows voters to delegate their votes either globally across all decisions or selectively for specific policy domains. The delegation process is modular, revocable, and transitive, enabling votes to flow through multiple delegates while maintaining a scalable design.

### 3.4. Bridging Strategies

Bridging algorithms identify diverse voter groups and enhance vote weights for decisions supported across these groups, promoting inclusivity and rewarding consensus over polarization.

### 3.5. Verifications

Crowdsourced, public verifications prevent fake accounts and ensure participant authenticity.

### 3.6. Connections

Voters can form reciprocal connections, creating a network that informs reputation and delegation dynamics.

### 3.7. Decentralized Network

The protocol operates on a blockchain, ensuring data integrity and transparency while enabling permissionless innovation.

### 3.8. Participants

* **Voters (End-Users):** Create profiles, cast votes, delegate voting power, and authorize data access.

* **Storers:** Interface between voters and the blockchain, adding and updating data.

* **Nodes (Miners):** Maintain the ledger, calculate vote weights, and process transactions, earning rewards.

* **Retrievers:** Access and publish voter data, enabling applications to utilize the protocol.

### 3.9. Incentives

Incentives encourage honest participation and network maintenance through tokens (for nodes) and reputation gains (for voters).

### 3.10. Governance

Governance is split between token holders and active voters, with decisions made via weighted voting. This includes the governance of the adaptive safeguards themselves.

## 4. Vote Weight and Reputation Dynamics

### 4.1. Formula

The weight of a vote (W_v) is calculated as:  
W_v = R_t * D * B * Q  

* R_t: Thematic reputation, subject to adaptive dynamics.  
* D: Delegation factor.  
* B: Bridging factor.  
* Q: Quality score (based on justification rigor).  

### 4.2. Adaptive Reputation Dynamics

The evolution of a participant's reputation is governed by a combination of direct contributions and system-wide adaptive dynamics, ensuring both meritocratic growth and systemic health.

* **Reputation Decay:** As in the original design, reputation scores decay slowly over time to incentivize continuous participation.

* **Contribution Gains:** Reputation is primarily gained through positive peer evaluations, verified contributions, and a track record of accurate voting.

* **Adaptive Adjustments:** The final reputation score in any given epoch is subject to the Adaptive Safeguards (Section 3.2.1). The B_velocity bonus is applied to the gains of new users, and the final score is never allowed to drop below the current R_min value, which is itself dynamically calculated based on the system's Gini coefficient. This ensures that while reputation is earned, the opportunity to earn it is never fully extinguished by systemic pressures.

## 10. Protection Against Abuse and Manipulation

### 10.1. Systemic Bias and Adaptive Mitigation

Beyond individual manipulation (e.g., Sybil attacks), the most significant threat to the protocol's integrity is systemic bias, specifically meritocratic tyranny. Simulations prove that a simple merit-based system, even if perfectly executed, can lead to feedback loops where a majority group's early success grants them the influence to win all subsequent decisions, effectively silencing minority perspectives.

The Adaptive Safeguards detailed in Section 3.2.1 are the primary defense against this threat. By dynamically adjusting the reputation floor and providing a decaying bonus to newcomers, the protocol actively works to:

1. Prevent systemic suppression by ensuring a baseline level of influence for all.

2. Avoid equity over-correction by making these aids responsive to the overall state of the network, rather than applying them as a blunt, static instrument.

This adaptive approach ensures the protocol remains fair and competitive over the long term.

## 11. Applications

* **DAO Governance:** Fairer voting with expert influence, resilient to capture by early majorities.

* **Public Consultations:** Transparent, representative outcomes that adapt to changing community demographics.

* **Community Debates:** Highlighting informed consensus while ensuring new ideas can emerge.

* **Policy Development:** Bridging diverse stakeholder input with a system that self-regulates for fairness.

## 12. Open Questions and Governance Challenges

The successful modeling of the adaptive safeguards has answered the critical question of whether meritocratic tyranny can be prevented. The focus now shifts to more nuanced, second-order governance challenges:

* **Governance of the Safeguards:** What is the optimal method for the community to debate and vote on the parameters of the adaptive system (e.g., the Gini threshold)? Should this require a higher-than-normal consensus?

* **Defining "Healthy" Inequality:** While a Gini of 0 represents perfect equality, it may not represent a perfectly effective system. What is the optimal range for the Gini coefficient that the community should target to balance merit and inclusion?

* **Meta-Reputation:** Should a separate "governance reputation" be developed for participants who show skill in tuning the protocol's adaptive parameters, distinct from their reputation in other thematic areas?

Ongoing work will focus on designing and simulating these meta-governance structures.

## 13. Related Work

* Aragon, DAOstack: Blockchain voting systems.

* Bloom, uPort: Decentralized reputation frameworks.

## 14. Acknowledgments

Thanks to contributors for their valuable feedback and to the SEI 2.3 framework for its ethical guidance in identifying and mitigating systemic risks.

## 15. References

* Nakamoto, S., 2008. Bitcoin: A Peer-to-Peer Electronic Cash System.

* Buterin, V., 2013. Ethereum Whitepaper.

* Ovadya, A., 2022. How Platform Recommendation Systems Might Reduce Division and Strengthen Democracy.

* Torrenegra, A., 2018. Torre Protocol: The People Network for Work.

* Hardt, S. & Lopes, L., 2015. Google Votes: A Liquid Democracy Experiment on a Corporate Social Network.

* Conger, K., 2016. LinkedIn Sues Mantheos For Scraping User Data. TechCrunch.

* Liddell, H. G., & Scott, R., 1889. An Intermediate Greek-English Lexicon.

## Intellectual Property

This work has not been validated or claimed as a novelty. All of the Intellectual Property Rights or other rights that might be claimed to pertain to the implementation or use of the technology described in this document or the extent to which any license under such rights might or might not be available; nor does it represent that it has made any independent effort to identify any such rights. Information on the procedures with respect to rights in RFC documents can be found in BCP 78 and BCP 79 of the Internet Research Task Force.

The writers invite any interested party to bring to its attention any copyrights, patents or patent applications, or other proprietary rights that may cover technology that may be required to implement this standard. Please address the information to jalban.arq@gmail.com.
