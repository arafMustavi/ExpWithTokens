# Project Inter-Stellar
Inter-Bank settlement system ideation and demo for the Banks in Bangladesh

Prototype Built using r3 Corda
---
To Deploy the Network:

```
gradlew.bat deployNodes
gradlew.bat clean deployNodes

```

To run the Network:

```
build\nodes\runnodes.bat
```

To check all the flows that started with the node, Just go to any of the four terminal and type:

```
flow list
```

## Transfer tokens from one account to other 

For someone who is looking into how to only transfer tokens from one account to other use below steps.


###  Step 1
```
flow start CreateAndShareAccountFlow accountName: branchA1, partyToShareAccountInfoToList: [CentralBank, BankA, BankB]
flow start CreateAndShareAccountFlow accountName: branchA2, partyToShareAccountInfoToList: [CentralBank, BankA]
flow start CreateAndShareAccountFlow accountName: branchA3, partyToShareAccountInfoToList: [CentralBank, BankA]
```
Run the above flow on the BankA node. This will create the branchA1, branchA2 and branchA3 accounts on the BankA node and share this account info with CentralBank and BankA node

Then let's go to the BankB node and create brunchB1 account: 
```
flow start CreateAndShareAccountFlow accountName: branchB1, partyToShareAccountInfoToList: [CentralBank, BankB, BankA]
flow start CreateAndShareAccountFlow accountName: branchB2, partyToShareAccountInfoToList: [CentralBank, BankB]
```

Run the below query to confirm if accounts are created on BankA node. Also run the above query on CentralBank and BankB node to confirm if account info is shared with these nodes.

    run vaultQuery contractStateType : com.r3.corda.lib.accounts.contracts.states.AccountInfo


###  Step 2

```
start IssueCashFlow accountName : brunchA1 , currency : USD , amount : 80

```
Run the above command on the Bank node, which will issue 80 USD to brunchA1 account.

###  Step 3
```
flow start QuerybyAccount whoAmI: branchA1
```
You can check balance of branchA1 account at BankA's node
[Option] You can also run the below command to confirm if 80 USD fungible tokens are stored at BankA's node. The current holder field in the output will be an AnonymousParty which specifies an account.
```
run vaultQuery contractStateType : com.r3.corda.lib.tokens.contracts.states.FungibleToken
```

###  Step 4
```
start MoveTokensBetweenAccounts senderAccountName : branchA1, rcvAccountName : branchB1 , currency : USD , amount : 10
```
This will move tokens from account branchA1 to account branchB1



###  Step 5
```
flow start QuerybyAccount whoAmI: branchA1
```
You can check balance of branchA1 account at BankA's node
```
run vaultQuery contractStateType : com.r3.corda.lib.tokens.contracts.states.FungibleToken
```

###  Step 6
```
flow start QuerybyAccount whoAmI: branchB1
```
You can check balance of branchB1 account at BankB's node
```
run vaultQuery contractStateType : com.r3.corda.lib.tokens.contracts.states.FungibleToken
```
## Further Reading

For accounts visit https://github.com/corda/accounts.

For tokens visit https://github.com/corda/token-sdk.










To issue a Token Flow:

```

start TokenIssueFlowInitiator owner: BankA, amount: 500 
start IssueStellarToken owner: BankA, amount: 500 

run vaultQuery contractStateType: InterStellar.TokenState

```


start TokenIssuanceFlow ownerAccount: AccountA1, amount: 500
start QueryByAccount name: AccountA1
start AllAccounts



To create an Account:

```

start CreateAccount name: AccountA1

run vaultQuery contractStateType: InterStellar.TokenState

start TokenIssuanceFlow ownerAccount: AccountA1, amount: 500

start QuerybyAccount name: AccountA1

start AllAccounts
```