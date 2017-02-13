# Airport Noise Monitor Project


# Background
In the United State, the FAA has recently adjusted the flight-path algorithms to allow airplanes to fly lower and fly more-controlled routed.
The inintended consequence is such that the airline traffic (for airplanes on final approach to a runway) is much more concentrated along 
a narrow strip of land.  Home-owners in those areas are very-negatively impacted.

Most airports create a noise-complaint process whereby homeowners can report excessively loud airplanes or excessive noise during night-time hours.
While this is great in theory, it's highly subjective and difficult to capture the information necessary to report a noise complaint.

We propose that an array of noise-monitoring sensors could accurately capture an offending airplanes noise (in decibals) and report the data to a central database.
With hundreds of such sensors along the final-approach-path of a nearby airport, it would be possible to accurately excessive noise pollution.

A contract will be deployed for each airport.  In this project, we will use the Baltimore-Washington International Airport (BWI).  
This will be set as a state variable in the constructor.

I recognize that this might be the worlds worst practical use-case for ethereum, but there's one compelling readon that ethereum adds and it's in the truth-keeping.  Data 
can't be altered or doctored.  Granted, the sensor can doctor it all it wants, but that's a problem for some government regulations department.

# Pre-Requisites and Assumptions and Make-Believe
In this imaginary project, we have a IoT sensor that can be deployed cheaply and easily to interested home-owners.
Homeowners will need to register the device. The registration process will force the homeowner to complete some 
basic details about themselves and pick form a list of airports (contact instance addresses).  This process 
will also call the contract to Add/Update it's sensor registration into the contract.
For the purpose of this project, let's pretend  the sensor will have local 'config' that will hold something similar to:
{
	contractAddress: 0xb61a1675eebb38a1fe16c2d724c0a0ac47529cf9,
	sensorAddress: 0x67719186b640f0cf1a30c1f9f11ffc4f8370045e,
	rpcUrl: "10.12.13.14:8545"
	name: "Mike Murphy",
	email: "mmurphy384@yahoo.com",
	streetAddress1: "123 Elm Street",
	streetAddress2: "",
	city: "Some City",
	province: "MD",
	country "US",
	thresholdDb: 30
}
The sensor will automaticaly determine it's GPS longitude and latitude.
Each time the sensor it powered up, it will re-register itself with the contract which will set the longtitude and latitude.
The sensor  is capable of monitoring air-plane noise and recording the peak noise in decibals.
If the noise exceeds a threshold, it is capable of making an rpc call to an ethereum contract that will record the event.


# Brainstorming Contract Needs
Within the contract, we will need a struct to define the sensor and an array to hold all of those sensors.  We'll also need public functions to addUpdate sensor, addComplaint.
we'll also need a way to get a list of complaints for a given sensor.  the p-code for this contract might look like:

contract NoiseMonitor {
	
	string public airportCode;
	
	struct Sensor {
		address addr,
		uint longitude,
		uint lattitude,
		uint dateLastRegistered
	}

	struct Complaint {
		address sensorAddr,
		uint epochTime,
		uint longitude,
		uint lattitude,		
		uint noiseDb
	}

	mapping (string => Sensor ) public sensors;

	mapping (address => Complaint) public complaints;

	function addUpdateSensor(uint id, uint longitude, uint lattitude)  {}	// msg.sender is the sensorAddress.  Can we just send data:{} instead of variables?

	function addComplaint(uint noiseDb) {}                                  // msg.sender is the sensorAddress

	function getComplaints(address sensorAddr) constant return (complaints _complaints) {}
	
	function getSensor(address sensorAddr) constant return (Sensor _sensor) {}
	

}

 
