# W3F Grant Proposal


* **Project Name:** Hazelword
* **Team Name:** Hazelword team (e.g. Duo)
* **Payment Address:**  Ethereum (USDT) ：0x78c347cb184c84383d472810d81b05d91364c998


## Project Overview :page_facing_up:

If this application is in response to an RFP, please indicate this on the first line of this section.

If this is an application for a follow-up grant (the continuation of an earlier, successful W3F grant), please provide name and/or pull request of said grant on the first line of this section.

### Overview

The Internet has realized the efficient transmission of information where the concept of Internet of Everything and its application have greatly changed human life. As the next-generation "Internet of Value", blockchain is expected to deliver and exchange value as accurately, efficiently and safely as information while the digital assets based on the native blockchain system are important carriers in transmission of value.As an objective measurement of value, price is an important basic component for realizing value exchange. With the rapid development of blockchain, whether value can be exchanged at low cost safely and efficiently has become a core standard for measuring the application value of blockchain. Therefore, as it were, the measurement of application value of blockchain is inseparable from the objective measurement of assets on any chain.We expect to provide a data-driven prediction service based on the “asset-backed events” and a data-correction mechanism based on fact checking. The oracle machine could resolve fundamental problems about trusted source of data of blockchain through the mechanism of market arbitrage.

At present, the quotation mode of the oracles on the market is basically uploaded by the node and verified by voting.
As an oracle machine, Uniswap extracts the price of the transaction, and cannot confirm whether there is a spread in the transaction price of these transactions, and how big the spread, especially if there is malicious manipulation, the price deviation will be even greater.

### Project Details

**Dapp (Web test network)**
https://test.hazelword.org

**Product Architecture**

![alt Product Architecture](https://github.com/Hazelword/hzl-sol/blob/main/doc/project.png)

**Quotation Process**
Hazelword provides the idea of a multi-party game, using quotation, arbitrage verification, quote vault, price chain, trusted TEE module, security module, DAO autonomy and other modules to form a safe real-time decentralized oracle system
Hazel oracles generate oracles quotations based on protocol algorithms, where participants include bidders, verifiers, and price callers.
The quotation realization process: If the current market price is 1 DOT=20.1 USDT, then the bidder needs to transfer 10 DOT and 201 USDT to the contract. During this period, the verifier can exchange at the price given by the bidder, such as , Transfer 201 USDT to the contract to exchange 10 DOT, or transfer 10 DOT to the contract to exchange 201 USDT.

**Participant Description:**
Quoter: Participants who provide quotes, including three parts: 
1. All quote miners
2. Quote vault
3. Take orders and quote validators

Verifier: If a quotation deviates from the market price, the verifier can trade with the quotation asset to obtain the benefit of the difference. While eating the quotation of the quotation, the verifier needs to provide a compensation quotation for the quotation price as Provide more honest quotation data, making the price infinitely close to the real market price. Contains two parts: 
1. All verifiers
2. Verifier Quote vault

Quote Vault: The Quote Vault is divided into two parts
1. The Quote Vault mentioned in the appeal
2. The verifier Quote Vault, the function of changing the Quote Vault is to provide honest quotations for mining and find that the quotations that deviate from the market are corrected and profited. The function of this module is mainly in two aspects: 
       1. It is convenient for anyone to participate in the system to obtain benefits
       2. Participants and institutions jointly maintain the security of the system

TEE module: Provide reliable external prices for Quote Vault use.

Price chain: According to the mining rules, every T1 time period, all valid quotations (quotes that have not been taken) within this period of time are used to generate the final price of the block N of the transaction pair according to the weight.

Price caller: Only need to pay a certain fee or purchase a certain number of queries to get the current price of all trading pairs in the current block, and any contract or account can become a price caller.

**Quotation mining has been price verified**
Taking ETH/USDT as an example, a miner intends to quote 1ETH=2000USDT. He needs to transfer the quoted assets ETH and USDT to the quoted contract, the scale is xETH and 2000xUSDT, the commission paid is λx2000HZL, and he participates in mining according to the commission scale paid. Get HZL. Anyone can become a miner at any time, and the price and scale are independently set by him (greater than or equal to the minimum quotation unit). At the same time, the Quote Vault will use the quotation funds in the pool to automatically provide quotations according to the storage user's choice. After the miner submits the asset and price to the quotation contract, any validator believes that there is room for arbitrage at the price, and can trade ETH or USDT according to the quotation in the quotation pool 1ETH=2000USDT. This mechanism ensures that the quotation is either a fair price in the market or an equivalent price recognized by the quoter (that is, 1ETH and 2000USDT are equivalent). Of course, the verifier is two-way, and the execution power eats the quotation 1ETH=2000USDT At the same time, you need to provide your own quotation. This process is the price verification period.

Of course, during the mining cycle T1, there may be price fluctuations. Therefore, if miners want to minimize their own costs, they need to report the price that is least likely to be traded during the verification period, which means that the miners’ quotation has a certain degree of future price. For the prediction and discovery function, for the verifier, whether arbitrage depends on the deviation between the quoted price and the market equilibrium price. We call the minimum deviation of the action taken by the verifier as the minimum arbitrage space. This value depends on the length and length of the verification period. transaction cost.

**Price chain Generation**
According to the Quotation Mining Agreement, the price of a transaction pair quoted by the bidder in this T1 cycle is A1, A2, A3...AN, and the quantity is n1, n2...ni. In the agreement, the verifier is After the price of a quoter is traded, a new price needs to be forced to be quoted. For example, A2, A3 is found by the verifier to have arbitrage space, then after the transaction, a new quote will be provided B2=y1A2,B3=y2A3, of course, if other verifications feel that B3 There is also arbitrage space, then B3 will be taken and a new quotation C3=y3B3 will be provided. By analogy, a continuous price chain with T1 as the maximum quotation time interval is formed: A1—B2—C3...AN , When this time period T1 ends, it will be calculated within the changed block, so the price of the transaction pair P=∑Ai*ni/Ni

**Safety**
The Quote Vault is an important link in the security system. The TEE module will run transparent and safe code blocks to return information from multiple trusted institutions,
 and make the smallest quotation based on market conditions, mainly to maintain continuous and stable price mining. In addition, 
 The verifier Quote Vault can continuously monitor the quotations in the quotation market that do not conform to the market conditions, and accurately make arbitrage behavior.
 Theoretically verify that the amount of the Quote Vault is directly proportional to the cost of doing evil. When the value of the Quote Vault increases, the cost of doing evil will increase. 
 At the same time, anyone who finds arbitrage space will spontaneously maintain the Hazelword quotation market. For example: we set the take-to-order factor β=2, the Quote Vault p=1000ETH, the time period T1=1 minute, 
 and the initial quotation is x=10ETH, then in the case of all transactions, x1=2020ETH, x2=4040ETH, x3=8080ETH. .. By analogy, 
 the attacker will either be exposed to great arbitrage opportunities in the market (the scale increases by a series, this kind of attack is almost ineffective), 
 or continue to use extremely high-scale assets to conduct self-transactions based on market prices in order to delay The chance of price being adopted, if one block of the current chain can contain 10 transactions, 
 then about 10 blocks in 1 minute can provide one hundred valid transactions, 1010^100=2*10^300ETH, which will be a no The possible number and resistance to attack are also beyond the reach of most centralized data source oracles.
**TEE encryption oracle**
![alt tee encryption](https://github.com/Hazelword/hzl-sol/blob/main/doc/tee.png)
Application contract：On-chain applications deploy and run smart contracts on the blockchain
HazelWord Open Oracle contract：HazelWord smart contract deployed on the Polkadot blockchain
HazelWord example：A trusted HTTPS/RPC client implemented in TEE, which processes web requests and returns a certified response result
Configuration Management Service：Configure user contract permission to use service permissions and configurations
HazelWord Service：The HazelWord service management dispatch center manages HazelWord Open Oracle contracts and HazelWord instances, and dispatches Oracle contract requests to Oracle instances for execution
Web data source：The data source web server can be publicly verified without permission, or verified with permission.

![alt Contract Architecture](https://github.com/Hazelword/hzl-sol/blob/main/doc/quote-vault.png)
In order to reduce the cost of ordinary users participating in quotation, it has truly become a decentralized quotation model. HazelWord provides users with automated quotation arbitrage capabilities by providing different on-chain strategy Quote Vault, which improves user asset income while solving the initial cold start problem of the agreement, and also provides more guarantees for the safety of the Hazel agreement.

### Ecosystem Fit

In the indirect oracle, the credit risk of the node uploading the data determines the cost of attacking the data of the oracle. If 1 trillion dollars of assets are derived based on the price provided by the oracle, the credit of the oracle node should also match it. This is obviously impossible in reality. No matter what node randomness is used, it cannot be guaranteed. This is an essential problem, not a technical problem, so indirect oracles can only be used in small-scale, non-financial scenarios.


* Where and how does your project fit into the ecosystem?
* Who is your target audience (parachain/dapp/wallet/UI developers, designers, your own user base, some dapp's userbase, yourself)?
* What need(s) does your project meet?

Our early thoughts were based on Vitalik Buterin article “UNI should become an oracle token” (https://gov.uniswap.org/t/uni-should- become-an-oracle-token/11988), this article has a big idea of our project
If the quotation of the bidder deviates greatly from the true price of the market, it will give the verifier an opportunity for arbitrage. When the validator takes advantage of the deviation between the bidder and the real price for arbitrage, it will make the bidder lose money. Everyone wants to take advantage of others, but is unwilling to take advantage of others. Through such an arbitrage penalty mechanism, miners participating in the quotation can be encouraged to quote at the correct price in the market, so as to realize the delivery of truly effective price information to the quotation system.
| Number | Deliverable | Specification | Data Verification Time|
| -----: | ----------- | ------------- | --------------------- |
|ChainLink |Off-chain centralized submission, on-chain aggregation|YES|Post, after the data becomes effective|
|API3 |Off-chain centralized submission (removal of the middle party), on-chain aggregation |YES |Post, after the data becomes effective|
| Band|Off-chain aggregation, on-chain voting verification | YES|Post, after the data becomes effective|
| Tellor|Competing for computing power to obtain data reporting rights, aggregation on the chain |NO |Post, after the data becomes effective|
| HazelWord| Decentralized submission on the chain, real-time verification and aggregation on the chain|NO |Before, before the data becomes effective|


## Team :busts_in_silhouette:

### Team members

* Name of team leader:HuangShouYi
* Names of team members 

### Contact

* **Contact Name:** Huangshouyi
* **Contact Email:** hazel@hazelword.org
* **Website:**

### Legal Structure

* **Registered Address:** HAZELWORD FOUNDATION LTD.
* **Registered Legal Entity:** 20 MAXWELL ROAD, #08-08, MAXWELL HOUSE, SINGAPORE 069113

### Team's experience

One of them Coming from the financial advisory sector and specialist in Token Economics, has designed and developed various smart contracts on Ethereum.
One of them is also a Substrate runtime developer. He is proficient in distributed financial blockchain development.
One of them has more than 7 years product/program/project management experience in Blockchain and high-tech industry.
The rest are front-end developers, ui designers, and Android IOS developers
### Team Code Repos

*  https://github.com/Hazelword
*  https://github.com/qksl

Please also provide the GitHub accounts of all team members. If they contain no activity, references to projects hosted elsewhere or live are also fine.

* https://github.com/ydong3
* https://github.com/ywdlucking
...

### Team LinkedIn Profiles (if available)

* https://www.linkedin.com/<person_1>
* https://www.linkedin.com/<person_2>

## Development Status :open_book:

If you've already started implementing your project or it is part of a larger repository, please provide a link and a description of the code here. In any case, please provide some documentation on the research and other work you have conducted before applying. This could be:

* The smart contract complete phase 1.0 development
* Deployed contract on test network
* Complete DAPP Web UI development

## Development Roadmap :nut_and_bolt:

This section should break the development roadmap down into milestones and deliverables. Since these will be part of the agreement, it helps to describe _the functionality we should expect in as much detail as possible_, plus how we can verify and test that functionality. Whenever milestones are delivered, we refer to this document to ensure that everything has been delivered as expected.

Below we provide an **example roadmap**. In the descriptions, it should be clear how your project is related to Substrate, Kusama or Polkadot. We _recommend_ that the scope of the work can fit within a three-month period and that teams structure their roadmap as 1 milestone ≈ 1 month.

For each milestone,

* make sure to include a specification of your software. _Treat it as a contract_; the level of detail must be enough to later verify that the software meets the specification.
To assist you in defining it, we have created a document with examples for some grant categories [here](../docs/grant_guidelines_per_category.md).
* include the amount of funding requested _per milestone_.
* include documentation (tutorials, API specifications, architecture diagrams, whatever is appropriate) in each milestone. This ensures that the code can be widely used by the community.
* provide a test suite, comprising unit and integration tests, along with a guide on how to set up and run them.
* commit to providing Dockerfiles for the delivery of your project.
* indicate milestone duration as well as number of full-time employees working on each milestone.
* **Deliverables 0a-0d are mandatory for all milestones**, and deliverable 0e at least for the last one. If you do not intend to deliver one of these, please state a reason in its specification (e.g. Milestone X is research oriented and as such there is no code to test).


### Overview

* **Total Estimated Duration:**  5 month
* **Full-Time Equivalent (FTE):**  45 days with 6 Full-Time 
* **Total Costs:** $7800

####  M1：Basic module

* **Estimated duration:** 2 month
* **FTE:**  80
* **Costs:** 7,000 USD

| Number | Deliverable | Specification|
| -----: | ----------- | ------------- |
| 0a。| License | GPLv3 |
| 0b。| Documentation | We will provide a document to show how to use the SDK|
| 0c。| Testing Guide | Provide testing guide documents to provide developers with how to test our code|
| 0d. | Docker | Login interface, price view interface and mortgage interface |
| 0e. | Article | An article to introduce |
| 1. | Quotation generation module |1. All quote miners 2. Quote vault|
| 2. |Quote buy module |1. All verifiers 2. Verifier Quote vault|
| 3. |Price caller module|Only need to pay a certain fee or purchase a certain number of queries to get the current price of all trading pairs in the current block, and any contract or account can become a price caller.|
| 4. |Price caller | According to the mining rules, every T1 time period, all valid quotations (quotes that have not been taken) within this period of time are used to generate the final price of the block N of the transaction pair according to the weight.|




####  M2：Quote Vault Basic Module UI

* **Estimated duration:** 1 month
* **FTE:**  30
* **Costs:** 800 USD

| Number | Deliverable | Specification|
| -----: | ----------- | ------------- |
| 0a。| License | GPLv3 |
| 0b。| Documentation | We will implement the expansion of Polkadot account login function. Users can see the currency price and the interactive interface with Dapp (pledge to Quote Vault)|
| 0c。| Testing Guide | UI components will be covered by visual testing|
| 0d. | Docker | Login interface, price view interface and mortgage interface |
| 0e. | Article | An article to introduce |
| 1. | dapp | Quote Vault UI <br />Use react or vue we have a design model (https://github.com/Hazelword/hzl-sol/blob/main/doc/h1.png) (https://github.com/Hazelword/hzl-sol/blob/main/doc/h2.png) (https://github.com/Hazelword/hzl-sol/blob/main/doc/h3.png)|
| 2. | User settings | Users can easily pledge to Quote Vault|
| 3. | dapp | Data user ui|


## Future Plans

Please include here

* Shares token design for governance.
* Products include well-matched back-end and front-end, which support iOS, Android, and WEB.
* The product for consulting service Blockchain Forest will be connected to Hezel data service
* More partners in the blockchain ecology will be introduced and accessed to.



## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?** Web3 Foundation Website 

Here you can also add any additional information that you think is relevant to this application but isn't part of it already, such as:

* Work you have already done.
* Wheter there are any other teams who have already contributed (financially) to the project.
* Previous grants you may have applied for.