# Awesome Daml [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated resources for learning [Daml](https://docs.canton.network/) the smart contract language behind the Canton Network and for finding your way around the Canton developer ecosystem.

Daml is a strongly-typed, Haskell-derived language for multi-party workflows. Instead of a global shared state, every contract carries an explicit set of signatories and observers, so who is allowed to see and do what is part of the type-checked model rather than an afterthought. That model is what Canton executes and synchronizes across independently-operated participant nodes.


## Which docs site should I start with?

| Site | Covers | Use it for |
| --- | --- | --- |
| [docs.canton.network](https://docs.canton.network/) | Daml 3.x, Canton 3.5, current tooling | Everything current. Start here. |
| [docs.daml.com](https://docs.daml.com/) | Daml SDK 2.10.x | The older tutorials and prose, much of which has no 3.x equivalent yet |
| [docs.digitalasset.com](https://docs.digitalasset.com/) | Digital Asset's commercial apps | Registry, USDCx |

The language itself barely changed between 2.x and 3.x; templates, choices, and the standard library are roughly the same. Runtime and the tooling went through some changes (especially `dpm`, which replaces the old `daml` assistant as of SDK 3.5). Read 2.x prose for the Daml language, 3.x docs for anything else you need in your development environment.

## Contents

- [Start Here](#start-here)
  - [Coming from Ethereum?](#coming-from-ethereum)
- [Learning the Language](#learning-the-language)
- [Language Reference](#language-reference)
- [The Ledger Model](#the-ledger-model)
- [Tooling](#tooling)
- [SDKs and Bindings](#sdks-and-bindings)
- [Libraries](#libraries)
- [Example Applications](#example-applications)
- [Running Code Locally](#running-code-locally)
- [Upgrades and Production](#upgrades-and-production)
- [The Canton Ecosystem](#the-canton-ecosystem)
- [Data and Explorers](#data-and-explorers)
- [Papers](#whitepapers-etc)
- [Community articles](#community-articles)
- [Community Forums](#community-forums)

## Start Here

- [Choose Your Path](https://docs.canton.network/appdev/get-started/choose-your-path): routes you to the right module depending on whether you're writing contracts, an app, or running a node.
- [Canton Network QuickStart](https://docs.canton.network/appdev/quickstart/index): clone a working full-stack app and get it running before learning any theory.
- [Module 1: Understanding Canton](https://docs.canton.network/appdev/modules/m1-understanding-canton): the conceptual groundwork the rest of the docs assume you have.

### Coming from Ethereum?

- [Canton for Blockchain Developers](https://docs.canton.network/appdev/modules/m2-canton-for-ethereum-devs): written for people arriving from EVM/Solidity. Focus on the privacy and authorization sections.
- [Concept Translation Tables](https://docs.canton.network/appdev/modules/m2-concept-translation): mapping the terminology and the concepts between the two. 
- [Canton + Daml Auditor Bootcamp](https://github.com/gdroz3r/Canton-daml-auditor-bootcamp): aimed at auditors arriving from EVM or Move, organized around twenty recurring Daml vulnerability patterns with code for each. Also the fastest way for a non-auditor to learn what bad Daml looks like.

## Learning the Language

- [An Introduction to Daml](https://docs.daml.com/daml/intro/0_Intro.html): the long-standing tutorial course, building an asset-trading app chapter by chapter. Still the best sustained introduction to the language, though it targets 2.x tooling.
- [Module 3: Daml Smart Contracts](https://docs.canton.network/appdev/modules/m3-language-fundamentals): the 3.x treatment, split across [templates](https://docs.canton.network/appdev/modules/m3-contract-templates), [choices](https://docs.canton.network/appdev/modules/m3-choices), [authorization](https://docs.canton.network/appdev/modules/m3-authorization), [interfaces](https://docs.canton.network/appdev/modules/m3-interfaces), and [contract keys](https://docs.canton.network/appdev/modules/m3-contract-keys).
- [Composition and Design Patterns](https://docs.canton.network/appdev/modules/m3-design-patterns): propose/accept, delegation, role contracts. The idioms that separate working Daml from good Daml.
- [Daml Patterns (2.x)](https://docs.daml.com/daml/patterns.html): the original pattern catalogue, with fuller worked examples.
- [Testing Daml Contracts](https://docs.canton.network/appdev/modules/m3-testing): Daml Script as a test harness, including multi-party scenarios.
- [Working with Time](https://docs.canton.network/appdev/modules/m3-working-with-time): ledger time vs. record time, and why naive time handling breaks under contention.
- [Training and Certification](https://www.digitalasset.com/training-and-certification): Digital Asset's structured path, including the Daml Fundamentals exam.
- [The structure and flow of Daml smart contracts](https://blog.digitalasset.com/blog/-daml-smart-contract-structure-part-1): two-part article separating the static shape of a contract from its runtime behavior. ([part 2](https://blog.digitalasset.com/blog/-daml-smart-contract-structure-part-2))


## Language Reference

- [Daml Cheat Sheet](https://docs.daml.com/cheat-sheet/): one page, syntax and stdlib. ([source](https://github.com/digital-asset/daml-cheat-sheet))
- [Daml Language Reference](https://docs.canton.network/appdev/reference/daml-language-reference): the syntax and semantics, authoritative.
- [Daml Standard Library](https://docs.canton.network/appdev/reference/daml-standard-library/index): `DA.List`, `DA.Map`, `DA.Text`, `DA.Time` and the rest, module by module.
- [Prelude](https://docs.canton.network/appdev/reference/daml-standard-library/prelude): what's in scope without importing anything.
- [Daml.Script](https://docs.canton.network/appdev/reference/daml-script/daml-script): the API you write tests and ledger-initialization scripts against.
- [Daml-LF Reference](https://docs.canton.network/appdev/reference/daml-lf-reference): the intermediate representation Daml compiles to. Relevant once you care about package identity and upgrade compatibility.
- [Error Codes](https://docs.canton.network/appdev/reference/error-codes): searchable list, useful when the ledger rejects a submission and you want the actual reason.

## The Ledger Model

The formal model is worth reading properly. Most Daml bugs are authorization or privacy misunderstandings, not syntax errors.

- [The Ledger Model](https://docs.canton.network/overview/learn/ledger-model): transactions as trees, with authorization rules over the nodes.
- [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model): subtransaction privacy i.e. who learns which parts of a transaction, and why.
- [Privacy Model for App Developers](https://docs.canton.network/appdev/deep-dives/privacy-model): privacy model's design consequences for your app.
- [How Transactions Work](https://docs.canton.network/overview/learn/how-transactions-work): submissions, commits and confirmations.
- [Two-Layer Consensus](https://docs.canton.network/overview/learn/two-layer-consensus): how Canton separates ordering from validation.
- [Trust Model Overview](https://docs.canton.network/overview/learn/trust-model): what each participant has to trust, and what it doesn't.
- [Composing Multi-Party Workflows](https://docs.canton.network/appdev/deep-dives/composition-multi-party): why Daml workflows compose across organizations that don't trust each other.
- [Explicit Contract Disclosure](https://docs.canton.network/appdev/deep-dives/explicit-contract-disclosure): handing a contract to a non-stakeholder without making them an observer.

## Tooling

- [dpm](https://docs.canton.network/sdks-tools/cli-tools/dpm): the CLI: scaffolding, builds, tests, codegen, SDK version management. Replaces the `daml` assistant from SDK 3.5 on. ([repo](https://github.com/digital-asset/dpm))
- [Daml SDK](https://docs.canton.network/sdks-tools/sdks/daml-sdk): compiler, Daml Script runner, and sandbox, installed via `dpm`.
- [Daml Studio](https://marketplace.visualstudio.com/items?itemName=DigitalAssetHoldingsLLC.daml): the VS Code extension. Type checking, inline script results, go-to-definition.
- [IDE Setup](https://docs.canton.network/appdev/tooling/ide-setup): getting the editor tooling actually working, which is not always automatic.
- [Development Tools Overview](https://docs.canton.network/appdev/tooling/development-tools-overview): what each tool in the box is for.
- [PQS (Participant Query Store)](https://docs.canton.network/sdks-tools/development-tools/pqs): streams ledger state into PostgreSQL so you can query contracts with SQL. ([repo](https://github.com/digital-asset/participant-query-store), [SQL reference](https://docs.canton.network/appdev/reference/pqs-sql-reference))
- [Canton Console](https://docs.canton.network/global-synchronizer/canton-console/getting-started-tutorial): Scala REPL against a node, for topology and admin work.
- [Debugging Tools](https://docs.canton.network/appdev/tooling/debugging-tools) and [Debugging with lnav](https://docs.canton.network/appdev/quickstart/lnav): for when the logs are the only evidence you have.
- [Troubleshooting Cheat Sheet](https://docs.canton.network/appdev/troubleshooting): symptom-to-cause table. Pairs with the [common issues FAQ](https://docs.canton.network/appdev/faq).
- [Seaport](https://devnet.seaport.to/): hosted environment for building and deploying Daml without a local toolchain.
- [daml-lint](https://github.com/OpenZeppelin/daml-lint): OpenZeppelin's static analyser, doing for Daml roughly what Slither does for Solidity: unguarded division, unbounded decimals, missing `ensure` clauses. Explicitly experimental.
- [daml.nvim](https://github.com/Sengoku11/daml.nvim): Neovim support with LSP, inline script results, and Tree-sitter highlighting. The only serious alternative to the VS Code extension.
- [CantonTrace](https://github.com/justmert/cantontrace): local debugging UI: ACS inspector, transaction tree with per-party privacy analysis, and step-through of the Daml engine. Fills a genuine gap in the official toolchain.

## SDKs and Bindings

- [JSON Ledger API](https://docs.canton.network/sdks-tools/api-reference/json-api): plain HTTP against the ledger. ([tutorial](https://docs.canton.network/appdev/modules/m4-json-api-tutorial))
- [gRPC Ledger API](https://docs.canton.network/sdks-tools/api-reference/ledger-api-services): the full API, including event streaming.
- [Wallet SDK](https://docs.canton.network/sdks-tools/sdks/wallet-sdk): TypeScript, for party management, transfers, and transaction signing.
- [Wallet Gateway](https://github.com/canton-network/wallet): dApp-side SDK and OpenRPC spec for talking to Canton wallets from a frontend.
- [dazl](https://github.com/digital-asset/dazl-client): Python Ledger API client. ([PyPI](https://pypi.org/project/dazl/))
- [go-daml](https://github.com/noders-team/go-daml): Go client with a type-safe code generator that reads `.dar` files.
- [c7_ledger](https://github.com/C7-Digital/c7_ledger): actively maintained drop-in replacements for `@daml/ledger` and `@daml/react`.
- [Contracts and Transactions in Java](https://docs.canton.network/appdev/deep-dives/contracts-and-transactions-in-java): working with generated Java codegen output.

## Libraries

- [Daml Finance](https://github.com/digital-asset/daml-finance): instruments, holdings, settlement, and lifecycling. Don't model a financial asset from scratch before reading this. ([docs](https://docs.daml.com/daml-finance/index.html))
- [daml-ctl](https://github.com/digital-asset/daml-ctl): small control-flow helpers ported from Haskell.
- [Canton Token Template](https://github.com/OpenZeppelin/canton-token-template): Starting point for a CIP-56 compliant token registry, by OpenZeppelin.
- [daml-tokenization-toolkit](https://github.com/SynfiniDLT/daml-tokenization-toolkit): tokenization and settlement built on Daml Finance, by ASX Operations.
- [account-hierarchy](https://github.com/SynfiniDLT/account-hierarchy): custody and account-hierarchy modelling for solving the nested-ownership problem.
- [daml-nft](https://github.com/SynfiniDLT/daml-nft): small NFT library.
- [Catalyx Package Manager](https://apps.catalyx.solutions/marketplace): community marketplace for reusable Daml packages.

## Example Applications

- [cn-quickstart](https://github.com/digital-asset/cn-quickstart): the reference full-stack app: Daml models, backend, frontend, and a LocalNet to run it against.
- [daml-finance-app](https://github.com/digital-asset/daml-finance-app): larger demo built on Daml Finance.
- [ex-java-bindings](https://github.com/digital-asset/ex-java-bindings): the same example client written three ways, for comparing the abstraction levels.
- [ex-java-bindings-with-opentelemetry](https://github.com/digital-asset/ex-java-bindings-with-opentelemetry): adds tracing to the above client.
- [splice](https://github.com/canton-network/splice): the Global Synchronizer's own applications: Canton Coin, Scan, validator, and SV apps. For reviewing what the production-quality Daml looks like.
- [example-insurance-claim](https://github.com/SynfiniDLT/example-insurance-claim): an insurance claim as a multi-party workflow example.
- [canton-erc20](https://github.com/ChainSafe/canton-erc20): ERC-20 bridge between Ethereum and CIP-56 tokens, by ChainSafe. ([Go middleware](https://github.com/ChainSafe/canton-middleware))
- [hemera](https://github.com/liakakos/hemera): Daml-to-Ethereum integration over the Java bindings. Unmaintained since 2023, but the same pattern of offchain integrations still works.
- [daml-on-sawtooth](https://github.com/blockchaintp/daml-on-sawtooth): Daml's runtime on Hyperledger Sawtooth. Unmaintained, but works as an example of Daml being a ledger-agnostic language.

## Running Code Locally

- [LocalNet Development](https://docs.canton.network/appdev/modules/m5-localnet-development): a full network (validators, synchronizer, wallets, PQS, Keycloak) in Docker Compose.
- [Development Environment Setup](https://docs.canton.network/appdev/modules/m3-dev-environment): the minimal setup, before you need Docker.
- [Deployment Progression](https://docs.canton.network/appdev/modules/m5-deployment-progression): sandbox to LocalNet to DevNet to production.
- [Deploy Quickstart to DevNet](https://docs.canton.network/appdev/quickstart/deploy-to-devnet): first deployment onto a shared network.
- [Testing Strategies](https://docs.canton.network/appdev/modules/m5-testing-strategies): where Daml Script stops being enough.
- [CI/CD Integration](https://docs.canton.network/appdev/modules/m5-ci-cd-integration): building and testing DARs in a pipeline.

## Upgrades and Production

Daml packages are immutable and content-addressed, which complicates the upgrades. 

- [Smart Contract Upgrades Overview](https://docs.canton.network/appdev/modules/m6-overview): start here, then [writing your first upgrade](https://docs.canton.network/appdev/modules/m6-writing-first-upgrade).
- [Upgrade Compatibility](https://docs.canton.network/appdev/modules/m6-upgrade-compatibility) and [Limitations](https://docs.canton.network/appdev/modules/m6-limitations): what you're allowed to change, and what you'll regret.
- [Smart Contract Upgrade (SCU) deep dive](https://docs.canton.network/appdev/deep-dives/smart-contract-upgrade): about the upgrade mechanism itself.
- [Package Selection](https://docs.canton.network/appdev/modules/m6-package-selection) and [Package Naming](https://docs.canton.network/appdev/modules/m6-package-naming): naming is extra important to get right early.
- [Security Best Practices](https://docs.canton.network/appdev/modules/m7-security): Daml-specific security practices.
- [Performance Best Practices](https://docs.canton.network/appdev/modules/m7-performance) and [Performance Optimization](https://docs.canton.network/appdev/deep-dives/performance-optimization).
- [Error Handling](https://docs.canton.network/appdev/modules/m7-error-handling): retryable vs real failures.
- [Application Architecture Design](https://docs.canton.network/appdev/deep-dives/app-architecture-design): how to design your application stack (frontend, Daml models, backend).
- [Observability](https://docs.canton.network/appdev/modules/m4-observability) and [Open Tracing](https://docs.canton.network/appdev/deep-dives/open-tracing).

## The Canton Ecosystem

- [Canton Network](https://www.canton.network/): the network itself, and [its problem statement](https://docs.canton.network/overview/understand/the-problem).
- [Canton Network in 5 Minutes](https://docs.canton.network/overview/understand/five-minute-overview): tldr.
- [Glossary](https://docs.canton.network/overview/understand/glossary)
- [Canton Developer Hub](https://dev-hub.canton.foundation/): the Foundation's catalogue of tools and SDKs, open to PRs. ([repo](https://github.com/canton-network-devs/Canton-Developer-Hub))
- [Canton Improvement Proposals](https://github.com/canton-foundation/cips): where protocol and standard proposals are developed. For instance, [CIP-56](https://github.com/canton-foundation/cips/blob/main/cip-0056/cip-0056.md) defines the token standard.
- [Token Standard](https://docs.canton.network/appdev/deep-dives/token-standard): about the CIP-56.
- [Canton Foundation](https://canton.foundation/): governance, plus their [grants program](https://canton.foundation/grants-program/).
- [Canton Development Fund](https://github.com/canton-foundation/canton-dev-fund): funding process in the open.
- [Canton Ecosystem](https://www.cantonecosystem.com/): directory of apps and wallets on the network.
- [Canton](https://github.com/digital-asset/canton): the protocol implementation, in Scala.
- [Daml](https://github.com/digital-asset/daml): the compiler, standard library, and language runtime. Apache-2.0.
- [Canton Hub](https://unityhub.dev/canton): community resource hub covering education, dev, and validator material.
- [Onboarding & Dev Fund Guide](https://canton-101.vercel.app): community walkthrough of the devnet-to-testnet-to-mainnet progression, and how Dev Fund proposals actually get approved.

## Data and Explorers

- [Scan API](https://docs.canton.network/sdks-tools/api-reference/splice-scan-api): read-only network data: mining rounds, Canton Coin (CC) supply, DSO state.
- [Validator API](https://docs.canton.network/sdks-tools/api-reference/splice-validator-api): per-node REST API for wallet ops, traffic, and party onboarding.
- [Noves Canton Data API](https://docs.noves.fi/reference/welcome-canton-apis): hosted API over publicly observable network data.
- [CCView](https://ccview.io): explorer with a public indexing API. ([API docs](https://docs.ccview.io/reference/ans))
- [Lighthouse](https://lighthouse.cantonloop.com): alternative community explorer.
- [CC Space](https://cc.itrocket.space/): explorer with analytics, alerting, and validator monitoring.

## Agentic Development

- [Canton Foundation MCP](https://github.com/canton-network-devs/Build-on-Canton-MCP): MCP server serving current Canton docs to coding assistants.
- [Claude Code Daml Skill](https://github.com/canton-network-devs/CF-Daml-Skill): packaged Daml knowledge for Claude Code.
- [CCPedia](https://ccpedia.xyz): AI-queryable index over CIPs, forum threads, docs, and Dev Fund proposals.

## Whitepapers etc

- [Daml: A Smart Contract Language for Securely Automating Real-World Multi-Party Business Workflows](https://arxiv.org/abs/2303.03749): Bernauer et al., 2023. The language paper: the authorization model, the privacy model, and the reasoning behind the template/choice design. The single best technical account of *why* Daml looks the way it does.
- [Canton: A Daml based ledger interoperability protocol](https://www.canton.io/publications/canton-whitepaper.pdf): the original 2020 technical paper, and considerably more precise than the marketing pages that superseded it.
- [Canton Network whitepapers](https://www.canton.network/whitepaper): the full set, including the Canton Network paper and the Canton Coin papers.
- [Polyglot Canton](https://www.canton.network/hubfs/Canton%20Network%20Files/whitepapers/Polyglot_Canton_Whitepaper_11_02_25.pdf): the case for opening Canton to languages beyond Daml, running Solidity and others over WebAssembly.
- [Daml Ledger Model (2.x)](https://docs.daml.com/concepts/ledger-model/index.html): the formal treatment of transactions, authorization, and privacy. Dense, and worth it.

### Academic Research

- [Access Control Verification in Smart Contracts Using Colored Petri Nets](https://doi.org/10.3390/computers13110274): Al-Azzoni & Iqbal, *Computers*, 2024. Parses Daml templates into Petri nets and model-checks the access control. Open access.
- [Smart contract life-cycle management](https://doi.org/10.3389/fbloc.2023.1276233): Mustafa, McGibney & Rea, *Frontiers in Blockchain*, 2024. A verification framework for Daml contracts, including a type-safety checker for access-control and IDOR-style flaws. Open access.
- [Visual Smart Contracts for DAML](https://doi.org/10.1007/978-3-031-09843-7_8): Heckel et al., ICGT 2022. Graph-transformation semantics for Daml, aimed at making contract behaviour visually inspectable.
- [Dynamic Role-Based Access Control Scenarios for Smart Contracts](https://www.jot.fm/contents/issue_2025_02/a4.html): Al-Azzoni, Heckel & Erum, *Journal of Object Technology*, 2025. Generating Daml access-control tests via graph rewriting. Open access.
- [Modelling Multi-Party Role-Based Access Control Policies for iContractML Smart Contracts](https://doi.org/10.1109/asew60602.2023.00018): Al-Azzoni & Heckel, ASEW 2023. Models RBAC once, then maps it to both Solidity and Daml.
- [Decentralized Oracle Networks (DONs) Provision for DAML Smart Contracts](https://doi.org/10.1007/978-3-031-45155-3_36): Mustafa et al., 2023. Integrating Oracles into Daml.

## Community articles

- [My thoughts after 6 months working with DAML](https://idiomaticsoft.com/post/2023-04-11-exploring-daml/): a practitioner's retrospective.
- [DAML: A Haskell-Based Language for Blockchain](https://serokell.io/blog/daml-interview): on what Daml inherits from Haskell and what it deliberately drops.
- [Learning Daml: Advantages and Challenges](https://www.halborn.com/blog/post/learning-daml-advantages-and-challenges): thoughts on security-audit perspective.
- [Deep Dive on Permissioned Blockchains: The Canton Network](https://collective.flashbots.net/t/deep-dive-on-permissioned-blockchains-the-canton-network/5517): Flashbots Collective research thread.
- [Exploring Canton Network: privacy-first distributed ledgers](https://medium.com/iobuilders/exploring-canton-network-a-deep-dive-into-privacy-first-distributed-ledgers-58046e0901a7): walkthrough of the privacy architecture.
- [DAML Development Guide](https://pixelplex.io/blog/daml-development-guide/)
- [Daml Masterclass](https://medium.com/daml-masterclass/full-stack-developer-happiness-a1a122ebd8de): long-running series on full-stack Daml, including [driving the ledger from Rust](https://medium.com/daml-masterclass/rust-daml-a-biz-friendly-smart-contract-platform-deserves-a-biz-friendly-client-language-ddb74922a263).

## Community Forums

- [Canton Network Forum](https://forum.canton.network/): formerly the Daml forum, and still a place where the language questions get answered by people who wrote the compiler.
- [Official Discord](https://discord.com/invite/canton).
- [Official Telegram](https://t.me/CantonNetwork1)
- [Stack Overflow `daml` tag](https://stackoverflow.com/questions/tagged/daml): not active, but the old language-specific answers are often still correct.
- [GitHub `daml` topic](https://github.com/topics/daml): for finding projects not catalogued anywhere else.
- [Digital Asset on YouTube](https://www.youtube.com/@digitalassetcom): talks and recorded sessions.
- [Canton Network blog](https://www.canton.network/blog)

## Contributing

Pull requests welcome. One link per entry, a description that says what the thing is and when you'd reach for it, and no marketing copy. Dead links get removed without ceremony.

## License

[CC0-1.0](LICENSE).
