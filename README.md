# cryptoFinance

A rough launch plan for various crypto/digital financial products.

## Objectives
* Build a historical track record of crypto financial trading with viable VaR
  and AUM.
* Implement simple and functional financial products, optimized for ease of
  use.
* Allow general, scalable access to these tools for savvy or novice
  investors.
* Explore and build natively on popular cryptocurrency platforms to uncover
  novel investment applications.

## Roadmap

### Phase 1: Index Fund 
* **Goal**: Use Iconomi's robust [DAA architecture](https://www.iconomi.net/arrays) to quickly launch a simple quantitative fund, demonstrating Markowitz Portfolio Theory.
* **Strategy**: *Modern portfolio theory (MPT)*, or *mean-variance analysis*, is a mathematical framework for assembling a portfolio of assets such that the expected return is maximized for a given level of risk, defined as variance. Its key insight is that an asset's risk and return should not be assessed by itself, but by how it contributes to a portfolio's overall risk and return.  
* **Origin**: Economist Harry Markowitz introduced MPT in a 1952 essay, for which he was later awarded a Nobel Prize in Economics.
* **Reasoning**: MPT has occasionally been bashed for being more theoretical than practical, which is reasonable since [pure MPT portfolios are highly sensitive to intercorrelation, the latest historical returns, and linear market assumptions](https://www.quora.com/Why-is-modern-portfolio-theory-wrong/answer/Gaurav-Chakravorty?srid=hGdJD). Generally, investors use MPT as a tool to assist in portfolio planning, but we intend to publish this portfolio to act as an active, investable market benchmark from which other investors could take insights from or build upon. Simply put; any technical trader should be usig a [continuously rebalanced Markowitz portfolio](http://www.math.ust.hk/~makchen/MAFS5140/Chap4.pdf) as a benchmark for optimal market return given risk at a given point in time.
* **Process**: 
    * Step 1: Data Acquisition
        * Discover relevant historical datasets to generate initial portfolio model.
        * Organize data into refreshable sources and pipelines, allowing the algorithm to leverage new data on demand.
        * Build these pipelines into an Analytics warehouse like [Google Cloud Platform](https://cloud.google.com/bigquery/), for ease of use and scalability.
    * Step 2: Data Preparation
        * Clean and interpolate data to ensure highest data fidelity and algorithmic effeciency. 
        * Batch compute covariant matrices, historical mean returns, saving/reusing values for algorithmic effeciency. 
        * (*Optional*) Potentially incorporate PCA (Principal Component Analysis) to examine independent underlying performance, accounting for intercorrelation of underlying assets.
        * (*Optional*) Also incorporate other [mathematical constraints](http://www.math.ust.hk/~makchen/MAFS5140/Chap4.pdf) to limit maximum weights, disallow short selling, etc.
        * (*Optional*) Use same data and algorithm to construct other portfolios for different edge cases on the effeicent frontier such as: **Lowest Risk Portfolio**, **Highest Risk Portfolio**,  etc.
        * Build these metric analyses on [Jupyter](https://cloud.google.com/datalab/) to scale computation effeciently, and save results.
        * Use saved results to a sub dataset for quick portfolio generation by calling a [Google Cloud Function](https://cloud.google.com/functions/).
    * Step 3: Data Application
        * Build a rudimentary back testing / live testing system to ensure ongoing success of this methodology. 
        * Given available mean and variance of underlying assets (potentially incorporating a maximum cap to reduce over-exposure), generate a vector portfolio weights.
        * Initial portfolio will follow the standard [**Maximum Sharpe Portfolio**](https://blog.thinknewfound.com/2013/02/the-intuition-behind-sharpe-maximization-in-unconstrained-mean-variance-optimization/), which seeks to find the tangency portfolio that yields the highest return for the least risk.
        * Integrate recommended portfolio weights into an Iconomi DAA.
        * (*Optional*) Use same data and algorithm to construct other portfolios for different edge cases on the effeicent frontier such as: **Lowest Risk Portfolio**, **Highest Risk Portfolio**,  etc.
    * Step 4: Data Updating
        * Re-reunning Steps 1 - 3 on a biweekly or monthly cadence to rebalance DAA portfolio to track market, since [minor variations significantly influence MPT viability](https://www.quora.com/Why-is-modern-portfolio-theory-wrong/answer/Gaurav-Chakravorty?srid=hGdJD).
        * (*Optional*) Ideally reduce cadence even further via automation, to allow optimal market mean and variance tracking. Theoretically, a continuously rebalanced MPT portfolio would be the best case, but such a setup may be impractical in practice (algorithmic/data/transactional costs would be too high.)
        * Incorporating new digital assets as they become available on the Iconomi platform, in order to rebalance with correct asset availability.

### Phase 2: Index Fund as a Token
* **Goal**: Tokenize the Iconomi DAA portfolio into a tradeable token, allowing for access in secondary markets, and inclusion as underlying in other portfolios.
* **Strategy**: Leverage all [existing work](https://github.com/redqueenxyz/sigmaCoin) and discoveries from Phase 1 to further improve fund liquidity through native Ethereum integration.
* **Origin**: Crypto securities are a new way to both represent and facilitate financial trades, and other platform native variants like [C20](https://crypto20.com/en/) and [BLX](https://www.iconomi.net/dashboard/#/daa/BLX) have shown early success in this secondary market.
* **Reasoning**: Native Ethereum implementations will quickly become necessary to keep pace with the market, and may even yield novel features that are undiscovered or unavailable in platforms like Iconomi, making the relatively simple wrapping of our Phase 1 findings an efficient way to explore this platform's technology purposefully for financial product applications.
* **Process**: 
    * Step 1: Platform (Ethereum) Exploration
    * Step 2: Data Accessibility ("Off-chain" components)
    * Step 3: Fund Tokenization ("On-chain" components)
    * Step 4: (*Optional*) Secondary Token ICO
    * Step 5: Token Deployment

### Phase 3: (*Optional*) Robo Investing as a Service
* **Goal**: Given newly gained knowledge of crypto financial products, work towards the construction of a simple investing bot assistant, complete with simple performance dashboards, dollar cost averaging, automated rebalancing, and other features necessary to comfort new investors in this space.
* **Strategy**: Having created new tools and techniques to appeal to technical and institutional traders, build a product that makes crypto investing more accesible to the average investor, incorporating salient techniques and best practices.
* **Origin**: Currently a variety of hypothetical crypto currency investors are overwhelmed by the difficulty to enter the market via exchanges, navigating the variety of tokens and digital assets available, deciding on an optimal strategy, and then executing that strategy consistently. We hope to simplify this entire process using a simple wrapper, and make crypto-Finance more accesible.
* **Reasoning**: Robo Advisors like [Wealthsimple](http://wealthsimple.com/), [Betterment](http://betterment.com/), and [Wealthfront](http://wealthfront.com/) are gaining notoriety for breaking down the jargon of investing, captivating the interest (and funding) of the less-savy consumer as a far more effecient means of investing. A similar product for cryptocurrencies (or the incorporation of digital assets onto those platforms) is an eventuality, and technology exploring such application may become valuable quickly.
* **Process**: 
    * Step 1: Web App Development
    * Step 2: Token / Asset Buying Integration
    * Step 3: Account Funding Integration
    * Step 4: App Launch 
    * Step 5: User Acqusition

### Phase 4: Evolutionary Investing as a Token
* **Goal**: Move away from the MPT and pursue a far more recent and robust approach in financial theory, namely [genetic algorithms](https://www.investopedia.com/articles/financial-theory/11/using-genetic-algorithms-forecast-financial-markets.asp), reinforced parallelized machine learning, and [evolutionary strategies](https://blog.openai.com/evolution-strategies/).
* **Strategy**: Implement cutting edge theory into a native Ethereum implementation, both to test the theoretical limits of the platform and apply the latest findings of quantiative financial theory.
* **Origin**: At the initial proposal of [sigmaCoin](https://github.com/redqueenxyz/sigmaCoin) at the Blockgeek 2017 Hackathon, Vitalik Buterin commented on the practical validity of the MPT model, noting that it's theortical assumptions could make it easy to game or trick in the highly volatile (and unregulated) world of crypto Finance. His response was to pusure an implementation that was more adverserial, the investigation of which has yielded this new and fascinating financial theory that warrants testing in market.
* **Reasoning**: By employing a simple yet intelligent updating rule across a variety of
  randomly intialized workers, building a mechanism for the creation,
  measurement, culling, and evolution of iterative generations of portfolios,
  we will implement [a multiagent search for the optimal cryptocurrency
  portfolio] that leverages the computational power of Ethereum itself to
  optimize its performance intelligently, without little human input beyond
  initialization.
    * Step 1: Whitepaper
    * Step 2: (*Optional*) Pre-sale ICO
    * Step 3: Platform Implementation ("On-chain" components)
    * Step 4: Platform Deployment

## Availability

A list of underlying assets and potential data sources, currently leveraging the [Iconomi](https://www.iconomi.net/) platform.

| Name             	| Coin 	| Description                                                                                                                                                                                                                                            	| Platform Availability 	| Data Availability 	| Portfolio Inclusion 	|
|------------------	|------	|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|-----------------------	|-------------------	|---------------------	|
| 0x | ZRX | Is utilized to: 1) solve the coordination problem and drive network effects around liquidity, creating a feedback loop where early adopters of the protocol benefit from wider adoption, and 2) be used for decentralized governance of the 0x protocol's update mechanism. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| AdEx | ADX | Is a token of influence that solves the current problems of online advertising. ADX tokens will be used for trading advertising property rather than just for governance, and will thus be easier for advertisers and publishers to understand and adopt. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| adToken | ADT | Is a utility-based token used for participating in the adChain protocol. adToken holders will pave the way for a new industry standard in digital advertising. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Aragon | ANT | Will be used to govern every single aspect of its functioning on the Aragon Network, whose goal is to act as a digital jurisdiction that is easy and user-friendly for organisations, entrepreneurs, and investors to operate. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Augur | REP | Is a distributed prediction market to exchange value when forecasting event outcomes based on the ‘wisdom of the crowd’ principle. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Bancor | BNT | Forms a monetary structure where increased demand for any of the network’s smart tokens drives up the value of BNT, benefiting all other smart tokens holding it in reserve. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Basic Attention Token | BAT | Radically improves the efficiency of digital advertising by creating a new token that can be exchanged between publishers, advertisers, and users. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Bitcoin | BTC | Is the original value token that still represents more than a half of tokenised digital assets’ market capitalisation. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Bitcoin Cash | BCH | Is the result of a Bitcoin hard fork and is the continuation of the Bitcoin project as peer-to-peer digital cash. In an effort to scale on-chain, BCH raises the block size limit to 8MB and will not implement segwit. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Blocktix | TIX | Is an Ethereum-based, counterfeit-resistant platform for distributing, advertising, and transferring ownership of event tickets. Blocktix fees compensate token holders participating in the event/advertising verification process. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Chronobank | LH | Are linked to the average hourly wage in the host country and are backed by a real labour force from big recruitment and labour-hire companies. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Civic | CVC | Is the official coin of the Civic ID theft protection service, an identity management service that allows users to protect and authorise the use of their identity in real-time. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Cofound.it | CFI | Is a distributed global platform that connects exceptional startups, experts, and investors worldwide. It will first be built by the blockchain community for the blockchain community—and then for the whole world. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Creditbit | CRB | Is a digital Ethereum Token that hosts on the Ethereum Blockchain, a public distributed digital ledger. One of the most prominent functionalities is Proof of Trust, a locking mechanism, that enables token owners to be involved in issued token distribution and voting. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Decentraland | MANA | A virtual reality platform powered by the Ethereum blockchain. Users can create, experience, and monetize content and applications. The MANA token allows users to claim parcels of virtual land and make in-world purchases of digital goods and services. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Digital Cash | DASH | Is a digital value token based on Bitcoin that provides for faster transactions and enhanced financial privacy. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| DigixDAO | DGD | Is the first organisation built on Ethereum that tokenises physical assets onto the Ethereum blockchain. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| district0x | DNT | Is a multi-utility ERC20 token providing holders with both network-wide governance utility and a means of gaining access to district-specific voting rights on the district0x platform, a network of decentralized markets and communities. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Edgeless | EDG | Is used to access the Edgeless Lounge and win a share of the prize pool. EDG token holders can trust that every month 40% of Edgeless’s profit will be transferred to the Edgeless Lounge prize pool. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| EOS | EOS | Token is a temporary token issued to complete the EOS ICO and is not required for use of the EOS platform. EOS is a smart-contract-enabled hosting platform built for open-source projects and is designed to enable vertical and horizontal scaling of decentralized applications. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Ether | ETH | Is the value token of a distributed platform that allows developers to create distributed applications and smart contracts. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Ethereum Classic | ETC | Is is a decentralized platform that runs smart contracts: applications that run exactly as programmed without any possibility of downtime, censorship, fraud, or third-party interference. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Everex | EVX | Offers blockchain-based microlending, remittances, and merchant payments to underserved individuals and small and medium-sized enterprises in Asia and internationally. EVX tokens are required for utilizing the Everex platform. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| FirstBlood | 1ST | Token holders are entitled to play, watch and judge matches on FirstBlood, host tournaments and claim rewards in 1ST tokens based on gaming activity. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| FunFair | FUN | Is the fundamental method of interaction with FunFair smart contracts, ensuring every participant is rewarded for their contribution. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| GameCredits | GAME | Is a gaming value token based on Bitcoin that aims to replace existing in-game purchasing options and mechanisms. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Gnosis | GNO | based on Ethereum—the next generation blockchain network. Speculate on anything with an easy-to-use prediction market. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Golem | GNT | Is a token of the Ethereum-based decentralised supercomputer network Golem. It is part of the open-source Golem project, where anyone can make money 'renting' out their computing power or developing & selling software. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Humaniq | HMQ | Is the core of the banking ecosystem that Humaniq has developed, creating a completely new banking experience by dissolving all the barriers of archaic banks. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Iconomi | ICN | Token benefits from the performance of the professionally managed CCP DAA, from fees collected on the ICONOMI platform, and from a system of regular buybacks. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| iExec RLC | RLC | Is a new decentralised cloud-computing platform that is blockchain based. It aims to tackle the current limitations of centralised cloud computing. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Legends Room | LGD | Is the tokenised currency used for The Legends Room, the first gentlemen’s cabaret in Las Vegas that accepts Bitcoin for all club services. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Lisk | LSK | The token that powers the Lisk network. Lisk is a public blockchain platform that provides distributed blockchain apps with their own separate blockchain, solving challenges around scalability. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Lunyr | LUN | Is used to advertise on the Lunyr network, the future of knowledge and sharing. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| MaidSafecoin | MAID | Is the token used on the Maidsafe Network, which is a distributed data storage network. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Matchpool | GUP | Is the token used on Matchpool, the first platform for mainstream matchmaking powered by a cryptographic token economy. GUP tokens can be purchased or sold with real money. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Melon | MLN | Is a core component of the Melon project. It is designed to enjoy a “usage right” to the Melon protocol. To use the Melon protocol one has to use MLN tokens. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Metal | MTL | Is fairly distributed through a process known as Proof of Processed Payments. When you send money or make purchases you earn a little reward in MTL for every dollar you spend. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Monaco | MCO | Is Visa-based debit card, which supports Ether and Bitcoin. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Mysterium | MYST | Will work as access tokens to the Mysterium Network, an open-source network allowing anyone to rent their unused network traffic while providing a secure connection for those in need. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Nexium | NXC | Follows basic standards of the community and can be used with Mist Ethereum Wallet or MyEtherWallet. NXC are tokens created for Beyond The Void within the Ethereum Blockchain. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Numeraire | NMR | Is an ERC20 Ethereum token used on the Numerai platform, a new kind of hedge fund built by a network of data scientists. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| OmiseGo | OMG | Is used as a bond on the OmiseGO platform, creating a custom chain with deep enforcement. OmiseGO is able to construct a system where consensus rules optimise for high-performant activity. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Patientory | PTOY | Is the fuel for driving the blockchain infrastructure. The primary use of PTOY tokens is to regulate network storage allocation, health care quality measures and revenue payment cycles. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Qtum | QTUM | Is the official token of the QTUM decentralised application creation platform. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Raiden | RDN | Is an off-chain scaling solution that enables near-instant, low-fee, scalable payments and works with any ERC20-compatible token. The RDN token is used to pay fees for using the Raiden Network. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Request | REQ | Token is required for the operation of Request contracts, especially the extension layers for advanced features. Request is a layer built on Ethereum that disintermediates payment requests. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Ripio Credit Network | RNC | Enables connections between lenders and borrowers located anywhere in the world, regardless of currency. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| SALT | SALT | A membership-based lending and borrowing network that allows users to leverage their blockchain assets to secure cash loans. SALT tokens represent levels of access to the platform and can also be redeemed for products, services, and other rewards.  | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| SingularDTV | SNGLS | Is a blockchain entertainment studio laying the foundation for a decentralised entertainment industry. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Status | SNT | Is used to create a Users-as-Stakeholders network, allowing the behaviour of the network and its software, to become aligned with the interests of its users. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Steem | STEEM | Is building a distributed content and media distribution platform, promising to disrupt publishing and distribution businesses. Community building and social interaction are rewarded. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Storj | SJCX | Is used to reduce transaction fees for the Storj community while also increasing functionality and usability. There are many benefits to using SJCX as a utility token in the Storj network. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Swarm City | SWT | Is the unit of exchange in Swarm City. Swarm City is built upon the Ethereum Platform and interacts with the Ethereum Blockchain. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Synereo | AMP | Is the native token of Synereo, which serves as a way to amplify the flow of information in the network and allows content creators to easily monetise original works without relying on ads. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| TenX | PAY | Is a crypto asset-based wallet/bank with a debit card. With a Cryptographically-secure Off-chain Multi-asset Instant Transaction network, the service will support unlimited crypto assets; for now, they support ETH, ERC20, DASH, and BTC. Users will choose which crypto asset to deduct for debit card payment and ATM withdrawals. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Tierion | TNT | Provides a platform for using the Bitcoin and Ethereum blockchains to verify any data, file, or business process. The TNT token provides an economic incentive to secure the network and serves as a method of settlement between parties to access network resources. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| The Quantum Resistant Ledger | QRL | Is the official token of The Quantum Resistant Ledger, utilising hash-based digital signatures which are resistant to classical and quantum computing attacks. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| TokenCard | TKN | Is a smart-contract-powered debit card, which can be used to pay on PoS terminals and for cash withdrawal on ATMs. Debit is in the form of ERC20 tokens deposited on TokenCard accounts. Money spent is proportionally reduced from users' tokens. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Viberate | VIB | Is a live music ecosystem and a blockchain-based marketplace that matches musicians with event organizers. VIB tokens are used to pay for platform services, including booking fees, advertising space, and event tickets. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Waves | WAVES | Is a Blockchain token platform that allows the creation, transfer, and exchange of custom and fiat tokens and assets through the Blockchain without volatility. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| WeTrust | TRST | Is a collaborative savings, lending and insurance platform that is autonomous, agnostic, frictionless, and decentralized. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
| Wings | WINGS | Represents a share within the Wings Decentralized Autonomous Organization (DAO) and allows users to vote on the development of the platform, and to receive dividends from the fees generated within the platform. Wings is a platform where users can create and invest in DAOs. | [✓](https://www.iconomi.net/digital-assets) | TBD |  TBD |
