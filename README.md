// File: ConveyorSystem.ST
// Description: PLC program simulating an industrial conveyor system with sensors and actuators

PROGRAM ConveyorSystem
VAR
    // Input Signals
    StartButton : BOOL;             // Start conveyor
    StopButton : BOOL;              // Stop conveyor
    ItemDetected : BOOL;            // Sensor detects an item
    DiverterCondition : BOOL;       // Condition for diverting (e.g., weight)

    // Internal Variables
    ConveyorRunning : BOOL := FALSE; // Internal flag for conveyor state
    ItemReadyToDivert : BOOL := FALSE; // Tracks if item is ready for diverter

    // Output Signals
    ConveyorMotor : BOOL;           // Motor to drive the conveyor
    Diverter : BOOL;                // Diverter actuator
END_VAR

// Main program logic
IF StartButton THEN
    ConveyorRunning := TRUE; // Start the conveyor
END_IF;

IF StopButton THEN
    ConveyorRunning := FALSE; // Stop the conveyor
END_IF;

// Control conveyor motor
ConveyorMotor := ConveyorRunning;

// Detect item and manage diverter
IF ItemDetected AND ConveyorRunning THEN
    // Item is detected and ready for diversion
    ItemReadyToDivert := TRUE;
END_IF;

// Activate diverter if conditions are met
IF ItemReadyToDivert AND DiverterCondition THEN
    Diverter := TRUE; // Activate the diverter
    ItemReadyToDivert := FALSE; // Reset after diversion
ELSE
    Diverter := FALSE; // Deactivate diverter
END_IF;
END_PROGRAM
