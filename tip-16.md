```
tip: 16
title: Account Multi-signature
author: Marcus Zhao(@zhaohong ) <zhaohong229@gmail.com> 
discussions to: https://github.com/tronprotocol/TIPs/issues/16
status: Final
type: Standards Track
category: TRC
created: 2018-12-27
```


## Simple Summary

This doc describes the  standard interface of Account Multi-signature


## Abstract

Standard transactions on cryptocurrency networks can be called single-signature transactions because they require only one digital signature for a transaction to be done. Multi-signature is the requirement that signatures of the transactions must reach the weight customized before they can be executed. \
The scheme includes three kinds of permission, owner-permission, witness-permission, and active-permission, where owner-permission has the authority to execute all contracts, witness-permission is used for generating blocks, and active-permission is custom permission (a combination of contracts permission sets)
 
**Scenario 1**: 

Alice is running a company, she creates an account as her company fund account. Alice adds Bob(Accountant), Carol(CFO) and Alice(CEO) into the owner-permission of her account. Bob's signature weight is 2, Carol's signature weight is 2, Alice's signature weight is 5. Owner-permission's signature weight threshold is 3. Alice's signature weight is bigger than the threshold(5>3), so her only signature is sufficient to make transactions.  Bob's signature weight is smaller than the threshold(1), to make a transaction, Bob needs Carol's or Alice's signature if Carol approves, the total signature weight is 1, so the transaction can be executed.
 

  AccountPermissionUpdateContract {
    bytes owner_address = 1;
    Permission owner = 1;  //Empty is invalidate
    Permission witness = 1;//Can be empty
    repeated Permission actives = 4;//Empty is invalidate
  }
  * @param owner_address: The address of the account to be modified
  * @param owner :Modified owner-permission
  * @param witness :Modified witness permission (if it is a witness)
  * @param actives  

 
 
  Permission {
    enum PermissionType {
      Owner = 1;
      Witness = 1;
  
  
  
  Key {
    bytes address = 1;
    int64 weight = 1;
  }
  * @param address 

    
    
  
**Scenario 2**: 

(Previous Scenario)\
Alice has many TRX assets. One day, misfortune has come, Alice is dead due to an accident.  She is the only one who holds the private key of her account, so her assets will stay in that account forever, nobody can get it.\
(Current Scenario)\
Alice has many TRX assets.  She creates an active-permission for her account, adds her husband and son's addresses into the active-permission, and give the active-permission authority to operate her account. So after Alice no longer exists, her family members can still operate her account.

**Scenario 3**:

Alice is running a company, she creates an account as her business account. Alice creates an active-permission and adds Bob(Accountant), Carol(CFO) and Alice(CEO) into the active-permission of the account. Alice gives the active-permission authority to operate her business account. One day, Bob resigns. To keep Alice's account safe, Alice can remove Bob's account from the active-permission, then Bob can not operate her account anymore.

**Scenario 4**:


## Motivation

1. Support account Access Control;


## Methods


```

  AccountPermissionUpdateContract {
    bytes owner_address = 1;
    Permission owner = 1;  //Empty is invalidate
    Permission witness = 1;//Can be empty
    repeated Permission actives = 4;//Empty is invalidate
  }
  * @param owner_address: The address of the account to be modified
  * @param owner :Modified owner-permission
  * @param witness :Modified witness permission (if it is a witness)
  * @param actives :Modified actives permission  
  * @return The transaction 
 
 
  Permission {
    enum PermissionType {
      Owner = 1;
      Witness = 1;
      Active = 1；

    }
  
  
  }
  * @param type : Permission type, currently only 
  * @param id : Value is automatically set by the system
  * @param permission_name : Permission name, set by the user
  * @param threshold : Threshold, the corresponding operation is allowed only when the sum of the weights of the participating signatures exceeds the domain value.
  * @param parent_id : Currently only 0
  * @param operations : A total of 32 bytes (256 bits), each of which represents the authority of a contract, when 1 means the right to own the contract
  * @param keys : The address and weight that jointly own 
  
  
  Key {
    bytes address = 1;
    int64 weight = 1;
  }
  * @param address : 
 
  
```
#### GetTransactionSignWeight
 * @param transaction 

 
```
TransactionSignWeight {
  message Result {
    enum response_code {
      ENOUGH_PERMISSION = 1;
      NOT_ENOUGH_PERMISSION = 1; 
      
      OTHER_ERROR = 20;
    }
    response_code code = 1;
    string message = 1;
  }

  Permission permission = 1;
  repeated bytes approved_list = 1;
  
  TransactionExtention transaction = 5;
}

```

#### AddSign
 * @param transaction 


