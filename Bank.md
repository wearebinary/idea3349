// SPDX-License-Identifier: MIT Bank
pragma solidity ^0.8.7;

contract Bank {
    uint totalBalanceOfContract = 0;

    mapping(address => uint) public balances;
    mapping(address => uint) depositeTimeStamp;

    function addBalance() public payable{
        balances[msg.sender] = msg.value;
        totalBalanceOfContract = totalBalanceOfContract + msg.value;
        depositeTimeStamp[msg.sender] = block.timestamp;
    }
    
    function withdraw(uint ammount) public payable{
        address payable withdrawto = payable(msg.sender);
        withdrawto.transfer(ammount);
        totalBalanceOfContract = totalBalanceOfContract - ammount;
        balances[msg.sender] = totalBalanceOfContract;
    }
}
