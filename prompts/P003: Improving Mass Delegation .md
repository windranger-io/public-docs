# Improving Mass Delegation

## Prompt

#### Scope

Prompt: Delegation function is used by many DAO tokens (COMP, UNI, BIT). We are interested in tooling to further enable/enhance one-to-many delegation (from Gnosis Safe) in a scalable, secure and cost-effective manner.

#### In Scope

- Functional one-to-many delegation solutions

- Potential to modularize (such that this would be interoperable with future plug ins and strategies)

#### Out of Scope

- Delegation policy, strategy

- Voting heuristics (vote weighting, reputation, etc).

## Submission

Please fill out this webform for submissions: [https://airtable.com/shrmYC43GewWYv3Ha](https://airtable.com/shrmYC43GewWYv3Ha)

## Guidance and Context

The items below are not exclusive lists or the defined frameworks for the solution. However, the items should be considered as part of the overall research and design exercise prior to submission of a solution.

### Current Limitations / Challenges

**Delegation Utility**

BitDAO voting is via delegated voting power (see more). This approach has certain benefits including: security as a result of distinct wallets for voting and holding assets and distribution of voting power without risk of delegates selling tokens. This also creates certain limitations. If a user has not delegated to themselves prior to the proposal on snapshot, they are not able to vote if the snapshot has already been initiated. Users with BIT in wallet balance, cannot vote without first delegating.

The following notable protocols also utilize delegated voting:

Onchain:

- Compound

- Uniswap

- Optimism

Offchain:

- Compound (with delegate by signature, though not very flexible)

#### Delegation Limitations

Current delegation is one-to-one - i.e. wallets entire holdings are delegated to a target address. Partial / array delegations are not supported.

#### Gas Costs

Current delegation solutions require individual transactions per each wallet being delegated to. This linear cost model results in prohibitively high gas costs, especially when considering scenarios where a DAO desires to delegate to a large number of contributors.

#### Time Consuming / Error-Prone

Delegation and ongoing maintenance of delegate addresses are time intensive (accounting for new/departing DAO members/delegates). Delegation and delegate management is time-consuming, manual and error-prone. No current solutions have accompanying UIs, change logs, etc.

#### Sweeping (Asset Recall)

The recalling of delegated funds suffer from issues stated above, specifically cost and effort.

## Guidance

#### Vote Strategy

Delegation mechanics are used by many DAOs. An existing Snapshot vote strategy recognizes this style of delegation ([link](https://github.com/snapshot-labs/snapshot-strategies/tree/master/src/strategies/comp-like-votes)). Ideally, tools should leverage this, enabling widespread adoption across the DAO landscape.

#### Gnosis Safe

Gnosis Safe is the gold standard for Organizational Multi Sigs and DAO treasuries. When delegating to large teams, the preferred approach is the controlling account is a Gnosis Safe address (with customizable owner policy). Solutions should consider building this as a a Gnosis plug in or as part of the [Gnosis Guild](https://twitter.com/GnosisGuild) Zodiac Suite

#### Cost Effective

Reduction of costs and ability to create economies of scale to enable mass delegation in a cost effective manner. This could potentially include (see Offchain Merkle Delegation Contract exploration below).

#### Ease Existing UX Pain Points

Improve the experience for users, decreasing effort, time and technical knowledge required to delegate, manage and sweep funds. A basic UI would ideally guide the user through the process, save information, prevent user errors, etc.

#### Account for undelegated votes from primary wallet

Take inspiration from Compound Finance’s comp-like voting delegation while also crediting accounts for non-delegated token balances ([github link](https://github.com/snapshot-labs/snapshot-strategies/tree/master/src/strategies/comp-like-votes-inclusive)). The key risk to avoid is the potential for double counting of votes

## Explorations and Ideation

#### Gnosis Safe - Manual Delegation

Delegation through the manual setting up of multiple Gnosis Safes (with shared/similar owners), through which each safe can delegate to target addresses on a one-to-one basis. While functionally sound, this process is manual and not practically scalable beyond 10-20 delegates.

#### Script With Private Key Hot Wallet

Script through which tokens are distributed via disperse.app, then uses each wallet’s private key to delegate to target addresses. This solution suffers from several of the stated challenges above.

#### Offchain Merkle Delegation Contract

One potential approach that can be taken for a negligible gas cost approach is an oracle based one where delegations are collated into merkle trie nodes and the root is published on chain for every delegation cycle. In order to maintain trust for each update a changelog should be published along with instructions for individuals to be able to generate the merkle trie root from the data.

    Example:

    	Proportional Trie Structure:

    	Each node: _keccak256(Address, index)_

    	Fixed Amount Trie Structure:

    	Each node: keccak256(Address, index, amount)

    	Weighted Trie Structure:

    	Each node: keccak256(Address, index, weight)

This would require the deployment of a simple middleware server as well (CRUD DB) with a simple api for updating containing the following elements:

- Add Delegate To Trie (PUT)
- Construct Trie Root (GET)

Benefits of this approach include: lower gas costs, this would be an immediate solution for offchain voting (via Snapshot) as well as forward compatible for onchain voting

Considerations include: slightly higher gas costs for delegates if used for onchain voting as well as the development of a new Snapshot strategy to read and transmit data from the contract to the snapshot application.

# References

COMP token delegation function

- [https://compound.finance/docs/governance#delegate](https://compound.finance/docs/governance#delegate)

Delegating from a Gnosis Safe

- [https://docs.bitdao.io/litepaper-1/how-to-delegate/multisig-using-gnosis-safe](https://docs.bitdao.io/litepaper-1/how-to-delegate/multisig-using-gnosis-safe)
- [https://www.notion.so/Gnosis-Delegation-ce07dc49eecc4bfb9d044820bf26624f](https://www.notion.so/Gnosis-Delegation-ce07dc49eecc4bfb9d044820bf26624f)
