###########################
Frequently Asked Questions
###########################

What's the simplest explanation of BTC Relay?
=============================

It allows users to pay with Bitcoin to use Ethereum.


How to use BTC Relay?
=============================

If you're a user, you should not need to use BTC Relay directly since it works
behind the scenes.

If you're a developer, did you see `How to use BTC Relay?
<https://github.com/ethereum/btcrelay/tree/master#how-to-use-btc-relay>`_


Who is BTC Relay for?
=============================

Developers who want a secure, fully decentralized and trustless method of
verifying Bitcoin transactions for their Ethereum and smart contract applications.

BTC Relay is a building block for developers that want interoperability between
Ethereum and Bitcoin.  For example, developers who want to allow their users to
pay with Bitcoin to use their Ethereum application.

How to be a Relayer and receive incentives?
=============================

Relayers are those who submit block headers to BTC Relay. To incentivize the community to be relayers, and thus allow BTC
Relay to be autonomous and up-to-date with the Bitcoin blockchain, Relayers can submit block headers to BTC Relay. 
When any transaction is verified in the block, or the header is retrieved, Relayers will be rewarded a fee (see details at https://github.com/ethereum/btcrelay/tree/master#incentives-for-relayers).

**Warning**: as specified above, incentives are only sent when transactions are verified in the block or the header is retrieved, not when the block is submitted.

Why isn't verifyTx / relayTx working?
=============================

* Does your transaction have at least 6 Bitcoin confirmations?

* Did you pass the correct parameters to
  `construct the Merkle proof <https://www.npmjs.com/package/bitcoin-proof>`_ correctly?
  Viewing the page source of some `examples <https://github.com/ethereum/btcrelay/tree/master#examples>`_
  might help.

* Did you send at least the fee as indicated by `getFeeAmount() <https://github.com/ethereum/btcrelay/tree/master#getfeeamountblockhash>`_?


What prevents fees from being too high?
=============================

If a fee for any block header is too high, anyone may
`changeFeeRecipient() <https://github.com/ethereum/btcrelay/tree/master#changefeerecipientblockhash-fee-recipient>`_
to themselves.

They can compare the current fee against `getChangeRecipientFee() <https://github.com/ethereum/btcrelay/tree/master#getchangerecipientfee>`_
to see if the fee is excessive.  Callers of ``changeFeeRecipient()``
must make sure to satisfy all `requirements <https://github.com/ethereum/btcrelay/tree/master#changefeerecipientblockhash-fee-recipient>`_
for successful completion.


How does BTC Relay work?
=============================

BTC Relay is an **Ethereum contract** that stores **Bitcoin block headers**. BTC Relay
uses these headers to build a mini-version of the Bitcoin blockchain:
a method used by Bitcoin SPV light wallets.

Relayers who submit headers can earn Ether.  When an application processes a
Bitcoin payment, it uses a header to verify that the payment is legitimate.
The relayer of the particular header earns a fee, usually specified when the
relayer submitted the header.

The cycle of relayers submitting headers, then applications processing Bitcoin
payments and rewarding a relayer with a micro-fee, can allow the system to be
autonomous and self-sustaining.

.. image:: http://btcrelay.org/images/howitworks.png
   :align: center
