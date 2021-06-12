# masterchef

## Goals:
- Create a generic featureful masterchef contract
## Problem:
- Please see ERC4000 for a detailed explanation 
- https://ethereum-magicians.org/t/erc-4000-staking-reward-pool-standard-request-for-comments/6004
## Spec
- Generic i.e. no specific token mentioned 
- Each pool should support the following properties with a check that the value is >= 0 && <= someMaxValue. The maxValue is to protect the user from unscrupulous admins changing the deposit fee to 100% or the time lockup to infinity. 
    - DepositFeeBP (deposit fee percent in basis points)
    - LockTime (require the user to wait X seconds before they can withdraw rewards to reduce sell pressure and add another layer of advantage for being in a native token pool. See polyzap for example https://farm.polyzap.finance/pools ) 
- Match the ERC4000 spec if possible
- Create and allow the use of a compatibility layer that maps the ERC4000 API provided by this masterchef to conform to the stakingRewards API of SNX/UNI. This allows it to be quickly adapter to work with sites using the old staking rewards style contracts. Example old style staking rewards from TORN: https://etherscan.io/address/0x720ffb58b4965d2c0bd2b827fa8316c2002a98aa#code 
- Allow having more than 1 token as rewards in cases of DAO partnerships and dual rewards. e.g.
    -  sushi MCV2 https://github.com/sushiswap/sushiswap/blob/master/contracts/MasterChefV2.sol
    - Ruler 
- Create a deployer factory that deploys generic masterchef contracts conforming to this standard. This allows nascent projects to more easily create new masterchef contracts and gives users some semblance of security knowing custom changes weren't made. This bridges the problematic gap left by audits taking way too long to complete and large numbers of protocols rushing to launch
- Use a consolidated fund model which allows a single fund holding contract address to supply many masterchef contracts and pools and giving admins the ability to shift rewards and remove the chance of sending funds to misconfigured contracts and loosing them. E.g.
    - Sharedstake.org https://github.com/SharedStake/Contracts/pull/22/files | Saddle pool
    - iron finance https://explorer-mainnet.maticvigil.com/address/0x65430393358e55A658BcdE6FF69AB28cF1CbB77a/transactions
    - Consolidated fund should support the ability to disable admin withdrawal of funds to petrify a working rewards system in place
