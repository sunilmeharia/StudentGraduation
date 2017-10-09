# StudentGraduation
Smart Contract for Certification of TheBlockchianhub
pragma solidity ^0.4.15;
contract Student
{
    // Student data variables
    address public owner;
    bytes32 public student;
    bytes32 public school;
    uint256 public graduateDate;
    bytes32 public graduateStatus;
 
    //Set Owner
    function graduation() {
        owner = msg.sender;
    }
    modifier onlyowner() { 
        if (msg.sender == owner){
_;
  }
  else {
     revert();
}

    }

    // Create initial Graduate Event
    function createGraduate(bytes32 _student, bytes32 _school, uint256 _graduateDate, bytes32 statusEntry, bytes32 descriptionEntry) onlyowner
    {
        student = _student;
        school = _school;
        graduateDate = _graduateDate;
        setStatus(statusEntry);
        bytes32 name = "Graduate Data Creation";
        
        majorEventFunc(graduateDate, name, descriptionEntry);
    }
    
    function getOwner() returns (address _owner)
    {
        return owner;
    }
    
    // Track changes
    function setStatus(bytes32 status) onlyowner
    {
        graduateStatus = status;
        majorEventFunc(block.timestamp, "Changed Status", status);
    }
  
   

    // Log major events
    function majorEventFunc(uint256 eventTimeStamp, bytes32 name, bytes32 description)
    {
        MajorEvent(block.timestamp, eventTimeStamp, name, description);
    }

    // Declare event structure
    event MajorEvent(uint256 logTimeStamp, uint256 eventTimeStamp, bytes32 indexed name, bytes32 indexed description);
    
    // This function gets executed if a transaction with invalid data is sent to
    // the contract or just ether without data. We revert the send so that no-one
    // accidentally loses money when using the contract.
    function () {
        revert();
    }
}
