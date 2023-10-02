// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract DeadmansSwitch {
    address public owner;
    address public preSetAddress;
    uint public lastCheckedBlock;

    constructor(address _preSetAddress) {
        owner = msg.sender;
        preSetAddress = _preSetAddress;
        lastCheckedBlock = block.number;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can call this function");
        _;
    }

    function still_alive() public onlyOwner {
        lastCheckedBlock = block.number;
    }

    function checkStatus() public view returns (bool) {
        return (block.number - lastCheckedBlock) <= 10;
    }

    function executeSwitch() public onlyOwner {
        require(!checkStatus(), "Owner is still alive");
        payable(preSetAddress).transfer(address(this).balance);
    }
}
