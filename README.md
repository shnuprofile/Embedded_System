# CS-350 Emerging Systems Architectures and Technologies - Portfolio

## Selected Artifacts

1. **Thermostat.py** - Smart Thermostat System
2. **Milestone3.py** - Morse Code Transmitter

---

## Reflection Questions

### Summarize the project and what problem it was solving.

**Thermostat.py** implements a fully functional smart thermostat system using a Raspberry Pi. The project solves the problem of environmental temperature control by reading room temperature via an I2C sensor, allowing users to set desired temperatures through physical buttons, and providing visual feedback through LEDs that indicate whether the system is actively heating or cooling. The system also simulates IoT connectivity by transmitting status data over UART to a hypothetical server, demonstrating how embedded devices communicate in real-world smart home applications.

**Milestone3.py** implements a Morse code transmission system that converts text messages into visual signals using LEDs. The project solves the problem of encoding and transmitting information using standardized timing patterns. Users can toggle between two preset messages (SOS and OK) via a button press, and the system displays dots (red LED) and dashes (blue LED) with proper timing intervals according to Morse code standards.

### What did you do particularly well?

I excelled at implementing the state machine architecture in both projects. The `TemperatureMachine` class cleanly manages transitions between off, heat, and cool states with appropriate entry and exit actions for each state. Similarly, the `CWMachine` handles six distinct states (off, dot, dash, dotDashPause, letterPause, wordPause) with precise timing requirements.

I also did well with hardware abstraction and modular design. The `ManagedDisplay` class encapsulates all LCD functionality, making the display easy to use and properly cleaned up. The separation of concerns between the state machine logic, display management, and GPIO control makes the code organized and maintainable.

### Where could you improve?

Error handling could be more robust. Neither project includes try-catch blocks around hardware operations that could fail (like I2C communication or serial transmission). Adding graceful error recovery would make the systems more resilient in production environments.

I could also improve the configurability of both projects. Hard-coded values like GPIO pin numbers, timing constants, and default temperatures could be moved to a configuration file or class constants at the top of the file, making the code easier to adapt to different hardware configurations.

Additionally, unit testing is absent from both projects. Implementing mock hardware interfaces would allow testing the state machine logic independently from the physical hardware.

### What tools and/or resources are you adding to your support network?

- **GPIOZero Library**: A powerful abstraction for GPIO control that simplifies button handling and PWM LED control
- **Python StateMachine Library**: Enables clean implementation of finite state machines with declarative state definitions and transitions
- **Adafruit CircuitPython Libraries**: Specifically adafruit_ahtx0 for temperature sensors and adafruit_character_lcd for display control
- **PySerial**: For UART communication, essential for any project requiring serial data transmission
- **Raspberry Pi Documentation**: Hardware pinout references and peripheral configuration guides
- **Threading in Python**: For running concurrent operations like display updates while maintaining responsive button handling

### What skills from this project will be particularly transferable to other projects and/or course work?

- **State Machine Design**: The pattern of using finite state machines to manage complex system behavior is applicable to game development, UI design, network protocols, and any system with distinct operational modes
- **Hardware/Software Integration**: Understanding how to interface with sensors, displays, and communication peripherals is fundamental to IoT, robotics, and embedded systems development
- **Interrupt-Driven Programming**: Using button callbacks and event handlers rather than polling translates directly to GUI programming, web development, and real-time systems
- **Serial Communication Protocols**: Understanding UART, I2C, and their configuration parameters is essential for any embedded systems work
- **Concurrent Programming**: Managing multiple threads for display updates and main loop execution applies to any multi-threaded application development

### How did you make this project maintainable, readable, and adaptable?

**Maintainability:**
- Used descriptive variable and function names (e.g., `processTempIncButton`, `updateLights`, `setupSerialOutput`)
- Included a DEBUG flag to easily toggle verbose console output for troubleshooting
- Implemented proper cleanup methods (`cleanupDisplay`, keyboard interrupt handling) to ensure resources are released

**Readability:**
- Organized code into logical classes (`ManagedDisplay`, `TemperatureMachine`, `CWMachine`) that each handle a specific responsibility
- Added comprehensive header comments explaining the purpose and functionality of each file
- Used consistent formatting and spacing throughout the codebase
- Included inline comments explaining non-obvious logic, particularly around timing and state transitions

**Adaptability:**
- The `ManagedDisplay` class can be reused in any project requiring LCD output
- The state machine pattern allows easy addition of new states or modification of transition logic
- GPIO pin assignments are defined at the top level, making hardware reconfiguration straightforward
- The Morse code dictionary in Milestone3.py allows transmission of any alphanumeric message, not just the preset ones
- Temperature conversion logic is isolated in its own method, making it easy to support different sensor types or temperature scales
