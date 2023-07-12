// SPDX-License-Identifier: MIT

pragma solidity ^0.8.9;




import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";

import "@openzeppelin/contracts/access/Ownable.sol";

import "@openzeppelin/contracts/access/AccessControl.sol";




contract MyToken is ERC1155, AccessControl {

    bytes32 public constant URI_SETTER_ROLE = keccak256("URI_SETTER_ROLE");

    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");

    // bytes memory public MINTER_ROLE1 = keccak256("MINTER_ROLE");

    bytes1 a = 0xb5;

    uint256 public  totalSupplyIDTOKEN = 0;

    //uint256 public  balances = 0;

     mapping(address => uint256) private balances;




    constructor() ERC1155("") {

        _grantRole(DEFAULT_ADMIN_ROLE, msg.sender);

        _grantRole(URI_SETTER_ROLE, msg.sender);

        _grantRole(MINTER_ROLE, msg.sender);

        _mint(msg.sender, totalSupplyIDTOKEN, 10**18, "");

        

        // balances[msg.sender] = totalSupply;

    }








    struct Employee{

        uint256 employeedId;

        uint256 dateofjoin;

        address walletaddress;

    }




    mapping(uint256 => Employee) public employee1;


    function saveEmployeeDetails(uint256  _employeedId, uint256  _dateofjoin, address  _walletaddress) external {

        Employee storage employee = employee1[_employeedId];

        employee.employeedId = _employeedId;

        employee.dateofjoin = _dateofjoin;

        employee.walletaddress = _walletaddress;

    }




    function transfer(address _to, uint256 _value) internal {

       require(balances[msg.sender] >= _value, "Insufficient balance");
        balances[msg.sender] -= _value;
        balances[_to] += _value;
        emit Transfer1(msg.sender, _to, _value);

    }


    function proofFor(string memory document) public pure returns(bytes32) {
        return sha256(bytes (document));
    }




    function companyCriteria(uint256 emplID, bytes calldata _data) external returns (uint256){
        Employee storage empl = employee1[emplID];
        //uint256 todaydate =  getCurrentTimestamp();
       uint256 yearremaining = 100;
        //return (yearremaining*2);
        //  require(1 >0, " You do not qualify for the compensation" );
         safeTransferFrom(msg.sender, empl.walletaddress, totalSupplyIDTOKEN,  yearremaining*2, _data);
        // transfer(empl.walletaddress, yearremaining*2);
        return 0;
    }


    function getCurrentTimestamp() public view returns (uint256) {
        return block.timestamp;
    }

    function setURI(string memory newuri) public onlyRole(URI_SETTER_ROLE) {
        _setURI(newuri);
    }


    function mint(address account, uint256 id, uint256 amount, bytes memory data)
        public
        onlyRole(MINTER_ROLE)
    {
        require(amount > 0, "Amount should be greater than zero");
        balances[msg.sender] += amount;
        // totalSupply += amount;
        _mint(account, id, amount, data);
    }




    function mintBatch(address to, uint256[] memory ids, uint256[] memory amounts, bytes memory data)

        public

        onlyRole(MINTER_ROLE)

    {

        _mintBatch(to, ids, amounts, data);

    }




    // The following functions are overrides required by Solidity.




    function supportsInterface(bytes4 interfaceId) public
        view
        override(ERC1155, AccessControl)returns (bool)
    {
        return super.supportsInterface(interfaceId);
    }

    // Event to emit when a transfer occurs
    event Transfer1(address indexed from, address indexed to, uint256 value);
    // Function to get the balance of an address

    function getBalance(address _address) external view returns (uint256) {
        return balances[_address];
    }

    // Function to transfer tokens from one address to another

}
