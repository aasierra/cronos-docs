---
meta:
  - name: "title"
    content: Cronos | Crypto.org EVM Chain | Genesis
  - name: "description"
    content: The genesis.json file defines the initial state of the Crypto.org Chain. Find out more about genesis file in this documentation.
  - name: "og:title"
    content: Cronos | Crypto.org EVM Chain | Genesis
  - name: "og:type"
    content: Website
  - name: "og:description"
    content: The genesis.json file defines the initial state of the Crypto.org Chain. Find out more about genesis file in this documentation.
  - name: "og:image"
    content: https://cronos.crypto.org/og-image.png
  - name: "twitter:title"
    content: Cronos | Crypto.org EVM Chain | Genesis
  - name: "twitter:site"
    content: "@cryptocom"
  - name: "twitter:card"
    content: summary_large_image
  - name: "twitter:description"
    content: The genesis.json file defines the initial state of the Crypto.org Chain. Find out more about genesis file in this documentation.
  - name: "twitter:image"
    content: https://cronos.crypto.org/og-image.png
canonicalUrl: https://cronos.crypto.org/docs/chain-details/genesis_file.html
---

# Genesis

The `genesis.json` file defines the initial state of the Crypto.org Chain. On top of the standard [tendermint genesis](https://docs.tendermint.com/master/tendermint-core/using-tendermint.html#genesis) format, we customize our own genesis file that includes different [modules](#module_overview) and facilitates the special features of the Crypto.org Chain. Sample genesis file can be found [here](https://github.com/crypto-com/testnets/blob/main/testnet-cronos-2/genesis.json).

## Fields in genesis

Specifically, the genesis file includes the following fields:

- `"genesis_time"`:
  The time of the beginning of the blockchain.
- `"genutil"`: A variety of genesis utility functionality for usage including genesis transactions creation (gentx) and genesis file validation command as well as Tendermint related initialization.
- `"ibc"`: Inter-Blockchain Communication across different chains.
- `"chain_id"`:
  A unique identifier for the blockchain. See [this](./chain-id.md) for further details.
- `"initial_height"`: The initial height of the blockchain.
- `"consensus_params`: Consensus parameters defined in the genesis file.
  - `"block"`:
    - `"max_bytes"`: Maximum size of a block (in bytes).
    - `"max_gas"`: The gas limit per block, default value is "-1", i.e., no rules about gas are enforced.
    - `"time_iota_ms"`: The minimum time increment between consecutive blocks, in milliseconds.
  - `"evidence"`: Evidence storage handling and block proposal detection with the evidence reactor.
    - `"max_age_num_blocks"`: _This field is to be deprecated._
    - `"max_age_duration"`: The maximum age of evidence. Any evidence older than this will be rejected.
    - `"max_num"`: The maximum age of evidence (in number of blocks).
  - `"validator"`:
    - `"pub_key_types"`: The supported validator public key types.
- `"app_hash"`: The initial application state defined in the genesis block.
- `"auth"`
  - `"params"`: Parameters of the auth module defined in the genesis file.
    - `"max_memo_characters"`: Maximum number of characters in a memo of a transaction.
    - `"tx_sig_limit"`: The maximum number of signers for a transaction.
    - `"tx_size_cost_per_byte"`: The amount of gas consumed per byte of a transaction.
    - `"sig_verify_cost_ed25519"`: Gas cost on `edd2519` signature verification.
    - `"sig_verify_cost_secp256k1"`: Gas cost on `secp256k1` signature verification.
  - `"accounts"`: Genesis accounts, which defines the initial allocation of the tokens.
    - `"@type"`: Account type.
    - `"address"`: Address of the genesis accounts.
    - `"pub_key"`: Public key of the genesis accounts.
    - `"account_number"`: The account number of the account in state.
    - `"sequence"`: Used to count the number of transactions sent by this account. It is incremented each time a transaction is included in a block, and used to prevent replay attacks.
    - `"base_vesting_account"`:
      - `"original_vesting"`: Special type of accounting that the token needs to be vested for a period of time before they can be transferred. Tokens can be delegated during the vesting period.
        - `"denom"`: Denomination of the token.
        - `"amount"`: Total amount in the vesting account.
        - `"delegated_free"`: Amount of delegated tokens that can be transferred after they've been vested.
        - `"delegated_vesting"`: Amount of delegated tokens that are still under vesting.
        - `"endtime"`: Vesting end time.
- `"bank"` The bank module handles tokens.
  - `"params"`: Parameters of the bank module defined in the genesis file.
    - `"send_enabled"`: The transfer capability in the genesis.
    - `"default_send_enabled"`: The default value for "send_enabled" value controls send transfer capability.
- `"distribution"`:The module that handles the logic of distribution block provisions and fees to validators and delegators.
  - `"delegator_starting_infos"`:
  - `"delegator_withdraw_infos"`: List of delegators withdraw address.
  - `"fee_pool"`:
    - `"community_pool"`: Allocated funds in the community pool, if any.
  - `"outstanding_rewards"`: Uncollected rewards, if any.
  - `"params"`: Parameters of the distribution module defined in the genesis file.
    - `"base_proposer_reward"`: Base bonus on transaction fees collected in a valid block.
    - `"bonus_proposer_reward"`: Maximum bonus on transaction fees collected in a valid block.
    - `"community_tax"`: The rate of community tax.
    - `"withdraw_addr_enabled"`: Whether delegators can set a different address to withdraw their rewards.
  - `"previous_proposer"`: Proposer of the previous block, if any.
  - `"validator_accumulated_commissions"`: Uncollected commission of validators, if any.
  - `"validator_current_rewards"`: Information related to the current rewards of validators, if any.
  - `"validator_historical_rewards"`: Information related to the historical rewards of validators, if any.
  - `"validator_slash_events"`: Information related to the historical slashing events of validators, if any.
- `"gov"`: The governance module.
  - `"deposit_params"`: Parameters for the deposit required for governance proposal.
    - `"max_deposit_period"`: The maximum deposit period for governance proposal.
    - `"min_deposit"`: The minimum deposit required for governance proposal.
  - `"deposits"`: List of deposits for each proposal ID, if any.
  - `"proposals"`: List of proposals for proposals, if any.
  - `"starting_proposal_id"`: The initial proposals id, starting from `"1"`
  - `"tally_params"`: Parameters for tally.
    - `"quorum"`: Minimum percentage of bonded staking tokens that needs to vote for the result to be valid.
    - `"threshold"`: Minimum percentage of votes that need to be `YES` for the result to be valid.
    - `"veto_threshold"`: Maximum percentage `NO_WITH_VETO` votes for the result to be valid.
  - `"votes"`: List of votes for each proposal ID, if any.
  - `"voting_params"`: Parameters for voting.
    - `"voting_period"`: The voting period for governance proposal.
- `"mint"`: The minting module for token minting.
  - `"minter"`:
    - `"annual_provisions"`: Annual expected provisions (set to zero in genesis).
    - `"inflation"`: The target yearly inflation rate, compounded weekly.
  - `"params":` Parameters of the mint module defined in the genesis file.
    - `"blocks_per_year"`: The expected number of blocks being produced per year.
    - `"goal_bonded"`: Target bonded token in percentage.
    - `"inflation_max"`: Maximum inflation rate.
    - `"inflation_min"`: Minimum inflation rate.
    - `"inflation_rate_change"`: Maximum annual change in inflation rate.
    - `"mint_denom"`: Token type being minted.
- `"slashing"`: The slashing module for the punishment of validator's misbehavior.
  - `"missed_blocks"`: Information related to validators missed blocks, if any.
  - `"params"`: Parameters of the slashing module defined in the genesis file.
    - `"downtime_jail_duration"`: The jailing duration for validators with low availability.
    - `"min_signed_per_window"`: Threshold of total missed blocks, in percentage.
    - `"signed_blocks_window"`: Window to calculate validators's liveness.
    - `"slash_fraction_double_sign"`: Maximum percentage of stake reduction for byzantine validators.
    - `"slash_fraction_downtime"`: Maximum percentage of stake reduction for validators with low availability.
  - `"signing_infos"`: Information related to each validator for the slashing module, if any.
- `"staking"`: The staking module that handles Proof-of-Stake related logics.
  - `"delegations"`: Information related to the delegation state of validators, if any.
  - `"exported"`: Whether this genesis file was generated by exporting of a previous state.
  - `"last_total_power"`: Total voting power in the genesis, if any.
  - `"last_validator_powers"`: The voting power of each validator in last known state, if any.
  - `"params"`: Parameters of the staking module defined in the genesis file.
    - `"bond_denom"`: Coin denomination for staking.
    - `"historical_entries"`: The number of historical entries to persist.
    - `"max_entries"`: The max entries for either unbonding delegation or redelegation.
    - `"max_validators"`: The maximum number of validator.
    - `"unbonding_time"`: The time duration of unbonding.
  - `"redelegations"`: List of redelegations for validators, if any.
  - `"unbonding_delegations"`: List of unbonding delegations for validators, if any.
  - `"validators"`: List of existing validators, if any.
- `"transfer"`: The transfer module that handles token transfer transactions.
  - `"receive_enabled"`: An array of Receive enabled entries mapping coin denominations to their `receive_enabled` status.
  - `"send_enabled"`: An array of SendEnabled entries mapping coin denominations to their `send_enabled` status.
- `"evm"`: Ethereum Virtual Machine
  - `"evm_denom"`: The token denomination used on the EVM state transitions and gas consumption for EVM messages.
  - `"enable_create"`: Toggles state transitions that use the `vm.Create` function, and it prevents all contract creation functionality if it is disabled.
  - `"enable_call"`: Toggles state transitions that use the `vm.Call` function, and it prevents transfers between accounts and executing a smart contract call if it is disabled.
  - `"extra_eips"`: The set of activateable Ethereum Improvement Proposals (EIPs) on the Ethereum VM Config that apply custom jump tables. 
 
