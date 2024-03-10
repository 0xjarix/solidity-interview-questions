# solidity-interview-questions
[Over 140 interview questions for Ethereum Developers aggregated by rareskills](https://www.rareskills.io/post/solidity-interview-questions)
## Here are my answers:
### Easy
1. What is the difference between private, internal, public, and external functions?  
   => private: can only be called by functions in the same contract.  
   => internal: can only be called by functions in the same contract or in contracts that inherit from that contract.   
   => public: can be called by anyone.  
   => external: can only be called by functions outside the contract.
2. Approximately, how large can a smart contract be?  
   => 24KB.
3. What is the difference between create and create2?
   => CREATE
4. What major change with arithmetic happened with Solidity 0.8.0?  
   => reverts with underflow/overflow  .
5. What special CALL is required for proxies to work?  
   => delegatecall().
6. Prior to EIP-1559, how do you calculate the dollar cost of an Ethereum transaction?  
    => Prior to EIP-1559, the dollar cost calculation of an Ethereum transaction was ((GAS USED * GAS PRICE / 10^-9) * CURRENT ETHER PRICE. In this era, the miner received 100% of the gas cost. After EIP-1559, the dollar cost calculation of an Ethereum transaction is (((BASEFEE + PRIORITY FEE) * GAS USED)) / 10^-9) * CURRENT ETHER PRICE. Now, the miner receives a portion of the gas cost (PRIORITY FEE) and the other portion, the protocol fee (BASEFEE), is burned.  
7. What are the challenges of creating a random number on the blockchain?  
    => That no one be able to guess the "random" number that can be a pseudo-random number if for example block.timestamp is used for randomness. It is highly advised to used oracles(Chainlink VRF).
8. What is the difference between a Dutch Auction and an English Auction?  
    => An English auction is when the price goes up throughout the auction, whereas a dutch auction is when it goes down.
9. What is the difference between transfer and transferFrom in ERC20?  
    => with transfer, tokens can only be send from the caller to the 'to' address, whereas in traansferFrom, transfers of tokens can be made on behalf of an address provided you have their approval.
10. Which is better to use for an address allowlist: a mapping or an array? Why?  
    => A mapping because every address should be corresponded to a bool or enum to know if yes or not, x address is allowed.  
11. Why shouldn’t tx.origin be used for authentication?  
    => Because tx.origin is not necessarily the caller of the function, it can be however, but since it's not always the case, it's better to use msg.sender.
12. What hash function does Ethereum primarily use?  
    => keccak256.
13. How much is 1 gwei of Ether?  
    => 1 ether = 10^9 gwei
14. How much is 1 wei of Ether?  
    => 1 ether = 10^18 wei
15. What is the difference between assert and require?  
    => they do the same check statements truthfulness and revert if they statements are false.
    => require() is preffered when we're checking functions' parameters or messages' global variables, external calls, return statements.
    => assert() is preffered when we want to handle internal errors, check that the state is as we expect it at the end of the function's instructions.
16. What is a flash loan?  
    => It is a type of uncollateralized loan that lets a user borrow assets with no upfront collateral as long as the borrowed assets are paid back within the same blockchain transaction.
17. What is the check-effects pattern?  
    => it's a pattern that requires the checks to happen at the start of the function before the effects like variable updates
18. What is the minimum amount of Ether required to run a solo staking node?  
    => 32ETH  
19. What is the difference between fallback and receive?  
    => msg.data
20. What is reentrancy?  
    => the process of entering a function more times than we are allowed usually via external calls badly placed. There are several kinds of reentrancies such as classic canonical reentrancy, cross-functions reentrancies, cross-contract reentrancy, read-only reentrancy
21. As of the Shanghai upgrade, what is the gas limit per block?  
    => 30million
22. What prevents infinite loops from running forever?  
    => gas
23. What is the difference between tx.origin and msg.sender?  
    => tx.origin is the address that started the chain of transactions whereas msg.sender is the address that made the call to that function.
24. How do you send Ether to a contract that does not have payable functions, or a receive or fallback?  
    => selfdestruct()
25. What is the difference between view and pure?  
    => In both view and pure functions, it is forbidden to write to the blockchain. However, In view functions we can read from the blockchain, whereas in pure we cannot.
26. What is the difference between transferFrom and safeTransferFrom in ERC721?  
    => safeTransferFrom checks whether the recipient is a valid ERC721 receiver contract, and if it is, lets you pass some data to that contract
27. How can an ERC1155 token be made into a non-fungible token?  
   => If there's only one available copy of the ERC1155, token id has a maximum supply of 1
28. What is access control and why is it important?  
   => Access control—that is, "who is allowed to do this thing"—is incredibly important in the world of smart contracts. The access control of your contract may govern who can mint tokens, vote on proposals, freeze transfers, and many other things. Bad access control can represent a critical vulnerability since it would grant some users rights to perform actions they shouldn't be able to perform
29. What does a modifier do?  
    => A modifier is a code snippet for checks and requirements used by functions so that we don't have to rewrite the same requirements for all the functions that need these checks. We can just use the modifier we created.
30. What is the largest value a uint256 can store?  
    => 2^256 - 1
31. What is variable and fixed interest rate?  
    => when taking a loan that you have to repay with interest, there are 2 kinds of interests fixed rate: that stays the same and is known when you take the loan and variable rate that can vary since the loan was taken.
### Medium
1. What is the difference between transfer and send? Why should they not be used?  
   => transfer() doesn't have a return value, if the transfer fails, it reverts, whatever the transaction may be, the gas limit is 2300, the receiving smart contract should have a fallback function defined or else the transfer call will throw an error.  
   => send() has a return value, a boolean that can be handled if we don't want to revert, the gas limit is 2300 as well, the receiving smart contract should have a fallback function defined or else the send call will return false.  
   => call() is the recommended way of sending ETH to a smart contract. The empty argument triggers the fallback function of the receiving address. using call, one can also trigger other functions defined in the contract and send a fixed amount of gas to execute the function. The transaction status is sent as a boolean and the return value is sent in the data variable.  
3. How do you write a gas-efficient for loop in Solidity? the unchecked box can be used to increment the counter. There's also a more optimal way that involves yul.
4. What is a storage collision in a proxy contract?
5. What is the difference between abi.encode and abi.encodePacked?
6. uint8, uint32, uint64, uint128, uint256 are all valid uint sizes. Are there others?
7. What changed with block.timestamp before and after proof of stake?
8. What is frontrunning?
9. What is a commit-reveal scheme and when would you use it?
10. Under what circumstances could abi.encodePacked create a vulnerability?
11. How does Ethereum determine the BASEFEE in EIP-1559?
12. What is the difference between a cold read and a warm read? A cold read is when you read a storage variable for the first time, a warm read is when you access it for the 2nd time, cold read costs 1000 gas while warm read costs 100 gas.
13. How does an AMM price assets? constant product
14. What is a function selector clash in a proxy and how does it happen?
15. What is the effect on gas of making a function payable? cheaper
16. What is a signature replay attack? using the a valid signature to sign another transaction
17. What is gas griefing? gas griefing is when a user sends enough gas for a call but not its sub-calls
18. How would you design a game of rock-paper-scissors in a smart contract such that players cannot cheat?
19. What is the free memory pointer and where is it stored?
20. What function modifiers are valid for interfaces?
21. What is the difference between memory and calldata in a function argument? calldata is non-modifiable
22. Describe the three types of storage gas costs. 
23. Why shouldn’t upgradeable contracts use the constructor?
24. What is the difference between UUPS and the Transparent Upgradeable Proxy pattern?
25. If a contract delegatecalls an empty address or an implementation that was previously self-destructed, what happens? What if it is a regular call instead of a delegatecall?
26. What danger do ERC777 tokens pose?
27. According to the solidity style guide, how should functions be ordered?
28. According to the solidity style guide, how should function modifiers be ordered?
29. What is a bonding curve?
30. How does safeMint differ from mint in the OpenZeppelin ERC721 implementation?
31. What keywords are provided in Solidity to measure time?
32. What is a sandwich attack?
33. If a delegatecall is made to a function that reverts, what does the delegatecall do?
34. What is a gas efficient alternative to multiplying and dividing by a multiple of two?
35. How large a uint can be packed with an address in one slot?
36. Which operations give a partial refund of gas?
37. What is ERC165 used for?
38. If a proxy makes a delegatecall to A, and A does address(this).balance, whose balance is returned, the proxy's or A?
39. What is a slippage parameter useful for?
40. What does ERC721A do to reduce mint costs? What is the tradeoff?
41. Why doesn't Solidity support floating point arithmetic?
42. What is TWAP? Time-Weighted Average Price: Average Price of a token most probably over a certain period of time
43. How does Compound Finance calculate utilization?
44. If a delegatecall is made to a function that reads from an immutable variable, what will the value be?
45. What is a fee-on-transfer token?
46. What is a rebasing token?
### Hard
### Advanced
