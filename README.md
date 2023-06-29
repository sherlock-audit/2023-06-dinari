
# Dinari contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Q&A

### Q: On what chains are the smart contracts going to be deployed?
Arbitrum
___

### Q: Which ERC20 tokens do you expect will interact with the smart contracts? 
Our own dShare tokens (BridgedERC20), USDC, and USDT
___

### Q: Which ERC721 tokens do you expect will interact with the smart contracts? 
none
___

### Q: Which ERC777 tokens do you expect will interact with the smart contracts? 
none
___

### Q: Are there any FEE-ON-TRANSFER tokens interacting with the smart contracts?

No
___

### Q: Are there any REBASING tokens interacting with the smart contracts?

No
___

### Q: Are the admins of the protocols your contracts integrate with (if any) TRUSTED or RESTRICTED?
Restricted (if any)
___

### Q: Is the admin/owner of the protocol/contracts TRUSTED or RESTRICTED?
Trusted
___

### Q: Are there any additional protocol roles? If yes, please explain in detail:
1. The roles
- BidgedERC20.MINTER_ROLE
- BridgedERC20.BURNER_ROLE
- OrderProcessor.OPERATOR_ROLE
- OrderProcessor.PAYMENTTOKEN_ROLE
- OrderProcessor.ASSETTOKEN_ROLE

2. Actions roles can take
- MINTER_ROLE: Can mint token to accounts
- BURNER_ROLE: Can burn token held by msg.sender
- OPERATOR_ROLE: Responsile for filling and canceling order requests. Can call fillOrder, cancelOrder, (takeEscrow and returnEscrow).
- PAYMENTTOKEN_ROLE: Whitelist of accepted stablecoins. Allows orders with paymentToken.
- ASSETTOKEN_ROLE: Whitelist of protocol dShare tokens. Allows orders with assetToken.

3. Expected outcomes
- MINTER_ROLE: Restrict dShare minting to buy order processing contracts (BuyOrderIssuer and DirectBuyIssuer).
- BURNER_ROLE: Restrict dShare burning to sell order processing contracts (SellOrderProcessor).
- OPERATOR_ROLE: Restrict order cancellation and fulfillment to trusted offchain "bridge" service provider addresses. Initially these addresses will be Dinari's automated vault management service. As 1:1 backing is confirmed, orders are fulfilled.

___

### Q: Is the code/contract expected to comply with any EIPs? Are there specific assumptions around adhering to those EIPs that Watsons should be aware of?
dShare tokens (BridgedERC20) are ERC20 and ERC2612 compliant.

___

### Q: Please list any known issues/acceptable risks that should not result in a valid finding.
DirectBuyIssuer relaxes the escrow lock on tokens deposited by users. This allows the operators to withdraw the tokens without filling the order and minting corresponding dShare tokens. 

The operators are trusted and responsible for upholding the value of the dShare tokens by correctly filling the orders. 
___

### Q: Please provide links to previous audits (if any).
none
___

### Q: Are there any off-chain mechanisms or off-chain procedures for the protocol (keeper bots, input validation expectations, etc)?
The protocol is designed to operate like a bridge. The operator role is a bot/keeper that executes offchain processes to maintain the offchain vault of shares before filling the order.

___

### Q: In case of external protocol integrations, are the risks of external contracts pausing or executing an emergency withdrawal acceptable? If not, Watsons will submit issues related to these situations that can harm your protocol's functionality.
Not acceptable - but likely not applicable
___



# Audit scope

