# Ethereum Smart Contract

## TwinToken(XTW) Contract Details
- Creates/Mints 10 billion Tokens and holds them inside contract.
- Token and Sale Contract reference eachother.
- Code based on OpenZeppelin audited erc20.
- Tested on truffle for unit testing.
- Uses Safemath Library from OpenZeppelin for safer mathematical calculations.
- Added distrubution function for ease of access. Only accessible to Owner of the contract.

```
function distributeTokens(address _to, uint256 _value) public onlyOwner returns (bool success) {
        _value = _value * 10**18;
        require(balances[owner] >= _value && _value > 0);
        
        balances[_to] = balances[_to].add(_value);
        balances[owner] = balances[owner].sub(_value);
        Transfer(owner, _to, _value);
        return true;
}
```


## TwinToken(XTW) Crowdsale Contract Details
- Converts payable ETH to TOKEN's directly to user
- ETH payed to contract is forwarded to a different wallet (owner's wallet)
- Updateable ETH/TOKEN rate

```
function changeRate (uint256 _RATE) external onlyOwner {
       RATE = _RATE;
}
```

- Ability to turn on/off sale. (via sale contract)
- Crowdsale ends on a specific date
- Token contrbutions will be removed from the Crowdsale contract and transfered to the purchaser.
