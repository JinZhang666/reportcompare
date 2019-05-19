# reportcompare
# spring
3. Design

3.1 Onboard System 
3.1.1 Body Structure
The Micro Air Vehicle (MAV) concludes two main systems (quadcopter and gripper). The quadcopter system is supposed to be stably controlled, well-operated, and capable to vertically lift up, land on, rotate and hover in the air. The gripper system is designed to successfully complete all missions of pick up and drop off packages to the target point. 

3.1.2 Design
In these two parts, the design idea of the aircraft vehicle is presented on a 3D printed vehicle frame. This frame is just for design and test use, the final product may change the material of the structure. 
As shown in the picture above, this is a 3D printing design of the vehicle structure. which was the initial design. All drawings of each single part are sketched and assembled in Auto Fusion 360 software. Size of the entire MAV is minimized to 30 cm for each axis now. The quadcopter system includes four arms, one base and one top board. The gripper system is attached at the bottom center of the drone in order to keep its center gravity point (CG) and that of the drone at the same z-axis (vertical direction). Two front claws are able to open widely and close tightly upon the rotational degree of two spur gears inside (up to 180°).
3.1.3 Fabrication
All designed parts in the test version vehicle structure are fabricated by 3D printer as the figure 2 shown below, and the material used is PLA filament (1.75 mm, white). Then, these are assembled with some supply materials like screws and bolts. Final product consists of 3D assembled parts and purchased electronic parts. The figure 2 shows the recent prototype used for testing flight performance, and its weight is 308 grams for now. The estimated weight of the gripper system is 30 grams in total, which means the final product would be around 350 grams after placing two cameras on it. 
3.1.4 Gripper control system
The system will be powered by a 9V battery connecting to Arduino board, and the output from Arduino is 5V, so both the gripper and a camera only require 5V power supply. The gripper will be functioned by XBEE wireless electrical components which are setting up serial communication with each other. XBEE components are placed on XBEE Arduino shields, and tell the servo motor to drive certain amount of clockwise rotation by clicking the first button, or counterclockwise rotation by clicking the second button.

3.1.5 Power system
One battery for flight control system we used is 1300mah battery with 11.1V output, and the other one for camera and gripper is 9V CVS battery.
3.1.6 Distribution board
We decided to use the distribution board to manage all the wires. The battery can provide a 12V input to the distribution board and with several devices on the board, it is easy to separate the power from the battery into many inputs and outputs which could connect to all electronics. 
3.1.7 Arduino UNO
It is an open source board specially utilized for robot programming. Arduino IDE is a software we used for programming Arduino UNO board, and XCTU is the one we used to set up XBEE transmitter, receiver and servo motor. (servo motor is used to actuate grippers which rotate clockwise and counterclockwise)
3.1.8 Set up
After building all circuits, an XBEE remote demo codes(transmitter and receiver) will be verified in Arduino IDE, then uploaded to Arduino boards. First, use an XBEE USB explorer to set up each XBEE component by applying the XCTU software. Make sure two Xbees are on the same channel with the same panID so these two may communicate with each other. One is the coordinator, and the other one is the end effector. The serial rate is supposed to be 9600, as the same as the default value in Arduino IDE servo head files. Open the dialogue window in XCTU, and type ‘+++’ for the transmitter, and we see ‘OK’ from the receiver. After the serial communication is well-set, place an XBEE Arduino shield on each Arduino UNO board, then insert the XBEE component to the shield. 
3.1.9 Flight control system
As the figure 3 shown. Radio Receiver receives the movement signal sent by the remote control (given by pilot) and sent it to a microcontroller. The microcontroller calculates the signal from the user and from its built-in Inertial measurement unit (IMU) system, then output a signal to Electrical speed controller (ESC). There are four groups of ESC and motors mounted on the aircraft. Each ESC gives individual speed to its corresponding motor based on the signal it receives in order to control the flight behavior of the MAV. 
3.1.10 Inertial measurement unit system (IMU)
IMU is an electronic device that collects the data measured by the sensors built inside. After IMU collects the data from built-in sensors, it will analyze the sensor data in order to guide the flight behavior of the aircraft.  The sensors include accelerometers and gyroscope which can detect the accelerated speed and body attitude of the aircraft. We chose Ardupilot Mega (APM) to implement our IMU System. It is a relatively general use autopilot board which is designed for different types of aircraft, including the MAV we designed. The flight control software written in C++ programming language can be loaded on the board to control basic flight movements. In addition, the stability during pick up task is the key issue we considered, the program helps us implement the autonomous stabilization functionality. 
3.1.11 Camera system
Two micro cameras with 5.8GHz FPV transmitters are using on the design to capture the front and bottom views. Each camera provides 150 degrees horizontally field of view. Two First Person View (FPV) receivers are connected with two snowflake monitors, because there are two cameras modules. Four 12V lipo batteries are used to power the receivers and snowflake monitors.
The FPV cameras are powered by the Arduino board, and the voltage that the board can provide is about 5v. After the test, the transmission frequency we choose is 5665MHz. This is the frequency that can get pictures from the camera. [6]
3.1.12 Thrust system
EMAX motors and RAYCorp 10*4.5 propellers are chosen to provide the thrust to the MAV. Combined with these glass fiber propellers, each motor can deliver an 1.131kg of thrust. That’s strong enough for a 500g MAV. The glass fiber also has strong compressive strength to make sure propellers would not be broken easily. 
3.2 Remote-Operation 
3.2.1 Flight control system
For flight control system, we chose FlySky 2.4GHz 6 Channel Digital Transmitter and Receiver Radio System. We setup the transmitter according to the official tutorial of ardupilot.[1] Different Channels on the transmitter are responsible for different movements of the flight the RC input channels are: 
- Channel 1: Roll input (move left or right)   
- Channel 2: Pitch input (move forward or backward)
- Channel 3: Throttle input (move uplift and downfall)
- Channel 4: Yaw input (rotate the head)
- Channel 5: Flight Mode Shift (to stabilize mode)
- Channel 6: Power for the receiver
3.2.2 Gripper control system (picture)
When clicking at any of two buttons, the motor is toggled between the rotation in main direction and stop. Then, first click at any of two buttons, the motor will rotate in button's direction, and when second click at same button the motor will stop. Same to the other button, just in opposite direction.
3.3 Calculations 
3.3.1 Two-Blade Propeller Thrust Equation (ppt) calculation
The pitch of propeller is 1.462 in and the diameter is 5 in. Revolutions per minute(RPM) of each propeller is about 42000 rpm and the initial velocity(V0) is 0 in/s.

From above equation, we have the max force 11.08N, or 1.131kg of thrust.
