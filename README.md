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

`flow list`

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