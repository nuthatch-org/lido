# lido

A [nuthatch](https://github.com/nightswatchhq/nuthatch) nest: **Lido stETH on Ethereum**.

Submissions, transfers, share transfers, rebases and oracle reports.

One binary, one config file, no graph-node, no gateway, no query fees.

## What it indexes

**Chain:** `mainnet`. **1 contract**, **32 tables**.

| alias | address |
|---|---|
| `steth` | `0xae7ab96520de3a18e5e111b5eaab095312d7fe84` |

## Verified

Indexed blocks **25,791,574 to 25,811,510** and sealed **26,280 events**. Every table below is generated from the vendored ABIs, and the run above is what this nest actually decoded, not an estimate.

## Read this before trusting it

- stETH sits behind an Aragon proxy whose EIP-1967 slot is **empty**. Resolving the address directly yields exactly one event, `ProxyDeposit`, and a nest that decodes nothing. The implementation comes from `implementation()`.
- That implementation is not on Sourcify; its ABI is vendored from Blockscout, which speaks the Etherscan-compatible API without a key.

## Run it

```sh
nuthatch init --from https://github.com/nightswatchhq/lido
cd lido
nuthatch dev --dir . --backfill 50000 --seal-direct
nuthatch sql --dir . "SELECT count(*) FROM \"steth__approval\""
```

The endpoint in `nuthatch.toml` is keyless and public, so this file is publishable: a `nuthatch.toml` is pinned into the nest's content address and must never carry a credential. It is enough to follow the tip. A **backfill** wants archive depth it may not have: pass your own with `--rpc`, and check it first with `nuthatch doctor --rpc <url>`.

## Tables

```
steth__approval
steth__c_l_balances_updated
steth__contract_version_set
steth__deposited_post_report_updated
steth__deposited_validators_changed
steth__deposits_reserve_set
steth__deposits_reserve_target_set
steth__e_i_p712_st_e_t_h_initialized
steth__e_l_rewards_received
steth__e_t_h_distributed
steth__external_bad_debt_internalized
steth__external_ether_transferred_to_buffer
steth__external_shares_burnt
steth__external_shares_minted
steth__internal_share_rate_updated
steth__lido_locator_set
steth__max_external_ratio_b_p_set
steth__recover_to_vault
steth__resumed
steth__script_result
steth__shares_burnt
steth__staking_limit_removed
steth__staking_limit_set
steth__staking_paused
steth__staking_resumed
steth__stopped
steth__submitted
steth__token_rebased
steth__transfer
steth__transfer_shares
steth__unbuffered
steth__withdrawals_received
```
