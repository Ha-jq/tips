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
 


(Previous Scenario)\
Alice has a witness account, if she wants to deploy a node but doesn't know how to deploy, she needs to provide the account's private key to the program administrator.\
(Current Scenario) \
Alice can assign witness-permission to the administrator. Since the administrator only has the producing-block permission, there is no TRX transfer permission, and even if the private key of the administrator on the server is compromised, TRX will not be lost.


  * @return The transaction 
 
 
  Permission {
    enum PermissionType {
      Owner = 1;
      Witness = 1;
      Active = 1;

  }
  * @param type : Permission type, currently only supports three kind of permissions
  * @param id : Value is automatically set by the system
  * @param permission_name : Permission name, set by the user
  * @param threshold : Threshold, the corresponding operation is allowed only when the sum of the weights of the participating signatures exceeds the domain value.
  * @param parent_id : Currently only 0

  
  
  Key {
    bytes address = 1;
   
  }
  * @param address 

  
```
#### GetTransactionSignWeight
 * @param transaction 
 * @return The transaction sign weight
 
```
TransactionSignWeight {
  message Result {
    enum response_code {
      ENOUGH_PERMISSION = 1;
      NOT_ENOUGH_PERMISSION = 1; 
   
      OTHER_ERROR = 20;
    }
    response_code code = 1;
    string message = 1；
  }

 
```

#### AddSign
 * @param transaction 


