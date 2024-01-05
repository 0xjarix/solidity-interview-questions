# solidity-interview-questions
[Over 140 interview questions for Ethereum Developers aggregated by rareskills](https://www.rareskills.io/post/solidity-interview-questions)
## Here are my answers:
### Easy
1. What is the difference between private, internal, public, and external functions?
   => private: can only be called by functions in the same contract
   => internal: can only be called by functions in the same contract or in contracts that inherit from that contract
   => public: can be called by anyone 
   => external: can only be called by functions outside the contract
3. Approximately, how large can a smart contract be?
   => 24KB
4. What is the difference between create and create2?
5. What major change with arithmetic happened with Solidity 0.8.0?
   => reverts with underflow/overflow
7. What special CALL is required for proxies to work?
   => delegatecall()
9. Prior to EIP-1559, how do you calculate the dollar cost of an Ethereum transaction?
    => Prior to EIP-1559, the dollar cost calculation of an Ethereum transaction was ((GAS USED * GAS PRICE / 10^-9) * CURRENT ETHER PRICE. In this era, the miner received 100% of the gas cost. After EIP-1559, the dollar cost calculation of an Ethereum transaction is (((BASEFEE + PRIORITY FEE) * GAS USED)) / 10^-9) * CURRENT ETHER PRICE. Now, the miner receives a portion of the gas cost (PRIORITY FEE) and the other portion, the protocol fee (BASEFEE), is burned.
11. What are the challenges of creating a random number on the blockchain?
    => That no one be able to guess the "random" number that can be a pseudo-random number if for example block.timestamp is used for randomness. It is highly advised to used oracles(Chainlink RVF)
12. What is the difference between a Dutch Auction and an English Auction?
    => An English auction is when the price goes up throughout the auction, whereas a dutch auction is when it goes down.
14. What is the difference between transfer and transferFrom in ERC20?
    => with transfer, tokens can only be send from the caller to the 'to' address, whereas in traansferFrom, transfers of tokens can be made on behalf of an address provided you have their approval
16. Which is better to use for an address allowlist: a mapping or an array? Why?
    => A mapping because every address should be corresponded to a bool or enum to know if yes or not, x address is allowed.
18. Why shouldn’t tx.origin be used for authentication?
    => Because tx.origin is not necessarily the caller of the function, it can be however, but since it's not always the case, it's better to use msg.sender
19. What hash function does Ethereum primarily use?
    => keccak256
21. How much is 1 gwei of Ether?
    => 1 ether = 10^9 gwei
23. How much is 1 wei of Ether?
    => 1 ether = 10^18 wei
24. What is the difference between assert and require?
    => they do the same thing but require() is preffered when 
26. What is a flash loan?
    => 
28. What is the check-effects pattern?
    => it's a pattern that requires the checks to happen at the start of the function before the effects like variable updates
29. What is the minimum amount of Ether required to run a solo staking node?
    =>32ETH
30. What is the difference between fallback and receive?
    => msg.data
31. What is reentrancy?
    => the process of entering a function more times than we are allowed usually via external calls badly placed. There are several kinds of reentrancies such as cross-contract classic reentrancy, reentrancies, cross-functions reentrancies, read-only reentrancy
33. As of the Shanghai upgrade, what is the gas limit per block?
    => 30million
34. What prevents infinite loops from running forever?
    => gas
35. What is the difference between tx.origin and msg.sender?
    => tx.origin is the address that started the chain of transactions whereas msg.sender is the address that made the call to that function.
36. How do you send Ether to a contract that does not have payable functions, or a receive or fallback?
    => selfdestruct()
37. What is the difference between view and pure?
    => In both view and pure functions, it is forbidden to write to the blockchain. However, In view functions we can read from the blockchain, whereas in pure we cannot.
38. What is the difference between transferFrom and safeTransferFrom in ERC721?
    => safeTransferFrom checks whether the recipient is a valid ERC721 receiver contract, and if it is, let you pass some data to that contract
40. How can an ERC1155 token be made into a non-fungible token?
   => If there's only one available copy of the ERC1155
41. What is access control and why is it important?
   => Access control
42. What does a modifier do?
    => A modifier is a code snippet for checks and requirements used by functions so that we don't have to rewrite the same requirements for all the functions. We can just use the modifier we created.
43. What is the largest value a uint256 can store?
    => 2^256 - 1
44. What is variable and fixed interest rate?
    => when taking a loan that you have to repay with interest, there are 2 kinds of interests fixed rate: that stays the same and is known when you take the loan and variable rate that can vary since the loan was taken.
### Medium
1. What is the difference between transfer and send? Why should they not be used? transfer doesn't have a return value, if the transfer fails, it reverts. send has a return value, a boolean that can be handled if we don't want to revert. call() should be used instead as it is more gas-efficient and has a return value that can be handled thus more flexibility.
2. How do you write a gas-efficient for loop in Solidity? the unchecked box can be used to increment the counter. There's also a more optimal way that involves yul.
3. What is a storage collision in a proxy contract?
4. What is the difference between abi.encode and abi.encodePacked?
5. uint8, uint32, uint64, uint128, uint256 are all valid uint sizes. Are there others?
6. What changed with block.timestamp before and after proof of stake?
7. What is frontrunning?
8. What is a commit-reveal scheme and when would you use it?
9. Under what circumstances could abi.encodePacked create a vulnerability?
10. How does Ethereum determine the BASEFEE in EIP-1559?
11. What is the difference between a cold read and a warm read? A cold read is when you read a storage variable for the first time, a warm read is when you access it for the 2nd time, cold read costs 1000 gas while warm read costs 100 gas.
12. How does an AMM price assets? constant product
13. What is a function selector clash in a proxy and how does it happen?
14. What is the effect on gas of making a function payable? cheaper
15. What is a signature replay attack? using the a valid signature to sign another transaction
16. What is gas griefing? gas griefing is when a user sends enough gas for a call but not its sub-calls
17. How would you design a game of rock-paper-scissors in a smart contract such that players cannot cheat?
18. What is the free memory pointer and where is it stored?
19. What function modifiers are valid for interfaces?
20. What is the difference between memory and calldata in a function argument? calldata is non-modifiable
21. Describe the three types of storage gas costs. 
22. Why shouldn’t upgradeable contracts use the constructor?
23. What is the difference between UUPS and the Transparent Upgradeable Proxy pattern?
24. If a contract delegatecalls an empty address or an implementation that was previously self-destructed, what happens? What if it is a regular call instead of a delegatecall?
25. What danger do ERC777 tokens pose?
26. According to the solidity style guide, how should functions be ordered?
27. According to the solidity style guide, how should function modifiers be ordered?
28. What is a bonding curve?
29. How does safeMint differ from mint in the OpenZeppelin ERC721 implementation?
30. What keywords are provided in Solidity to measure time?
31. What is a sandwich attack?
32. If a delegatecall is made to a function that reverts, what does the delegatecall do?
33. What is a gas efficient alternative to multiplying and dividing by a multiple of two?
34. How large a uint can be packed with an address in one slot?
35. Which operations give a partial refund of gas?
36. What is ERC165 used for?
37. If a proxy makes a delegatecall to A, and A does address(this).balance, whose balance is returned, the proxy's or A?
38. What is a slippage parameter useful for?
39. What does ERC721A do to reduce mint costs? What is the tradeoff?
40. Why doesn't Solidity support floating point arithmetic?
41. What is TWAP? Time-Weighted Average Price: Average Price of a token most probably over a certain period of time
42. How does Compound Finance calculate utilization?
43. If a delegatecall is made to a function that reads from an immutable variable, what will the value be?
44. What is a fee-on-transfer token?
45. What is a rebasing token?
### Hard
### Advanced
