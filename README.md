# investigation-of-Previous-ReferenceState

## Introduction
This program is builded for the following requests.

  ・Whether Previous Reference State can include in the transaction or not.
  
In order to investigate these matter, I added sort of process to https://github.com/sbir3japan/corda-dev-traning-sbir3japan.git.

## Note 
**This program focused only on IOU Issue and added the process of adding Previous Reference State.**

**Reference State are not included in Transfer and Settle Flow.**

**※To come to the point, this code will be error because previous Reference state cannnot includ in transaction.**

## Newly added files
### Put under "contracts\src\main\java\net\corda\training\states"
  AddressState.java: State corresponding to Ref.State.
  
### Put under "contracts\src\main\java\net\corda\training\contracts"
  AddressContract.java: Defined the Publish command that issues AddressState and the Move command that updates AddressState, and added restrictions on them.
    
### Put under "workflows\src\main\java\net\corda\training\flow"
  PublishFlow.java: Flow for publishing AddressState.
    
  MoveFlow.java: Flow for updating AddressState.
    
  
## Changes to existing files
### Put under "contracts\src\main\java\net\corda\training\contracts"
  IOUContract.java: Added process to include AddressState.
    
### Put under "workflows\src\main\java\net\corda\training\flow"
  IOUIssueFlow.java: Added constraints regarding AddressState.

## Procedure
  1. Run the nodes. By using following command, you will find AddressState hash.
        run vaultQuery contractStateType: net.corda.training.states.AddressState
        
  2. Run PublishFlow.java.By using following command, you will find AddressState hash.
        run vaultQuery contractStateType: net.corda.training.states.AddressState
        
  3. Run MoveFlow.java      ※You should confirm Transaction Hash.

  4. Run IOUIssueFlow.java  ※This process will not successful

  5. See the node log file and you will find the following error message.
        One or more input states or referenced states have already been used as input states in other transactions.
