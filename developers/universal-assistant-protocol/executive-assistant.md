# Executive Assistant

The [IExecutiveAssistant](https://github.com/yearone-io/universal-assistant-protocol/blob/main/contracts/IExecutiveAssistant.sol) interface defines a standard for assistant contracts that participate in the Universal Assistant Protocol (UAP). Its primary role is to outline a single function, execute, which is responsible for processing transactions that have been delegated to an assistant via a universal receiver delegate. This interface ensures that all executive assistants adhere to a consistent method of execution within the UAP framework.

```solidity
interface IExecutiveAssistant {
    function execute(
        address assistantAddress,
        address notifier,
        uint256 value,
        bytes32 typeId,
        bytes memory data
    ) external returns (bytes memory);
}
```

The execute function is designed to be called via delegatecall from the universal receiver delegate, meaning that when it runs, it executes in the context of the calling contract (typically a Universal Profile). As a result, msg.sender inside the execute function will refer to the Universal Profile, allowing the assistant to interact with its data store. Specifically, the assistant is expected to read its operational instructions from the Universal Profile’s ERC725Y data store under the key formatted as "UAPAssistantInstructions:". The function parameters include the assistant’s own address, the notifier (the address that triggered the action), the Ether value sent with the transaction, a transaction type identifier (typeId), and additional data. After processing, the function returns a bytes array containing updated values and data encoded using abi.encode.

This interface not only standardizes how executive assistant contracts operate within the protocol but also facilitates a modular and secure approach to handling various transaction types based on on-chain configurations and pre-defined instructions.
