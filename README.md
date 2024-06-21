Smart Contract Project

In this project we create smart contract that implements the require(), assert() and revert() statements.

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain.

This program serves as a simple and straightforward introduction to Solidity programming, and can be used as a stepping stone for more complex projects in the future.

CODE


// SPDX-License-Identifier: MIT
pragma solidity 0.8.18;

contract Mytoken {
    constructor() {
        owner = msg.sender;
    }

    //public variables here
    string public name = "simple";
    string public symbol = "SIMP";
    uint public totalSupply = 0;
    address public owner;

    // emits events 
    event Mint(address indexed to, uint amount);
    event Burn(address indexed from, uint amount);
    event Transfer(address indexed from, address indexed to, uint amount);

    //errors
    error InsufficientBalance(uint balance, uint withdrawAmount);

    // mapping varaible here 
    mapping(address => uint ) public balances;

    // modifiers 
    modifier onlyOwner {
        assert(msg.sender == owner);
        _;
    }
    //mint function
    function mint (address _address, uint _value) public onlyOwner{
        totalSupply += _value;
        balances[_address] += _value;
        emit Mint (_address, _value);
    }

    // burn function 
    function burn (address _address, uint _value) public onlyOwner{
        if (balances[_address]<  _value){
            revert InsufficientBalance ({balance: balances[_address],withdrawAmount: _value});
        }else{
            totalSupply -= _value;
            balances[_address] -= _value;
            emit Burn(_address, _value);
        }
    }

    function transfer (address _reciever, uint _value) public {
        require (balances[msg.sender] >= _value, "Account must be greater then transfered value");
        balances[msg.sender] -= _value;
        balances[_reciever] += _value;
        emit Transfer(msg.sender, _reciever, _value);
    }
}

CODE EXPLANATION

So I have created this smart contract which we have built,example like my token it is simple token smart contract then with a name 
called symbol name SIMPLE

Here total supply initialzed with 0 and there is a public like this variable we have initialized

we are using constructor so once we deploy a smmart contract 

We created some function like minting function and burn function and and also a transfer function
So in this example we have we also have some events like main burn and transfer to record the logs of the event which are happening 
in this smart contract
and we define our own custom error in suffering balance and mapping address and balnce to store the mappingof of that balamc

We have one modifier caled only owner so here we are using assert ot check the message and sender of each function is our owner 
so this function will only called by the owner not any by anyone
and similarly for burn function and then transfer is public people can call this transfer function

But we have also have required to check if current message or sender balanceof the sender must be greater than the value taht which we want 
to displayed


AUTHOR

ANISH CHOUDHARY 

@Anishakki01


LICENECE

// SPDX-License-Identifier: MIT pragma solidity 0.8.18
SO I test this contract here in remix let's deploy it once more.





