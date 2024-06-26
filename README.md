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
   => The main difference lies in how they calculate the new contract address.  
   => CREATE uses the sender's address and the nonce. It's possible to predict the address but it becomes less predictable when the nonce changes between the address calculations and the contract creaction.  
   => CREATE2 uses the sender's address and a salt value provided by the sender and the contract's init code. It offers more flexibility in choosing the contract's address by adjusting the salt value or the contract bytecode.  
   => CREATE2 is the better option for deployments.
4. What major change with arithmetic happened with Solidity 0.8.0?  
   => reverts with underflow/overflow.
5. What special CALL is required for proxies to work?  
   => delegatecall().
6. Prior to EIP-1559, how do you calculate the dollar cost of an Ethereum transaction?  
    => Prior to EIP-1559, the dollar cost calculation of an Ethereum transaction was ((GAS USED * GAS PRICE / 10^-9) * CURRENT ETHER PRICE. In this era, the miner received 100% of the gas cost. After EIP-1559, the dollar cost calculation of an Ethereum transaction is (((BASEFEE + PRIORITY FEE) * GAS USED)) / 10^-9) * CURRENT ETHER PRICE. Now, the miner receives a portion of the gas cost (PRIORITY FEE) and the other portion, the protocol fee (BASEFEE), is burned.  
7. What are the challenges of creating a random number on the blockchain?  
    => Ethereum proceeds deterministically (same output for the same input) and blockchain data is public so hackers can predict that "random" number if it is built using blockchain data such as block.timestamp, block.number or block.difficulty. It is highly advised to use oracles(Chainlink).
8. What is the difference between a Dutch Auction and an English Auction?  
    => An English auction is when the price goes up throughout the auction, whereas a dutch auction is when it goes down.
9. What is the difference between transfer and transferFrom in ERC20?  
    => with transfer, tokens can only be send from the caller to the 'to' address, whereas in traansferFrom, transfers of tokens can be made on behalf of an address provided you have their approval.
10. Which is better to use for an address allowlist: a mapping or an array? Why?  
    => A mapping because every address should be corresponded to a bool or enum to know if yes or not, x address is allowed. Mappings are more gas-efficient as we don't have to loop through all the addresses like we would do in an array.
11. Why shouldn’t tx.origin be used for authentication?  
    => Because tx.origin is not necessarily the caller of the function, it can be, however; since it's not always the case, it's better to use msg.sender.
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
    => when taking a loan that you have to repay with interest, there are 2 kinds of interests:  
       - fixed rate that stays the same and is known when you take the loan  
       - variable rate that can vary since the loan was taken.
### Medium
1. What is the difference between transfer and send? Why should they not be used?  
   => transfer() doesn't have a return value, if the transfer fails, it reverts, whatever the transaction may be, the gas limit is 2300, the receiving smart contract should have a fallback function defined or else the transfer call will throw an error.  
   => send() has a return value, a boolean that can be handled if we don't want to revert, the gas limit is 2300 as well, the receiving smart contract should have a fallback function defined or else the send call will return false.  
   => call() is the recommended way of sending ETH to a smart contract. The empty argument triggers the fallback function of the receiving address. using call, one can also trigger other functions defined in the contract and send a fixed amount of gas to execute the function. The transaction status is sent as a boolean and the return value is sent in the data variable.  
3. How do you write a gas-efficient for loop in Solidity?  
   => the unchecked box can be used to increment the counter. There's also a more optimal way that involves yul.
5. What is a storage collision in a proxy contract?  
   => When a delegate call is used, the called contract has access to the calling contract's storage. Therefore, if the layout of the storage variables in the delegate contract doesn't match the layout in the proxy contract, a storage collision occurs.
7. What is the difference between abi.encode and abi.encodePacked?  
   => abi.encode: padded encoding, takes up the whole slot  
   => abi.encodePacked: unpadded encoding, takes up the required space. Used to concate variables of different types like when we want to create IPFS CID hash concatenated with the correct url
8. uint8, uint32, uint64, uint128, uint256 are all valid uint sizes. Are there others?  
   => Yes, alluint8 to uint256 in steps of 8 (unsigned of 8 up to 256 bits). For example, there is also uint16, uint24, uint40, uint160(for addresses)
10. What changed with block.timestamp before and after proof of stake?  
   => Under proof of work, the Ethereum block interval varied, but miners could modify the block timestamp by +/-15 seconds, as long as the modified value was greater than the parent timestamp, without the block getting rejected.  
   => Under proof of stake, the Ethereum block interval is fixed at 12 seconds (or possibly a multiple of 12 seconds, in rare cases).
11. What is frontrunning?  
    => when a broker or an investor joins a trade because they have foreknowledge of a large confidential deal which will impact the asset's price. In the world of Decentralized Finance, large confidential deal are large pending transactions, in the mempool, that can be frontrunned by MEV-Searchers with their MEV-Bot.
13. What is a commit-reveal scheme and when would you use it?  
    => The Commit-Reveal scheme finds a fun application in-game scenarios such as a digital version of Rock, Paper, and Scissors. Players commit their choices without revealing them, ensuring a fair game. Once both players have committed, the reveal phase follows, determining the winner based on the choices made.
15. Under what circumstances could abi.encodePacked create a vulnerability?  
    => encodePacked can result in hash collisions when used with two dynamic arguments (string/bytes)
17. How does Ethereum determine the BASEFEE in EIP-1559?  
    => The base fee is calculated by a formula that compares the size of the previous block (the amount of gas used for all the transactions) with the target size. The base fee will increase by a maximum of 12.5% per block if the target block size is exceeded.
19. What is the difference between a cold read and a warm read?
    => A cold read is when you read a storage variable for the first time, a warm read is when you access it for the 2nd time, cold read costs 1000 gas while warm read costs 100 gas.
21. How does an AMM price assets?  
    => constant product: the product of the reserves is a constant x*y = k
22. What is a function selector clash in a proxy and how does it happen?  
    =>  In the case of a proxy, and plus particularly of a transparent proxy, a same function with the same arguments can be defined in the proxy and its implementation resulting in a function clash.
24. What is the effect on gas of making a function payable?  
    => cheaper as there is no checks for the ether sent `require(msg.value == 0)`
25. What is a signature replay attack?  
    => using the same signature to sign the same transaction multiple times
26. What is gas griefing?   
    => gas griefing is when a user sends enough gas for a call but not its sub-calls.
27. How would you design a game of rock-paper-scissors in a smart contract such that players cannot cheat?  
    => We use the commit-reveal scheme [already explained above].
29. What is the free memory pointer and where is it stored?  
    => it is stored in sequence 0x40-0x60
30. What function modifiers are valid for interfaces?  
    => pure, view, external, override, payable
32. What is the difference between memory and calldata in a function argument?  
    => calldata is non-modifiable
33. Describe the three types of storage gas costs.  
    =>  The basic costs associated with storage operations include 20,000 gas for storing a new variable, 5,000 gas for rewriting an existing variable, and a relatively nominal 200 gas for reading from a storage slot
34. Why shouldn’t upgradeable contracts use the constructor?  
    => Since, they are upgradeable, we will not want to have immutable variables, hence, we don't use constructor, but initialize() instead.
35. What is the difference between UUPS and the Transparent Upgradeable Proxy pattern?  
    => in UUPS proxies the upgrade is handled by the implementation, and can eventually be removed. Transparent proxies, on the other hand, include the upgrade and admin logic in the proxy itself.
37. If a contract delegatecalls an empty address or an implementation that was previously self-destructed, what happens? What if it is a regular call instead of a delegatecall?  
    => If a contract delegatecalls to a self-destructed implementation, the delegatecall will return a success. Same thing for `call`, it will return true too.
39. What danger do ERC777 tokens pose?  
    => reentrancy
40. According to the solidity style guide, how should functions be ordered?  
    => constructor - receive - fallback - external - public - internal - private
41. According to the solidity style guide, how should function modifiers be ordered?  
    => Visibility - Mutability - Virtual - Override - Custom modifiers
42. What is a bonding curve?  
    => a mathematical concept used to describe the relationship between price and the supply of an asset.
43. How does safeMint differ from mint in the OpenZeppelin ERC721 implementation?  
    => safeMint provides check to make sur the contract minting the NFT can actually receive it.
44. What keywords are provided in Solidity to measure time?  
    => seconds, minutes, hours, days, weeks
45. What is a sandwich attack?  
    => When users with access to the mempool sees a profitable trade, they then pay extra gas to process their purchase of the token sooner to drive the price and the demand of the token up, after that the original tx happens(the sandwiched tx), this increases the price even more. Then the attacker sells the token at an inflationed rate, thus devaluing the token tx value and pocketting the difference.
46. If a delegatecall is made to a function that reverts, what does the delegatecall do?
    => Delegatecall will return false, it does not revert.
47. What is a gas efficient alternative to multiplying and dividing by a multiple of two?  
    => bitwise shifts(left for mul and right for div)
48. How large a uint can be packed with an address in one slot?  
    => uint96
49. Which operations give a partial refund of gas?  
    => SELFDESTRUCT (24000 gas)
50. What is ERC165 used for?  
    => The ERC165 standard allows smart contracts to exercise type introspection on other contracts, that is, examining which functions can be called on them. This is usually referred to as a contract's interface.
51. If a proxy makes a delegatecall to A, and A does address(this).balance, whose balance is returned, the proxy's or A?  
   => The proxy's
52. What is a slippage parameter useful for?  
    => it is useful to avoid users swap a token let's say for a much higher price than they initially wanted
53. What does ERC721A do to reduce mint costs? What is the tradeoff?  
    => ERC721A do to reduce mint costs with batch miniting.  
    => transferFrom and safeTransferFrom transactions cost more gas.
54. Why doesn't Solidity support floating point arithmetic?  
    => Loss of Precision
55. What is TWAP?  
    => Time-Weighted Average Price: Average Price of a token most probably over a certain period of time
56. How does Compound Finance calculate utilization?  
    => All interest rates in Compound are determined as a function of a metric known as the utilization rate. The utilization rate Ua for a money market a is defined1 as:
Ua = Borrowsa / (Casha + Borrowsa − Reservesa)  
Borrowsa refers to the amount of a borrowed.  
Casha refers to the amount of a left in the system.  
Reservesa refers to the amount of a that Compound keeps as profit.  
Intuitively speaking, this is the percentage of money borrowed out of the total money supplied.  
For example: given that reserves are 0, if Alice supplies $500 USDC and Bob supplies $500 USDC, but Charles borrows $100 USDC, the total borrows is $100 and the total cash is 
500 + 500 − 100 = 900  
So the utilization rate is 
100 / (900 + 100) = 10 % 100 / (900 + 100) = 10%.  
A high ratio signifies that a lot of borrowing is taking place, so interest rates go up to get more people to inject cash into the system. A low ratio signifies that demand for borrowing is low, so interest rates go down to encourage more people to borrow cash from the system. This follows economic theory's idea of price (the "price" of money is its interest rate) relative to supply and demand.
57. If a delegatecall is made to a function that reads from an immutable variable, what will the value be?  
    => An immutable variable is stored in the bytecode of the implementation contract and it is this value which will be read. With a proxy, you can change/upgrade the value of an immutable variable by upgrading to a new implementation.
58. What is a fee-on-transfer token?  
    => token that by fundamental design, takes a percentage of internal commission upon transfer or trade
59. What is a rebasing token?  
    => Rebase, or elastic, tokens are cryptocurrencies that automatically adjust supply levels to maintain a constant value
### Hard
1. How does fixed point arithmetic represent numbers?

2. What is an ERC20 approval frontrunning attack?  
=> A malicious actor monitors the mempool for new approve transactions, before they are processed. Once they see an approve transaction, they quickly submit a "transferFrom" transaction to move the approved tokens to their own wallet, before the original approve transaction is processed. When the approve transaction is finally mined, it approves the exchange's transfer. But the tokens have already been stolen by the frontrunner via transferFrom. The exchange's subsequent transfer then fails, as the allowance has been emptied by the malicious frontrunner.

What opcode accomplishes address(this).balance?
=> SELFBALANCE

How many arguments can a solidity event have?  
=> A log can have up to 4 topics, but a non-anonymous solidity event can have up to 3 indexed arguments

What is an anonymous Solidity event?  
=> 

Under what circumstances can a function receive a mapping as an argument?

What is an inflation attack in ERC4626?  
=> ERC4626 vaults hold deposited assets and issue vault shares representing claims on those assets. When assets are deposited, the vault mints new shares proportional to the deposit amount. Conversely, when shares are burned, the corresponding assets are withdrawn. The inflation attack exploits a lack of validation on deposit amounts. A malicious actor deposits a very large amount of an asset, much more than they actually provide. This mints a huge number of new shares, inflating the total supply. They then immediately redeem a small subset of the shares, withdrawing real assets while leaving inflated shares outstanding. This effectively steals value from existing share holders by diluting the claims on underlying assets.

How many arguments can a solidity function have?  
=> 16

How many storage slots does this use? uint64[] x = [1,2,3,4,5]? Does it differ from memory?

Prior to the Shanghai upgrade, under what circumstances is returndatasize() more efficient than push zero?

Why does the compiler insert the INVALID op code into Solidity contracts?

What is the difference between how a custom error and a require with error string is encoded at the EVM level?

What is the kink parameter in the Compound DeFi formula?

How can the name of a function affect its gas cost, if at all?

What is a common vulnerability with ecrecover?

What is the difference between an optimistic rollup and a zk-rollup?

How does EIP1967 pick the storage slots, how many are there, and what do they represent?

How much is one Sazbo of ether?

What can delegatecall be used for besides use in a proxy?

Under what circumstances would a smart contract that works on Etheruem not work on Polygon or Optimism? (Assume no dependencies on external contracts)

How can a smart contract change its bytecode without changing its address?

What is the danger of putting msg.value inside of a loop?

Describe the calldata of a function that takes a dynamic length array of uint128 when uint128[1,2,3,4] is passed as an argument

Why is strict inequality comparisons more gas efficient than ≤ or ≥? What extra opcode(s) are added?

If a proxy calls an implementation, and the implementation self-destructs in the function that gets called, what happens?

What is the relationship between variable scope and stack depth?

What is an access list transaction?

How can you halt an execution with the mload opcode?

What is a beacon in the context of proxies?

Why is it necessary to take a snapshot of balances before conducting a governance vote?

How can a transaction be executed without a user paying for gas?

In solidity, without assembly, how do you get the function selector of the calldata?

How is an Ethereum address derived?

What is the metaproxy standard?

If a try catch makes a call to a contract that does not revert, but a revert happens inside the try block, what happens?

If a user calls a proxy makes a delegatecall to A, and A makes a regular call to B, from A's perspective, who is msg.sender? from B's perspective, who is msg.sender? From the proxy's perspective, who is msg.sender?

Under what circumstances do vanity addresses (leading zero addresses) save gas?

Why do a significant number of contract bytecodes begin with 6080604052? What does that bytecode sequence do?

How does Uniswap V3 determine the boundaries of liquidity intervals?

What is the risk-free rate?

When a contract calls another call via call, delegatecall, or staticcall, how is information passed between them?

What is the difference between bytes and bytes1[] in memory?

### Advanced
1. What addresses to the ethereum precompiles live at?  
   => The nine precompiles live in addresses 0x01 to 0x09

How does Solidity manage the function selectors when there are more than 4 functions?

If a delegatecall is made to a contract that makes a delegatecall to another contract, who is msg.sender in the proxy, the first contract, and the second contract?

How does ABI encoding vary between calldata and memory, if at all?

What is the difference between how a uint64 and uint256 are abi-encoded in calldata?

What is read-only reentrancy?  
=> A read-only reentrancy is a reentrancy caused by reading an outdated storage variable

What are the security considerations of reading a (memory) bytes array from an untrusted smart contract call?

If you deploy an empty Solidity contract, what bytecode will be present on the blockchain, if any?

How does the EVM price memory usage?

What is stored in the metadata section of a smart contract?  
=> ipfs of the solidity compiler produced JSON

What is the uncle-block attack from an MEV perspective?

How do you conduct a signature malleability attack?

Under what circumstances do addresses with leading zeros save gas and why?

What is the difference between payable(msg.sender).call{value: value}(””) and msg.sender.call{value: value}(””)?

How many storage slots does a string take up?

How does the --via-ir functionality in the Solidity compiler work?

Are function modifiers called from right to left or left to right, or is it non-deterministic?

If you do a delegatecall to a contract and the opcode CODESIZE executes, which contract size will be returned?

Why is it important to ECDSA sign a hash rather than an arbitrary bytes32?

Describe how symbolic manipulation testing works.

What is the most efficient way to copy regions of memory?

How can you validate on-chain that another smart contract emitted an event, without using an oracle?

When selfdestruct is called, at what point is the Ether transferred? At what point is the smart contract's bytecode erased?

Under what conditions does the Openzeppelin Proxy.sol overwrite the free memory pointer? Why is it safe to do this?

Why did Solidity deprecate the "years" keyword?  
=> it has been deprecated because not every year is composed by 365 days (leap years)

What does the verbatim keyword do, and where can it be used?  
=> In short, it will allow us to add our own bytecode to an already compiled contract. It can be used in YUL for optimization purposes

How much gas can be forwarded in a call to another smart contract?

What does an int256 variable that stores -1 look like in hex?  
=> 0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff

What is the use of the signextend opcode?  
=> SIGNEXTEND does appear rarely. Because SIGNEXTEND is used for complement code, and the complement code is to use addition instead of subtraction. For example, for 4 bit numbers, y = x + a mod 16 , subtracting 1 is equal to adding 15, which is why the complement code of -1 is equal to 1111 , standing for 15.

Why do negative numbers in calldata cost more gas?

What is a zk-friendly hash function and how does it differ from a non-zk-friendly hash function?

What is a nullifier in the context of zero knowledge, and what is it used for?

## Bonus(Interview questions I came up with):
What's the difference between a contract and an abstract contract?
=> An abstract contract has at least one of its functions not implemented
