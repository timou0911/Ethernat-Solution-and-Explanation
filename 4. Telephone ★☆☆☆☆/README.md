[Level 4. Telephone](https://ethernaut.openzeppelin.com/level/0x2C2307bb8824a0AbBf2CC7D76d8e63374D2f8446)

## Concepts

1. The meaning of `msg.sender` and `tx.origin`, also the difference between these two global variables.

## Level Target

1. Take ownership of the contract.

## Breakdown & Analysis

1. Let's begin by identifying the lines of code that pertain to assigning the value of `owner`.

    1. The assignment in the function `changeOwner`.
   
    2. There are no other lines allowing us to change the value of `owner`. (we can’t get access to the `constructor` since it’s not included in the contract bytecode)
    
    So the only way is to crack from the function `changeOwner`.
    
2. To successfully call `changeOwner`, we’ll have to make the value of `msg.sender` and the value of `tx.origin` different.

    1. `msg.sender` is the address that invokes the function, it can be an externally-owned account(EOA) or a contract account(CA).
   
    2. `tx.origin` is the original caller that starts the transaction, since smart contracts can’t be invoked automatically, there will be an EOA that initiates the transaction, so `tx.origin` can only be an EOA.
        
    Consider a simple example: Alice → contract A → contract B.
        
    The `msg.sender` of contract B is the address of contract A, yet, the `tx.origin` of contract B is Alice.
        
    And that is how we can make `msg.sender` and `tx.origin` different in this level.
        

## Detailed Steps

See [Attack.sol](https://github.com/timou0911/Ethernat-Solution-and-Explanation/blob/main/4.%20Telephone%20%E2%98%85%E2%98%86%E2%98%86%E2%98%86%E2%98%86/Attack.sol).

## Fhishing through `tx.origin`

