### Needed before launch of mainnet

block:one_tx_per_account/1 needs to be implemented

parts of the api need to be encrypted, to keep channel state private.

test transaction types in easy.

There should be a way to start the node in lite-mode. So that it only downloads headers, not full blocks. 1000CHF (paid in ETH or BTC)

trees:garbage needs to garbage collect more trees. 100 CHF (paid in ETH or BTC)

We should optionally garbage collect old blocks, only keep the headers. 400 CHF (paid in ETH or BTC)

spk:is_improvement needs better checks. 50 CHF (paid in ETH or BTC)
Make sure delay isn't too big, and the fees aren't too high. 

we need a cron like process to match trades in the markets.

We need to regularly check on our channels to see if either participant is running out of funds. There needs to be enough money left to cover the cost of the channel for the amount of time until you can close the channel without your partner's help.
When you are running short on funds you need to ask your partner to close the channel. If they don't, you need to start closing the channel without their help.

In spk prove_facts2, the burn and existence trees store by hash not by integer, so the code needs to be modified for them. 60 CHF (paid in ETH or BTC)

It is currently possible for an attacker to trick us into ignoring a good block. They trick us into storing a good blocks hash into block_hashes. They give us a good block's header, but mix in some bad transactions, or censor a transaction, or they don't give us some of the merkel tree we need to verify the transactions. 1000 CHF (paid in ETH or BTC)
Make sure that if something was garbage collected from a merkel tree, and we try accessing the thing, it gives a different message than trying to access something that doesn't exist. Make sure we don't assume a block is invalid just because we don't have the proof of it's validity. 200 CHF (paid in ETH or BTC)

We need to also add a way for the two parties to work together to close the channel early, so they don't have to wait to do a timeout_tx. We can either make a new tx, or make channel_team_close more complicated. 200 CHF (paid in ETH or BTC)
We need a test showing that it works.
(maybe this task was already done? need to check)


### Things we can do after launch of mainnet

it would be nice if instead of embedding those sed commands into the makefile, if instead we read them from a different file.
Then we wouldn't have to escape all the newlines and double-quotes.

Secrets seems unnecessary. As soon as we find out a secret, why not use arbitrage to update all the channels immediately?

/tests holds tests that use multiple nodes. Currently these tests use curl, so it isn't obvious if an error happens. You have to review the log by hand.
It would be much better if these test were re-written in python or erlang, and we could check the responses from each command, that way an error is thrown when it happens, and it will be easier to diagnose what went wrong.
Also, we wont have to open 4 terminals to run these tests.



maybe accessing the internal handler should require a signed request with a nonce.
The server should ignore commands that don't increment the nonce from last time.

alternatively, we could just turn on a firewall. This is simpler, but it has the drawback that commands on a local node have to originate from the same computer.


Prices listed are minimums. If the code is high quality, you can get much more.
(Bounty program hasn't started yet. Talk to Zack before starting a bounty)

Off-chain markets. 500 CHF (paid in ETH or BTC)
We need an integration test where one node is a market, and the other two nodes are traders. 

download_blocks:get_blocks should download multiple blocks at a time. 100 CHF (paid in ETH or BTC)

We need to test channel_solo_close and channel_slash and channel_timeout from easy. 30 CHF (paid in ETH or BTC)

Cold storage. 150 CHF (paid in ETH or BTC)

Download blocks talk/1 seems useless. talker:talk is accomplishing the same goal. 40 CHF (paid in ETH or BTC)

It is possible to use channel_slash to store data in a channel such that the channel can't be closed with a channel_timeout.
Maybe this is a mistake.

Javascript light wallets need to be able to do all the channel stuff that full nodes do. 2000 CHF (paid in ETH or BTC)

We need to update download_blocks so that peers get ranked, and we spend more time talking to higher-ranked peers.

download_blocks could be more efficient.

Maybe nodes need to advertise their own IP/port combo as a peer?

It would be nice if there were some macros for chalang/src/compiler_lisp2.erl that did backtracking. that way we wouldn't have to think about control flow when making smart contracts.

The current market design charges a 1/10000 fee on every trade. This is to protect from rounding errors. There is a more elegant way to stop rounding errors. Set a certain maximum trade size. All orders must be measured in increments of the same size 
A limitation of channels is that their output amounts are measured in integers from 0 to 10000.
Every 1 in G of the possible 10000 outputs can be valid.
A1 = amount of money getting matched from our bet,
A2 = amount of money in biggest possible bet,
B = A2 div 10000,
0 == A1 rem B
Making A1 rem B == 0 limits the possible output values of the contract, which slightly reduces liquidity. Being able to reduce the fee to zero is worth this small cost.
