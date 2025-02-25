# Overview

If you're unfamiliar with LSP1 Universal Receiver, please check [Lukso's guide on LSP1](https://github.com/lukso-network/LIPs/blob/main/LSPs/LSP-1-UniversalReceiver.md).

Our [UniversalReceiverDelegateUAP](https://github.com/yearone-io/universal-assistant-protocol/blob/main/contracts/UniversalReceiverDelegateUAP.sol)  contract serves as a Universal Receiver Delegate tailored for the Universal Assistant Protocol (UAP). It extends a base universal receiver delegate, allowing it to intercept and handle incoming transactions on a Universal Profile. The primary purpose is to dynamically evaluate transaction types and, based on on-chain configurations stored in the profile’s data, delegate the transaction processing to a series of "assistant" contracts—specifically, executive and screener assistants (coming soon).

When a transaction is received, the contract’s `universalReceiverDelegate` function is invoked. This function first attempts to fetch a type-specific configuration using a generated mapping key that incorporates the transaction’s `typeId`. If a configuration exists, it decodes an ordered list of executive assistant addresses from the returned data. In cases where no configuration is found, it simply defers to the default behavior defined in its parent contract.

Overall, this design enables flexible and modular transaction handling on Universal Profiles. By leveraging on-chain configurations to dynamically determine which assistant contracts to engage, the system supports customizable behavior for different transaction types while maintaining a robust security model through screening and trust verification mechanisms.
