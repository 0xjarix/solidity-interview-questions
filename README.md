# solidity-interview-questions
[Over 140 interview questions for Ethereum Developers aggregated by rareskills](https://www.rareskills.io/post/solidity-interview-questions)
## Here are my answers:
### Easy
1. What is the difference between private, internal, public, and external functions?
   =>
3. Approximately, how large can a smart contract be?
   => 24KB
4. What is the difference between create and create2?
5. What major change with arithmetic happened with Solidity 0.8.0?
   => reverts with underflow/overflow
7. What special CALL is required for proxies to work?
   => delegatecall()
9. Prior to EIP-1559, how do you calculate the dollar cost of an Ethereum transaction?
10. What are the challenges of creating a random number on the blockchain?
    => That no one be able to guess the "random" number that can be a pseudo-random number if for example block.timestamp is used for randomness. It is highly advised to used oracles(Chainlink RVF)
12. What is the difference between a Dutch Auction and an English Auction?
    =>
14. What is the difference between transfer and transferFrom in ERC20?
    =>
16. Which is better to use for an address allowlist: a mapping or an array? Why?
17. Why shouldn’t tx.origin be used for authentication?
    => Because 
19. What hash function does Ethereum primarily use?
    => keccak256
21. How much is 1 gwei of Ether?
    => 1 ether = 10^9 gwei
23. How much is 1 wei of Ether?
    => 1 ether = 10^18 wei
24. What is the difference between assert and require?
    => they do the same thing but require() is preffered when 
26. What is a flash loan?
27. What is the check-effects pattern?
    => it's a pattern that requires the checks to happen at the start of the function before the effects like variable updates
28. What is the minimum amount of Ether required to run a solo staking node?
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
39. How can an ERC1155 token be made into a non-fungible token?
   => If there's only one available copy of the ERC1155
40. What is access control and why is it important?
   => Access control
41. What does a modifier do?
    => A modifier is a code snippet for checks and requirements used by functions so that we don't have to rewrite the same requirements for all the functions. We can just use the modifier we created.
42. What is the largest value a uint256 can store?
    => 2^256 - 1
43. What is variable and fixed interest rate?
    => when taking a loan that you have to repay with interest, there are 2 kinds of interests fixed rate: that stays the same and is known when you take the loan and variable rate that can vary since the loan was taken.
### Medium
### Hard
### Advanced
