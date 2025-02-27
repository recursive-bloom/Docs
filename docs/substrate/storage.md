---
title: Storage
---

The following sections contain Storage methods are part of the default Substrate runtime. On the api, these are exposed via `api.query.<module>.<method>`. 

(NOTE: These were generated from a static/snapshot view of a recent Substrate master node. Some items may not be available in older nodes, or in any customized implementations.)

- **[assets](#assets)**

- **[authorship](#authorship)**

- **[babe](#babe)**

- **[balances](#balances)**

- **[bounties](#bounties)**

- **[contracts](#contracts)**

- **[council](#council)**

- **[democracy](#democracy)**

- **[electionProviderMultiPhase](#electionprovidermultiphase)**

- **[elections](#elections)**

- **[gilt](#gilt)**

- **[grandpa](#grandpa)**

- **[identity](#identity)**

- **[imOnline](#imonline)**

- **[indices](#indices)**

- **[lottery](#lottery)**

- **[mmr](#mmr)**

- **[multisig](#multisig)**

- **[offences](#offences)**

- **[proxy](#proxy)**

- **[randomnessCollectiveFlip](#randomnesscollectiveflip)**

- **[recovery](#recovery)**

- **[scheduler](#scheduler)**

- **[session](#session)**

- **[society](#society)**

- **[staking](#staking)**

- **[substrate](#substrate)**

- **[sudo](#sudo)**

- **[system](#system)**

- **[technicalCommittee](#technicalcommittee)**

- **[technicalMembership](#technicalmembership)**

- **[timestamp](#timestamp)**

- **[tips](#tips)**

- **[transactionPayment](#transactionpayment)**

- **[transactionStorage](#transactionstorage)**

- **[treasury](#treasury)**

- **[uniques](#uniques)**

- **[vesting](#vesting)**


___


## assets
 
### account(`AssetId, AccountId`): `AssetBalance`
- **interface**: `api.query.assets.account`
- **summary**:   The number of units of assets held by any given account. 
 
### approvals(`AssetId, AccountId, AccountId`): `Option<AssetApproval>`
- **interface**: `api.query.assets.approvals`
- **summary**:   Approved balance transfers. First balance is the amount approved for transfer. Second is the amount of `T::Currency` reserved for storing this. First key is the asset ID, second key is the owner and third key is the delegate. 
 
### asset(`AssetId`): `Option<AssetDetails>`
- **interface**: `api.query.assets.asset`
- **summary**:   Details of an asset. 
 
### metadata(`AssetId`): `AssetMetadata`
- **interface**: `api.query.assets.metadata`
- **summary**:   Metadata of an asset. 

___


## authorship
 
### author(): `Option<AccountId>`
- **interface**: `api.query.authorship.author`
- **summary**:   Author of current block. 
 
### didSetUncles(): `bool`
- **interface**: `api.query.authorship.didSetUncles`
- **summary**:   Whether uncles were already set in this block. 
 
### uncles(): `Vec<UncleEntryItem>`
- **interface**: `api.query.authorship.uncles`
- **summary**:   Uncles 

___


## babe
 
### authorities(): `Vec<(AuthorityId,BabeAuthorityWeight)>`
- **interface**: `api.query.babe.authorities`
- **summary**:   Current epoch authorities. 
 
### authorVrfRandomness(): `MaybeRandomness`
- **interface**: `api.query.babe.authorVrfRandomness`
- **summary**:   Temporary value (cleared at block finalization) that includes the VRF output generated at this block. This field should always be populated during block processing unless secondary plain slots are enabled (which don't contain a VRF output). 
 
### currentSlot(): `Slot`
- **interface**: `api.query.babe.currentSlot`
- **summary**:   Current slot number. 
 
### epochConfig(): `Option<BabeEpochConfiguration>`
- **interface**: `api.query.babe.epochConfig`
- **summary**:   The configuration for the current epoch. Should never be `None` as it is initialized in genesis. 
 
### epochIndex(): `u64`
- **interface**: `api.query.babe.epochIndex`
- **summary**:   Current epoch index. 
 
### epochStart(): `(BlockNumber,BlockNumber)`
- **interface**: `api.query.babe.epochStart`
- **summary**:   The block numbers when the last and current epoch have started, respectively `N-1` and `N`. NOTE: We track this is in order to annotate the block number when a given pool of entropy was fixed (i.e. it was known to chain observers). Since epochs are defined in slots, which may be skipped, the block numbers may not line up with the slot numbers. 
 
### genesisSlot(): `Slot`
- **interface**: `api.query.babe.genesisSlot`
- **summary**:   The slot at which the first epoch actually started. This is 0 until the first block of the chain. 
 
### initialized(): `Option<MaybeRandomness>`
- **interface**: `api.query.babe.initialized`
- **summary**:   Temporary value (cleared at block finalization) which is `Some` if per-block initialization has already been called for current block. 
 
### lateness(): `BlockNumber`
- **interface**: `api.query.babe.lateness`
- **summary**:   How late the current block is compared to its parent. 

  This entry is populated as part of block execution and is cleaned up on block finalization. Querying this storage entry outside of block execution context should always yield zero. 
 
### nextAuthorities(): `Vec<(AuthorityId,BabeAuthorityWeight)>`
- **interface**: `api.query.babe.nextAuthorities`
- **summary**:   Next epoch authorities. 
 
### nextEpochConfig(): `Option<BabeEpochConfiguration>`
- **interface**: `api.query.babe.nextEpochConfig`
- **summary**:   The configuration for the next epoch, `None` if the config will not change (you can fallback to `EpochConfig` instead in that case). 
 
### nextRandomness(): `Randomness`
- **interface**: `api.query.babe.nextRandomness`
- **summary**:   Next epoch randomness. 
 
### pendingEpochConfigChange(): `Option<NextConfigDescriptor>`
- **interface**: `api.query.babe.pendingEpochConfigChange`
- **summary**:   Pending epoch configuration change that will be applied when the next epoch is enacted. 
 
### randomness(): `Randomness`
- **interface**: `api.query.babe.randomness`
- **summary**:   The epoch randomness for the *current* epoch. 

  #### Security 

  This MUST NOT be used for gambling, as it can be influenced by a malicious validator in the short term. It MAY be used in many cryptographic protocols, however, so long as one remembers that this (like everything else on-chain) it is public. For example, it can be used where a number is needed that cannot have been chosen by an adversary, for purposes such as public-coin zero-knowledge proofs. 
 
### segmentIndex(): `u32`
- **interface**: `api.query.babe.segmentIndex`
- **summary**:   Randomness under construction. 

  We make a tradeoff between storage accesses and list length. We store the under-construction randomness in segments of up to `UNDER_CONSTRUCTION_SEGMENT_LENGTH`. 

  Once a segment reaches this length, we begin the next one. We reset all segments and return to `0` at the beginning of every epoch. 
 
### underConstruction(`u32`): `Vec<Randomness>`
- **interface**: `api.query.babe.underConstruction`
- **summary**:   TWOX-NOTE: `SegmentIndex` is an increasing integer, so this is okay. 

___


## balances
 
### account(`AccountId`): `AccountData`
- **interface**: `api.query.balances.account`
- **summary**:   The balance of an account. 

  NOTE: This is only used in the case that this pallet is used to store balances. 
 
### locks(`AccountId`): `Vec<BalanceLock>`
- **interface**: `api.query.balances.locks`
- **summary**:   Any liquidity locks on some account balances. NOTE: Should only be accessed when setting, changing and freeing a lock. 
 
### reserves(`AccountId`): `Vec<ReserveData>`
- **interface**: `api.query.balances.reserves`
- **summary**:   Named reserves on some account balances. 
 
### storageVersion(): `Releases`
- **interface**: `api.query.balances.storageVersion`
- **summary**:   Storage version of the pallet. 

  This is set to v2.0.0 for new networks. 
 
### totalIssuance(): `Balance`
- **interface**: `api.query.balances.totalIssuance`
- **summary**:   The total units issued in the system. 

___


## bounties
 
### bounties(`BountyIndex`): `Option<Bounty>`
- **interface**: `api.query.bounties.bounties`
- **summary**:   Bounties that have been made. 
 
### bountyApprovals(): `Vec<BountyIndex>`
- **interface**: `api.query.bounties.bountyApprovals`
- **summary**:   Bounty indices that have been approved but not yet funded. 
 
### bountyCount(): `BountyIndex`
- **interface**: `api.query.bounties.bountyCount`
- **summary**:   Number of bounty proposals that have been made. 
 
### bountyDescriptions(`BountyIndex`): `Option<Bytes>`
- **interface**: `api.query.bounties.bountyDescriptions`
- **summary**:   The description of each bounty. 

___


## contracts
 
### accountCounter(): `u64`
- **interface**: `api.query.contracts.accountCounter`
- **summary**:   The subtrie counter. 
 
### codeStorage(`CodeHash`): `Option<PrefabWasmModule>`
- **interface**: `api.query.contracts.codeStorage`
- **summary**:   A mapping between an original code hash and instrumented wasm code, ready for execution. 
 
### contractInfoOf(`AccountId`): `Option<ContractInfo>`
- **interface**: `api.query.contracts.contractInfoOf`
- **summary**:   The code associated with a given account. 

  TWOX-NOTE: SAFE since `AccountId` is a secure hash. 
 
### deletionQueue(): `Vec<DeletedContract>`
- **interface**: `api.query.contracts.deletionQueue`
- **summary**:   Evicted contracts that await child trie deletion. 

  Child trie deletion is a heavy operation depending on the amount of storage items stored in said trie. Therefore this operation is performed lazily in `on_initialize`. 
 
### pristineCode(`CodeHash`): `Option<Bytes>`
- **interface**: `api.query.contracts.pristineCode`
- **summary**:   A mapping from an original code hash to the original code, untouched by instrumentation. 

___


## council
 
### members(): `Vec<AccountId>`
- **interface**: `api.query.council.members`
- **summary**:   The current members of the collective. This is stored sorted (just by value). 
 
### prime(): `Option<AccountId>`
- **interface**: `api.query.council.prime`
- **summary**:   The prime member that helps determine the default vote behavior in case of absentations. 
 
### proposalCount(): `u32`
- **interface**: `api.query.council.proposalCount`
- **summary**:   Proposals so far. 
 
### proposalOf(`Hash`): `Option<Proposal>`
- **interface**: `api.query.council.proposalOf`
- **summary**:   Actual proposal for a given hash, if it's current. 
 
### proposals(): `Vec<Hash>`
- **interface**: `api.query.council.proposals`
- **summary**:   The hashes of the active proposals. 
 
### voting(`Hash`): `Option<Votes>`
- **interface**: `api.query.council.voting`
- **summary**:   Votes on a given proposal, if it is ongoing. 

___


## democracy
 
### blacklist(`Hash`): `Option<(BlockNumber,Vec<AccountId>)>`
- **interface**: `api.query.democracy.blacklist`
- **summary**:   A record of who vetoed what. Maps proposal hash to a possible existent block number (until when it may not be resubmitted) and who vetoed it. 
 
### cancellations(`Hash`): `bool`
- **interface**: `api.query.democracy.cancellations`
- **summary**:   Record of all proposals that have been subject to emergency cancellation. 
 
### depositOf(`PropIndex`): `Option<(Vec<AccountId>,BalanceOf)>`
- **interface**: `api.query.democracy.depositOf`
- **summary**:   Those who have locked a deposit. 

  TWOX-NOTE: Safe, as increasing integer keys are safe. 
 
### lastTabledWasExternal(): `bool`
- **interface**: `api.query.democracy.lastTabledWasExternal`
- **summary**:   True if the last referendum tabled was submitted externally. False if it was a public proposal. 
 
### locks(`AccountId`): `Option<BlockNumber>`
- **interface**: `api.query.democracy.locks`
- **summary**:   Accounts for which there are locks in action which may be removed at some point in the future. The value is the block number at which the lock expires and may be removed. 

  TWOX-NOTE: OK ― `AccountId` is a secure hash. 
 
### lowestUnbaked(): `ReferendumIndex`
- **interface**: `api.query.democracy.lowestUnbaked`
- **summary**:   The lowest referendum index representing an unbaked referendum. Equal to `ReferendumCount` if there isn't a unbaked referendum. 
 
### nextExternal(): `Option<(Hash,VoteThreshold)>`
- **interface**: `api.query.democracy.nextExternal`
- **summary**:   The referendum to be tabled whenever it would be valid to table an external proposal. This happens when a referendum needs to be tabled and one of two conditions are met: 

  - `LastTabledWasExternal` is `false`; or

  - `PublicProps` is empty.
 
### preimages(`Hash`): `Option<PreimageStatus>`
- **interface**: `api.query.democracy.preimages`
- **summary**:   Map of hashes to the proposal preimage, along with who registered it and their deposit. The block number is the block at which it was deposited. 
 
### publicPropCount(): `PropIndex`
- **interface**: `api.query.democracy.publicPropCount`
- **summary**:   The number of (public) proposals that have been made so far. 
 
### publicProps(): `Vec<(PropIndex,Hash,AccountId)>`
- **interface**: `api.query.democracy.publicProps`
- **summary**:   The public proposals. Unsorted. The second item is the proposal's hash. 
 
### referendumCount(): `ReferendumIndex`
- **interface**: `api.query.democracy.referendumCount`
- **summary**:   The next free referendum index, aka the number of referenda started so far. 
 
### referendumInfoOf(`ReferendumIndex`): `Option<ReferendumInfo>`
- **interface**: `api.query.democracy.referendumInfoOf`
- **summary**:   Information concerning any given referendum. 

  TWOX-NOTE: SAFE as indexes are not under an attacker’s control. 
 
### storageVersion(): `Option<Releases>`
- **interface**: `api.query.democracy.storageVersion`
- **summary**:   Storage version of the pallet. 

  New networks start with last version. 
 
### votingOf(`AccountId`): `Voting`
- **interface**: `api.query.democracy.votingOf`
- **summary**:   All votes for a particular voter. We store the balance for the number of votes that we have recorded. The second item is the total amount of delegations, that will be added. 

  TWOX-NOTE: SAFE as `AccountId`s are crypto hashes anyway. 

___


## electionProviderMultiPhase
 
### currentPhase(): `ElectionPhase`
- **interface**: `api.query.electionProviderMultiPhase.currentPhase`
- **summary**:   Current phase. 
 
### desiredTargets(): `Option<u32>`
- **interface**: `api.query.electionProviderMultiPhase.desiredTargets`
- **summary**:   Desired number of targets to elect for this round. 

  Only exists when [`Snapshot`] is present. 
 
### minimumUntrustedScore(): `Option<ElectionScore>`
- **interface**: `api.query.electionProviderMultiPhase.minimumUntrustedScore`
- **summary**:   The minimum score that each 'untrusted' solution must attain in order to be considered feasible. 

  Can be set via `set_minimum_untrusted_score`. 
 
### queuedSolution(): `Option<ReadySolution>`
- **interface**: `api.query.electionProviderMultiPhase.queuedSolution`
- **summary**:   Current best solution, signed or unsigned, queued to be returned upon `elect`. 
 
### round(): `u32`
- **interface**: `api.query.electionProviderMultiPhase.round`
- **summary**:   Internal counter for the number of rounds. 

  This is useful for de-duplication of transactions submitted to the pool, and general diagnostics of the pallet. 

  This is merely incremented once per every time that an upstream `elect` is called. 
 
### snapshot(): `Option<RoundSnapshot>`
- **interface**: `api.query.electionProviderMultiPhase.snapshot`
- **summary**:   Snapshot data of the round. 

  This is created at the beginning of the signed phase and cleared upon calling `elect`. 
 
### snapshotMetadata(): `Option<SolutionOrSnapshotSize>`
- **interface**: `api.query.electionProviderMultiPhase.snapshotMetadata`
- **summary**:   The metadata of the [`RoundSnapshot`] 

  Only exists when [`Snapshot`] is present. 

___


## elections
 
### candidates(): `Vec<(AccountId,BalanceOf)>`
- **interface**: `api.query.elections.candidates`
- **summary**:   The present candidate list. A current member or runner-up can never enter this vector and is always implicitly assumed to be a candidate. 

  Second element is the deposit. 

  Invariant: Always sorted based on account id. 
 
### electionRounds(): `u32`
- **interface**: `api.query.elections.electionRounds`
- **summary**:   The total number of vote rounds that have happened, excluding the upcoming one. 
 
### members(): `Vec<SeatHolder>`
- **interface**: `api.query.elections.members`
- **summary**:   The current elected members. 

  Invariant: Always sorted based on account id. 
 
### runnersUp(): `Vec<SeatHolder>`
- **interface**: `api.query.elections.runnersUp`
- **summary**:   The current reserved runners-up. 

  Invariant: Always sorted based on rank (worse to best). Upon removal of a member, the last (i.e. _best_) runner-up will be replaced. 
 
### voting(`AccountId`): `Voter`
- **interface**: `api.query.elections.voting`
- **summary**:   Votes and locked stake of a particular voter. 

  TWOX-NOTE: SAFE as `AccountId` is a crypto hash. 

___


## gilt
 
### active(`ActiveIndex`): `Option<ActiveGilt>`
- **interface**: `api.query.gilt.active`
- **summary**:   The currently active gilts, indexed according to the order of creation. 
 
### activeTotal(): `ActiveGiltsTotal`
- **interface**: `api.query.gilt.activeTotal`
- **summary**:   Information relating to the gilts currently active. 
 
### queues(`u32`): `Vec<GiltBid>`
- **interface**: `api.query.gilt.queues`
- **summary**:   The queues of bids ready to become gilts. Indexed by duration (in `Period`s). 
 
### queueTotals(): `Vec<(u32,BalanceOf)>`
- **interface**: `api.query.gilt.queueTotals`
- **summary**:   The totals of items and balances within each queue. Saves a lot of storage reads in the case of sparsely packed queues. 

  The vector is indexed by duration in `Period`s, offset by one, so information on the queue whose duration is one `Period` would be storage `0`. 

___


## grandpa
 
### currentSetId(): `SetId`
- **interface**: `api.query.grandpa.currentSetId`
- **summary**:   The number of changes (both in terms of keys and underlying economic responsibilities) in the "set" of Grandpa validators from genesis. 
 
### nextForced(): `Option<BlockNumber>`
- **interface**: `api.query.grandpa.nextForced`
- **summary**:   next block number where we can force a change. 
 
### pendingChange(): `Option<StoredPendingChange>`
- **interface**: `api.query.grandpa.pendingChange`
- **summary**:   Pending change: (signaled at, scheduled change). 
 
### setIdSession(`SetId`): `Option<SessionIndex>`
- **interface**: `api.query.grandpa.setIdSession`
- **summary**:   A mapping from grandpa set ID to the index of the *most recent* session for which its members were responsible. 

  TWOX-NOTE: `SetId` is not under user control. 
 
### stalled(): `Option<(BlockNumber,BlockNumber)>`
- **interface**: `api.query.grandpa.stalled`
- **summary**:   `true` if we are currently stalled. 
 
### state(): `StoredState`
- **interface**: `api.query.grandpa.state`
- **summary**:   State of the current authority set. 

___


## identity
 
### identityOf(`AccountId`): `Option<Registration>`
- **interface**: `api.query.identity.identityOf`
- **summary**:   Information that is pertinent to identify the entity behind an account. 

  TWOX-NOTE: OK ― `AccountId` is a secure hash. 
 
### registrars(): `Vec<Option<RegistrarInfo>>`
- **interface**: `api.query.identity.registrars`
- **summary**:   The set of registrars. Not expected to get very big as can only be added through a special origin (likely a council motion). 

  The index into this can be cast to `RegistrarIndex` to get a valid value. 
 
### subsOf(`AccountId`): `(BalanceOf,Vec<AccountId>)`
- **interface**: `api.query.identity.subsOf`
- **summary**:   Alternative "sub" identities of this account. 

  The first item is the deposit, the second is a vector of the accounts. 

  TWOX-NOTE: OK ― `AccountId` is a secure hash. 
 
### superOf(`AccountId`): `Option<(AccountId,Data)>`
- **interface**: `api.query.identity.superOf`
- **summary**:   The super-identity of an alternative "sub" identity together with its name, within that context. If the account is not some other account's sub-identity, then just `None`. 

___


## imOnline
 
### authoredBlocks(`SessionIndex, ValidatorId`): `u32`
- **interface**: `api.query.imOnline.authoredBlocks`
- **summary**:   For each session index, we keep a mapping of `ValidatorId<T>` to the number of blocks authored by the given authority. 
 
### heartbeatAfter(): `BlockNumber`
- **interface**: `api.query.imOnline.heartbeatAfter`
- **summary**:   The block number after which it's ok to send heartbeats in the current session. 

  At the beginning of each session we set this to a value that should fall roughly in the middle of the session duration. The idea is to first wait for the validators to produce a block in the current session, so that the heartbeat later on will not be necessary. 

  This value will only be used as a fallback if we fail to get a proper session progress estimate from `NextSessionRotation`, as those estimates should be more accurate then the value we calculate for `HeartbeatAfter`. 
 
### keys(): `Vec<AuthorityId>`
- **interface**: `api.query.imOnline.keys`
- **summary**:   The current set of keys that may issue a heartbeat. 
 
### receivedHeartbeats(`SessionIndex, AuthIndex`): `Option<Bytes>`
- **interface**: `api.query.imOnline.receivedHeartbeats`
- **summary**:   For each session index, we keep a mapping of `AuthIndex` to `offchain::OpaqueNetworkState`. 

___


## indices
 
### accounts(`AccountIndex`): `Option<(AccountId,BalanceOf,bool)>`
- **interface**: `api.query.indices.accounts`
- **summary**:   The lookup from index to account. 

___


## lottery
 
### callIndices(): `Vec<CallIndex>`
- **interface**: `api.query.lottery.callIndices`
- **summary**:   The calls stored in this pallet to be used in an active lottery if configured by `Config::ValidateCall`. 
 
### lottery(): `Option<LotteryConfig>`
- **interface**: `api.query.lottery.lottery`
- **summary**:   The configuration for the current lottery. 
 
### lotteryIndex(): `u32`
- **interface**: `api.query.lottery.lotteryIndex`
 
### participants(`AccountId`): `(u32,Vec<CallIndex>)`
- **interface**: `api.query.lottery.participants`
- **summary**:   Users who have purchased a ticket. (Lottery Index, Tickets Purchased) 
 
### tickets(`u32`): `Option<AccountId>`
- **interface**: `api.query.lottery.tickets`
- **summary**:   Each ticket's owner. 

  May have residual storage from previous lotteries. Use `TicketsCount` to see which ones are actually valid ticket mappings. 
 
### ticketsCount(): `u32`
- **interface**: `api.query.lottery.ticketsCount`
- **summary**:   Total number of tickets sold. 

___


## mmr
 
### nodes(`u64`): `Option<Hash>`
- **interface**: `api.query.mmr.nodes`
- **summary**:   Hashes of the nodes in the MMR. 

  Note this collection only contains MMR peaks, the inner nodes (and leaves) are pruned and only stored in the Offchain DB. 
 
### numberOfLeaves(): `u64`
- **interface**: `api.query.mmr.numberOfLeaves`
- **summary**:   Current size of the MMR (number of leaves). 
 
### rootHash(): `Hash`
- **interface**: `api.query.mmr.rootHash`
- **summary**:   Latest MMR Root hash. 

___


## multisig
 
### calls(`[u8;32]`): `Option<(OpaqueCall,AccountId,BalanceOf)>`
- **interface**: `api.query.multisig.calls`
 
### multisigs(`AccountId, [u8;32]`): `Option<Multisig>`
- **interface**: `api.query.multisig.multisigs`
- **summary**:   The set of open multisig operations. 

___


## offences
 
### concurrentReportsIndex(`Kind, OpaqueTimeSlot`): `Vec<ReportIdOf>`
- **interface**: `api.query.offences.concurrentReportsIndex`
- **summary**:   A vector of reports of the same kind that happened at the same time slot. 
 
### reports(`ReportIdOf`): `Option<OffenceDetails>`
- **interface**: `api.query.offences.reports`
- **summary**:   The primary structure that holds all offence records keyed by report identifiers. 
 
### reportsByKindIndex(`Kind`): `Bytes`
- **interface**: `api.query.offences.reportsByKindIndex`
- **summary**:   Enumerates all reports of a kind along with the time they happened. 

  All reports are sorted by the time of offence. 

  Note that the actual type of this mapping is `Vec<u8>`, this is because values of different types are not supported at the moment so we are doing the manual serialization. 

___


## proxy
 
### announcements(`AccountId`): `(Vec<ProxyAnnouncement>,BalanceOf)`
- **interface**: `api.query.proxy.announcements`
- **summary**:   The announcements made by the proxy (key). 
 
### proxies(`AccountId`): `(Vec<ProxyDefinition>,BalanceOf)`
- **interface**: `api.query.proxy.proxies`
- **summary**:   The set of account proxies. Maps the account which has delegated to the accounts which are being delegated to, together with the amount held on deposit. 

___


## randomnessCollectiveFlip
 
### randomMaterial(): `Vec<Hash>`
- **interface**: `api.query.randomnessCollectiveFlip.randomMaterial`
- **summary**:   Series of block headers from the last 81 blocks that acts as random seed material. This is arranged as a ring buffer with `block_number % 81` being the index into the `Vec` of the oldest hash. 

___


## recovery
 
### activeRecoveries(`AccountId, AccountId`): `Option<ActiveRecovery>`
- **interface**: `api.query.recovery.activeRecoveries`
- **summary**:   Active recovery attempts. 

  First account is the account to be recovered, and the second account is the user trying to recover the account. 
 
### proxy(`AccountId`): `Option<AccountId>`
- **interface**: `api.query.recovery.proxy`
- **summary**:   The list of allowed proxy accounts. 

  Map from the user who can access it to the recovered account. 
 
### recoverable(`AccountId`): `Option<RecoveryConfig>`
- **interface**: `api.query.recovery.recoverable`
- **summary**:   The set of recoverable accounts and their recovery configuration. 

___


## scheduler
 
### agenda(`BlockNumber`): `Vec<Option<Scheduled>>`
- **interface**: `api.query.scheduler.agenda`
- **summary**:   Items to be executed, indexed by the block number that they should be executed on. 
 
### lookup(`Bytes`): `Option<TaskAddress>`
- **interface**: `api.query.scheduler.lookup`
- **summary**:   Lookup from identity to the block number and index of the task. 
 
### storageVersion(): `Releases`
- **interface**: `api.query.scheduler.storageVersion`
- **summary**:   Storage version of the pallet. 

  New networks start with last version. 

___


## session
 
### currentIndex(): `SessionIndex`
- **interface**: `api.query.session.currentIndex`
- **summary**:   Current index of the session. 
 
### disabledValidators(): `Vec<u32>`
- **interface**: `api.query.session.disabledValidators`
- **summary**:   Indices of disabled validators. 

  The set is cleared when `on_session_ending` returns a new set of identities. 
 
### keyOwner(`(KeyTypeId,Bytes)`): `Option<ValidatorId>`
- **interface**: `api.query.session.keyOwner`
- **summary**:   The owner of a key. The key is the `KeyTypeId` + the encoded key. 
 
### nextKeys(`ValidatorId`): `Option<Keys>`
- **interface**: `api.query.session.nextKeys`
- **summary**:   The next session keys for a validator. 
 
### queuedChanged(): `bool`
- **interface**: `api.query.session.queuedChanged`
- **summary**:   True if the underlying economic identities or weighting behind the validators has changed in the queued validator set. 
 
### queuedKeys(): `Vec<(ValidatorId,Keys)>`
- **interface**: `api.query.session.queuedKeys`
- **summary**:   The queued keys for the next session. When the next session begins, these keys will be used to determine the validator's session keys. 
 
### validators(): `Vec<ValidatorId>`
- **interface**: `api.query.session.validators`
- **summary**:   The current set of validators. 

___


## society
 
### bids(): `Vec<Bid>`
- **interface**: `api.query.society.bids`
- **summary**:   The current bids, stored ordered by the value of the bid. 
 
### candidates(): `Vec<Bid>`
- **interface**: `api.query.society.candidates`
- **summary**:   The current set of candidates; bidders that are attempting to become members. 
 
### defender(): `Option<AccountId>`
- **interface**: `api.query.society.defender`
- **summary**:   The defending member currently being challenged. 
 
### defenderVotes(`AccountId`): `Option<SocietyVote>`
- **interface**: `api.query.society.defenderVotes`
- **summary**:   Votes for the defender. 
 
### founder(): `Option<AccountId>`
- **interface**: `api.query.society.founder`
- **summary**:   The first member. 
 
### head(): `Option<AccountId>`
- **interface**: `api.query.society.head`
- **summary**:   The most primary from the most recently approved members. 
 
### maxMembers(): `u32`
- **interface**: `api.query.society.maxMembers`
- **summary**:   The max number of members for the society at one time. 
 
### members(): `Vec<AccountId>`
- **interface**: `api.query.society.members`
- **summary**:   The current set of members, ordered. 
 
### payouts(`AccountId`): `Vec<(BlockNumber,BalanceOf)>`
- **interface**: `api.query.society.payouts`
- **summary**:   Pending payouts; ordered by block number, with the amount that should be paid out. 
 
### pot(): `BalanceOf`
- **interface**: `api.query.society.pot`
- **summary**:   Amount of our account balance that is specifically for the next round's bid(s). 
 
### rules(): `Option<Hash>`
- **interface**: `api.query.society.rules`
- **summary**:   A hash of the rules of this society concerning membership. Can only be set once and only by the founder. 
 
### strikes(`AccountId`): `StrikeCount`
- **interface**: `api.query.society.strikes`
- **summary**:   The ongoing number of losing votes cast by the member. 
 
### suspendedCandidates(`AccountId`): `Option<(BalanceOf,BidKind)>`
- **interface**: `api.query.society.suspendedCandidates`
- **summary**:   The set of suspended candidates. 
 
### suspendedMembers(`AccountId`): `bool`
- **interface**: `api.query.society.suspendedMembers`
- **summary**:   The set of suspended members. 
 
### votes(`AccountId, AccountId`): `Option<SocietyVote>`
- **interface**: `api.query.society.votes`
- **summary**:   Double map from Candidate -> Voter -> (Maybe) Vote. 
 
### vouching(`AccountId`): `Option<VouchingStatus>`
- **interface**: `api.query.society.vouching`
- **summary**:   Members currently vouching or banned from vouching again 

___


## staking
 
### activeEra(): `Option<ActiveEraInfo>`
- **interface**: `api.query.staking.activeEra`
- **summary**:   The active era information, it holds index and start. 

  The active era is the era being currently rewarded. Validator set of this era must be equal to [`SessionInterface::validators`]. 
 
### bonded(`AccountId`): `Option<AccountId>`
- **interface**: `api.query.staking.bonded`
- **summary**:   Map from all locked "stash" accounts to the controller account. 
 
### bondedEras(): `Vec<(EraIndex,SessionIndex)>`
- **interface**: `api.query.staking.bondedEras`
- **summary**:   A mapping from still-bonded eras to the first session index of that era. 

  Must contains information for eras for the range: `[active_era - bounding_duration; active_era]` 
 
### canceledSlashPayout(): `BalanceOf`
- **interface**: `api.query.staking.canceledSlashPayout`
- **summary**:   The amount of currency given to reporters of a slash event which was canceled by extraordinary circumstances (e.g. governance). 
 
### currentEra(): `Option<EraIndex>`
- **interface**: `api.query.staking.currentEra`
- **summary**:   The current era index. 

  This is the latest planned era, depending on how the Session pallet queues the validator set, it might be active or not. 
 
### currentPlannedSession(): `SessionIndex`
- **interface**: `api.query.staking.currentPlannedSession`
- **summary**:   The last planned session scheduled by the session pallet. 

  This is basically in sync with the call to [`SessionManager::new_session`]. 
 
### earliestUnappliedSlash(): `Option<EraIndex>`
- **interface**: `api.query.staking.earliestUnappliedSlash`
- **summary**:   The earliest era for which we have a pending, unapplied slash. 
 
### erasRewardPoints(`EraIndex`): `EraRewardPoints`
- **interface**: `api.query.staking.erasRewardPoints`
- **summary**:   Rewards for the last `HISTORY_DEPTH` eras. If reward hasn't been set or has been removed then 0 reward is returned. 
 
### erasStakers(`EraIndex, AccountId`): `Exposure`
- **interface**: `api.query.staking.erasStakers`
- **summary**:   Exposure of validator at era. 

  This is keyed first by the era index to allow bulk deletion and then the stash account. 

  Is it removed after `HISTORY_DEPTH` eras. If stakers hasn't been set or has been removed then empty exposure is returned. 
 
### erasStakersClipped(`EraIndex, AccountId`): `Exposure`
- **interface**: `api.query.staking.erasStakersClipped`
- **summary**:   Clipped Exposure of validator at era. 

  This is similar to [`ErasStakers`] but number of nominators exposed is reduced to the `T::MaxNominatorRewardedPerValidator` biggest stakers. (Note: the field `total` and `own` of the exposure remains unchanged). This is used to limit the i/o cost for the nominator payout. 

  This is keyed fist by the era index to allow bulk deletion and then the stash account. 

  Is it removed after `HISTORY_DEPTH` eras. If stakers hasn't been set or has been removed then empty exposure is returned. 
 
### erasStartSessionIndex(`EraIndex`): `Option<SessionIndex>`
- **interface**: `api.query.staking.erasStartSessionIndex`
- **summary**:   The session index at which the era start for the last `HISTORY_DEPTH` eras. 

  Note: This tracks the starting session (i.e. session index when era start being active) for the eras in `[CurrentEra - HISTORY_DEPTH, CurrentEra]`. 
 
### erasTotalStake(`EraIndex`): `BalanceOf`
- **interface**: `api.query.staking.erasTotalStake`
- **summary**:   The total amount staked for the last `HISTORY_DEPTH` eras. If total hasn't been set or has been removed then 0 stake is returned. 
 
### erasValidatorPrefs(`EraIndex, AccountId`): `ValidatorPrefs`
- **interface**: `api.query.staking.erasValidatorPrefs`
- **summary**:   Similar to `ErasStakers`, this holds the preferences of validators. 

  This is keyed first by the era index to allow bulk deletion and then the stash account. 

  Is it removed after `HISTORY_DEPTH` eras. 
 
### erasValidatorReward(`EraIndex`): `Option<BalanceOf>`
- **interface**: `api.query.staking.erasValidatorReward`
- **summary**:   The total validator era payout for the last `HISTORY_DEPTH` eras. 

  Eras that haven't finished yet or has been removed doesn't have reward. 
 
### forceEra(): `Forcing`
- **interface**: `api.query.staking.forceEra`
- **summary**:   Mode of era forcing. 
 
### historyDepth(): `u32`
- **interface**: `api.query.staking.historyDepth`
- **summary**:   Number of eras to keep in history. 

  Information is kept for eras in `[current_era - history_depth; current_era]`. 

  Must be more than the number of eras delayed by session otherwise. I.e. active era must always be in history. I.e. `active_era > current_era - history_depth` must be guaranteed. 
 
### invulnerables(): `Vec<AccountId>`
- **interface**: `api.query.staking.invulnerables`
- **summary**:   Any validators that may never be slashed or forcibly kicked. It's a Vec since they're easy to initialize and the performance hit is minimal (we expect no more than four invulnerables) and restricted to testnets. 
 
### ledger(`AccountId`): `Option<StakingLedger>`
- **interface**: `api.query.staking.ledger`
- **summary**:   Map from all (unlocked) "controller" accounts to the info regarding the staking. 
 
### minimumValidatorCount(): `u32`
- **interface**: `api.query.staking.minimumValidatorCount`
- **summary**:   Minimum number of staking participants before emergency conditions are imposed. 
 
### nominators(`AccountId`): `Option<Nominations>`
- **interface**: `api.query.staking.nominators`
- **summary**:   The map from nominator stash key to the set of stash keys of all validators to nominate. 
 
### nominatorSlashInEra(`EraIndex, AccountId`): `Option<BalanceOf>`
- **interface**: `api.query.staking.nominatorSlashInEra`
- **summary**:   All slashing events on nominators, mapped by era to the highest slash value of the era. 
 
### payee(`AccountId`): `RewardDestination`
- **interface**: `api.query.staking.payee`
- **summary**:   Where the reward payment should be made. Keyed by stash. 
 
### slashingSpans(`AccountId`): `Option<SlashingSpans>`
- **interface**: `api.query.staking.slashingSpans`
- **summary**:   Slashing spans for stash accounts. 
 
### slashRewardFraction(): `Perbill`
- **interface**: `api.query.staking.slashRewardFraction`
- **summary**:   The percentage of the slash that is distributed to reporters. 

  The rest of the slashed value is handled by the `Slash`. 
 
### spanSlash(`(AccountId,SpanIndex)`): `SpanRecord`
- **interface**: `api.query.staking.spanSlash`
- **summary**:   Records information about the maximum slash of a stash within a slashing span, as well as how much reward has been paid out. 
 
### storageVersion(): `Releases`
- **interface**: `api.query.staking.storageVersion`
- **summary**:   True if network has been upgraded to this version. Storage version of the pallet. 

  This is set to v6.0.0 for new networks. 
 
### unappliedSlashes(`EraIndex`): `Vec<UnappliedSlash>`
- **interface**: `api.query.staking.unappliedSlashes`
- **summary**:   All unapplied slashes that are queued for later. 
 
### validatorCount(): `u32`
- **interface**: `api.query.staking.validatorCount`
- **summary**:   The ideal number of staking participants. 
 
### validators(`AccountId`): `ValidatorPrefs`
- **interface**: `api.query.staking.validators`
- **summary**:   The map from (wannabe) validator stash key to the preferences of that validator. 
 
### validatorSlashInEra(`EraIndex, AccountId`): `Option<(Perbill,BalanceOf)>`
- **interface**: `api.query.staking.validatorSlashInEra`
- **summary**:   All slashing events on validators, mapped by era to the highest slash proportion and slash value of the era. 

___


## substrate

_These are well-known keys that are always available to the runtime implementation of any Substrate-based network._
 
### changesTrieConfig(): `u32`
- **interface**: `api.query.substrate.changesTrieConfig`
- **summary**:   Changes trie configuration is stored under this key. 
 
### childStorageKeyPrefix(): `u32`
- **interface**: `api.query.substrate.childStorageKeyPrefix`
- **summary**:   Prefix of child storage keys. 
 
### code(): `Bytes`
- **interface**: `api.query.substrate.code`
- **summary**:   Wasm code of the runtime. 
 
### extrinsicIndex(): `u32`
- **interface**: `api.query.substrate.extrinsicIndex`
- **summary**:   Current extrinsic index (u32) is stored under this key. 
 
### heapPages(): `u64`
- **interface**: `api.query.substrate.heapPages`
- **summary**:   Number of wasm linear memory pages required for execution of the runtime. 

___


## sudo
 
### key(): `AccountId`
- **interface**: `api.query.sudo.key`
- **summary**:   The `AccountId` of the sudo key. 

___


## system
 
### account(`AccountId`): `AccountInfo`
- **interface**: `api.query.system.account`
- **summary**:   The full account information for a particular account ID. 
 
### allExtrinsicsLen(): `Option<u32>`
- **interface**: `api.query.system.allExtrinsicsLen`
- **summary**:   Total length (in bytes) for all extrinsics put together, for the current block. 
 
### blockHash(`BlockNumber`): `Hash`
- **interface**: `api.query.system.blockHash`
- **summary**:   Map of block numbers to block hashes. 
 
### blockWeight(): `ConsumedWeight`
- **interface**: `api.query.system.blockWeight`
- **summary**:   The current weight for the block. 
 
### digest(): `DigestOf`
- **interface**: `api.query.system.digest`
- **summary**:   Digest of the current block, also part of the block header. 
 
### eventCount(): `EventIndex`
- **interface**: `api.query.system.eventCount`
- **summary**:   The number of events in the `Events<T>` list. 
 
### events(): `Vec<EventRecord>`
- **interface**: `api.query.system.events`
- **summary**:   Events deposited for the current block. 
 
### eventTopics(`Hash`): `Vec<(BlockNumber,EventIndex)>`
- **interface**: `api.query.system.eventTopics`
- **summary**:   Mapping between a topic (represented by T::Hash) and a vector of indexes of events in the `<Events<T>>` list. 

  All topic vectors have deterministic storage locations depending on the topic. This allows light-clients to leverage the changes trie storage tracking mechanism and in case of changes fetch the list of events of interest. 

  The value has the type `(T::BlockNumber, EventIndex)` because if we used only just the `EventIndex` then in case if the topic has the same contents on the next block no notification will be triggered thus the event might be lost. 
 
### executionPhase(): `Option<Phase>`
- **interface**: `api.query.system.executionPhase`
- **summary**:   The execution phase of the block. 
 
### extrinsicCount(): `Option<u32>`
- **interface**: `api.query.system.extrinsicCount`
- **summary**:   Total extrinsics count for the current block. 
 
### extrinsicData(`u32`): `Bytes`
- **interface**: `api.query.system.extrinsicData`
- **summary**:   Extrinsics data for the current block (maps an extrinsic's index to its data). 
 
### lastRuntimeUpgrade(): `Option<LastRuntimeUpgradeInfo>`
- **interface**: `api.query.system.lastRuntimeUpgrade`
- **summary**:   Stores the `spec_version` and `spec_name` of when the last runtime upgrade happened. 
 
### number(): `BlockNumber`
- **interface**: `api.query.system.number`
- **summary**:   The current block number being processed. Set by `execute_block`. 
 
### parentHash(): `Hash`
- **interface**: `api.query.system.parentHash`
- **summary**:   Hash of the previous block. 
 
### upgradedToTripleRefCount(): `bool`
- **interface**: `api.query.system.upgradedToTripleRefCount`
- **summary**:   True if we have upgraded so that AccountInfo contains three types of `RefCount`. False (default) if not. 
 
### upgradedToU32RefCount(): `bool`
- **interface**: `api.query.system.upgradedToU32RefCount`
- **summary**:   True if we have upgraded so that `type RefCount` is `u32`. False (default) if not. 

___


## technicalCommittee
 
### members(): `Vec<AccountId>`
- **interface**: `api.query.technicalCommittee.members`
- **summary**:   The current members of the collective. This is stored sorted (just by value). 
 
### prime(): `Option<AccountId>`
- **interface**: `api.query.technicalCommittee.prime`
- **summary**:   The prime member that helps determine the default vote behavior in case of absentations. 
 
### proposalCount(): `u32`
- **interface**: `api.query.technicalCommittee.proposalCount`
- **summary**:   Proposals so far. 
 
### proposalOf(`Hash`): `Option<Proposal>`
- **interface**: `api.query.technicalCommittee.proposalOf`
- **summary**:   Actual proposal for a given hash, if it's current. 
 
### proposals(): `Vec<Hash>`
- **interface**: `api.query.technicalCommittee.proposals`
- **summary**:   The hashes of the active proposals. 
 
### voting(`Hash`): `Option<Votes>`
- **interface**: `api.query.technicalCommittee.voting`
- **summary**:   Votes on a given proposal, if it is ongoing. 

___


## technicalMembership
 
### members(): `Vec<AccountId>`
- **interface**: `api.query.technicalMembership.members`
- **summary**:   The current membership, stored as an ordered Vec. 
 
### prime(): `Option<AccountId>`
- **interface**: `api.query.technicalMembership.prime`
- **summary**:   The current prime member, if one exists. 

___


## timestamp
 
### didUpdate(): `bool`
- **interface**: `api.query.timestamp.didUpdate`
- **summary**:   Did the timestamp get updated in this block? 
 
### now(): `Moment`
- **interface**: `api.query.timestamp.now`
- **summary**:   Current time for the current block. 

___


## tips
 
### reasons(`Hash`): `Option<Bytes>`
- **interface**: `api.query.tips.reasons`
- **summary**:   Simple preimage lookup from the reason's hash to the original data. Again, has an insecure enumerable hash since the key is guaranteed to be the result of a secure hash. 
 
### tips(`Hash`): `Option<OpenTip>`
- **interface**: `api.query.tips.tips`
- **summary**:   TipsMap that are not yet completed. Keyed by the hash of `(reason, who)` from the value. This has the insecure enumerable hash function since the key itself is already guaranteed to be a secure hash. 

___


## transactionPayment
 
### nextFeeMultiplier(): `Multiplier`
- **interface**: `api.query.transactionPayment.nextFeeMultiplier`
 
### storageVersion(): `Releases`
- **interface**: `api.query.transactionPayment.storageVersion`

___


## transactionStorage
 
### blockTransactions(): `Vec<TransactionInfo>`
- **interface**: `api.query.transactionStorage.blockTransactions`
 
### byteFee(): `Option<BalanceOf>`
- **interface**: `api.query.transactionStorage.byteFee`
- **summary**:   Storage fee per byte. 
 
### chunkCount(`BlockNumber`): `u32`
- **interface**: `api.query.transactionStorage.chunkCount`
- **summary**:   Count indexed chunks for each block. 
 
### entryFee(): `Option<BalanceOf>`
- **interface**: `api.query.transactionStorage.entryFee`
- **summary**:   Storage fee per transaction. 
 
### maxBlockTransactions(): `u32`
- **interface**: `api.query.transactionStorage.maxBlockTransactions`
- **summary**:   Maximum number of indexed transactions in the block. 
 
### maxTransactionSize(): `u32`
- **interface**: `api.query.transactionStorage.maxTransactionSize`
- **summary**:   Maximum data set in a single transaction in bytes. 
 
### proofChecked(): `bool`
- **interface**: `api.query.transactionStorage.proofChecked`
- **summary**:   Was the proof checked in this block? 
 
### storagePeriod(): `BlockNumber`
- **interface**: `api.query.transactionStorage.storagePeriod`
- **summary**:   Storage period for data in blocks. Should match `sp_storage_proof::DEFAULT_STORAGE_PERIOD` for block authoring. 
 
### transactions(`BlockNumber`): `Option<Vec<TransactionInfo>>`
- **interface**: `api.query.transactionStorage.transactions`
- **summary**:   Collection of transaction metadata by block number. 

___


## treasury
 
### approvals(): `Vec<ProposalIndex>`
- **interface**: `api.query.treasury.approvals`
- **summary**:   Proposal indices that have been approved but not yet awarded. 
 
### proposalCount(): `ProposalIndex`
- **interface**: `api.query.treasury.proposalCount`
- **summary**:   Number of proposals that have been made. 
 
### proposals(`ProposalIndex`): `Option<TreasuryProposal>`
- **interface**: `api.query.treasury.proposals`
- **summary**:   Proposals that have been made. 

___


## uniques
 
### account(`AccountId, ClassId, InstanceId`): `Option<()>`
- **interface**: `api.query.uniques.account`
- **summary**:   The assets held by any given account; set out this way so that assets owned by a single account can be enumerated. 
 
### asset(`ClassId, InstanceId`): `Option<InstanceDetails>`
- **interface**: `api.query.uniques.asset`
- **summary**:   The assets in existence and their ownership details. 
 
### attribute(`ClassId, Option<InstanceId>, Bytes`): `Option<(Bytes,DepositBalanceOf)>`
- **interface**: `api.query.uniques.attribute`
- **summary**:   Metadata of an asset class. 
 
### class(`ClassId`): `Option<ClassDetails>`
- **interface**: `api.query.uniques.class`
- **summary**:   Details of an asset class. 
 
### classMetadataOf(`ClassId`): `Option<ClassMetadata>`
- **interface**: `api.query.uniques.classMetadataOf`
- **summary**:   Metadata of an asset class. 
 
### instanceMetadataOf(`ClassId, InstanceId`): `Option<InstanceMetadata>`
- **interface**: `api.query.uniques.instanceMetadataOf`
- **summary**:   Metadata of an asset instance. 

___


## vesting
 
### vesting(`AccountId`): `Option<VestingInfo>`
- **interface**: `api.query.vesting.vesting`
- **summary**:   Information regarding the vesting of a given account. 
