# Airport Noise Monitor Project


# Background
In the United State, the FAA has recently adjusted the flight-path algorithms to allow airplanes to fly lower and fly more-controlled routed.
The inintended consequence is such that the airline traffic (for airplanes on final approach to a runway) is much more concentrated along 
a narrow strip of land.  Home-owners in those areas are very-negatively impacted.

Most airports create a noise-complaint process whereby homeowners can report excessively loud airplanes or excessive noise during night-time hours.
While this is great in theory, it's highly subjective and difficult to capture the information necessary to report a noise complaint.

We propose that an array of noise-monitoring sensors could accurately capture an offending airplanes noise (in decibals) and report the data to a central database.
With hundreds of such sensors along the final-approach-path of a nearby airport, it would be possible to accurately excessive noise pollution.


# Pre-Requisites and Assumptions and Make-Believe
In this imaginary project, we have a IoT sensor that can be deployed cheaply and easily to interested home-owners.
Home owners will use a web app to register their sensor to record their email address and some kind of confirmation process will affirm the info.
The sensor knows it's GPS location, the current time (epoch), and is capable of monitoring air-plane noise and recording the peak noise in decibals.
If the noise exceeds a threshold, it is capable of making an rpc call to an ethereum contract that will record the event.


# Brainstorming Contract Needs
A contract will be deployed for each airport.  In this project, we will use the Baltimore-Washington International Airport.  
This will be set as a state variable in the constructor.

Within the contract, we will need a struct to define the sensor and an array to hold all of those sensors.

contract NoiseMonitor {
	struct Sensor {
		uint: longitude,
		uint: lattitude,
		string: email,
		bool: isRegistered
	}
	string airport public;
	mapping (string => Sensor ) public sensors;
}

 
