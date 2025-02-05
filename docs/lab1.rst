====================================
Lab 1: The Artemis Board and Bluetooth
====================================

.. contents::
    :depth: 2
    :local:

Lab Overview
============

### Part 1  
This part tests the connection between the Artemis board and the computer. The Arduino IDE was installed, and tasks were completed to verify the Artemis board's functionality.

Prelab
------

- **Installed:** Arduino IDE 2.2.1
- **Materials:**
  - SparkFun RedBoard Artemis Nano  
  - USB-C to USB-C cable  
  - Arduino IDE  
  - Better Serial Plotter (for Task 4)

Lab Tasks: Part 1A
==================

### Task 1 & 2: Example - Blink It Up

The Artemis board was connected to the computer using the SparkFun Apollo3 Boards package installed via Arduino IDE's Boards Manager.

Example code used: `File -> Examples -> 01.Basics -> Blink`

- A loop was implemented to turn the board LED on for 1 second, then off for 1 second using `digitalWrite()`.

.. image:: <path/to/board-manager-image>
    :alt: Arduino IDE Board Manager

.. code-block:: arduino

    // Code for Blink Task
    void loop() {
        digitalWrite(LED_BUILTIN, HIGH);
        delay(1000);
        digitalWrite(LED_BUILTIN, LOW);
        delay(1000);
    }

---

### Task 3: Serial Communication (Example04_Serial)

The Artemis board's serial communication with the computer was tested.  
Example code: `File -> Examples -> Apollo3 -> Example04_Serial`.

- Outputs printed in the serial monitor:  
  "Hello", "This is the serial example", "Test 1", "Test 2", "Test 3".

.. image:: <path/to/serial-monitor-image>
    :alt: Serial Monitor Output

.. video:: <path/to/serial-video.mp4>
    :alt: Serial communication test video

---

### Task 4: Temperature Sensor Test (Example02_AnalogRead)

The Artemis board's temperature sensor was tested using the AnalogRead example.  
Example code: `File -> Examples -> Apollo3 -> Example02_AnalogRead`.

- Covering the sensor increased the temperature reading from ~32.3°C to ~33.4°C.

.. image:: <path/to/temp-test-image>
    :alt: Temperature sensor reading

- Various temperature readings were plotted using the Better Serial Plotter.

.. image:: <path/to/serial-plot-image>
    :alt: Temperature plot with Better Serial Plotter

---

### Task 5: Microphone Output Test

The microphone output was tested by speaking into the Artemis board's microphone.  
Example code: `File -> Examples -> PDM -> Example1_MicrophoneOutput`.

- Speaking into the microphone changed the frequency readings.

.. image:: <path/to/mic-output-image>
    :alt: Microphone output test

.. video:: <path/to/mic-test-video.mp4>
    :alt: Microphone frequency test video

---

Discussion for Part 1
----------------------

- The connection between the Artemis board and the computer was tested.
- Tasks included turning on/off an LED, printing serial monitor outputs, viewing temperature data, testing the microphone, and creating a musical tuner.

Lab Tasks: Part 1B
==================

This part tests **Bluetooth communication** between the Artemis board and the computer.

Prelab: Setup
-------------

- Installed Python 3 and pip
- Created project folder: “MAE 5190 Lab”
- Created virtual environment:

.. code-block:: console

    python3 -m venv FastRobots_ble

- Activated and deactivated the virtual environment:

.. code-block:: console

    source FastRobots_ble/bin/activate
    deactivate

- Installed Python packages:

.. code-block:: console

    pip install numpy pyyaml colorama nest_asyncio bleak jupyterlab

- Installed additional packages with TA assistance (e.g., matplotlib).

.. image:: <path/to/cli-setup-image>
    :alt: CLI setup screenshot

---

Prelab: Codebase Setup
-----------------------

- Installed provided codebase in the project directory
- Copied the “ble_python” directory into the project folder
- Opened Jupyter Notebook:

.. code-block:: console

    jupyter lab

- Configured Bluetooth communication by updating:
    - MAC address in `connection.yaml`
    - UUIDs generated in `demo.ipynb`

.. image:: <path/to/uuid-generation-image>
    :alt: UUID generation in Jupyter Notebook

Lab Tasks: Bluetooth Communication
-----------------------------------

### Task 1: ECHO Command

Sent a string value to the Artemis board and received an augmented string back.

---

### Task 2: GET_TIME_MILLIS Command

Added a command to return the current time string from the Artemis board.

---

### Task 3: Notification Handler

Created a Python handler to process string notifications from the Artemis board.

---

### Task 4: Current Time Loop

Implemented a loop to send timestamps to the computer. Measured data transfer rate.

---

### Task 5: SEND_TIME_DATA Command

Stored timestamps in an array and sent them as a batch. Measured data transfer rate.

---

### Task 6: GET_TEMP_READINGS Command

Added a second array for temperature readings. Synchronized time and temperature data.

---

### Task 7: Discussion for Tasks 4 and 5

- Comparison of individual vs. array-based data transfer rates.
- Advantages/disadvantages of each method.
- Memory considerations for Artemis board.

---

Discussion for Part 2
----------------------

- Learned how to use Bluetooth communication and UUIDs.
- Experienced minimal issues connecting to Bluetooth.

Lab 1 References
================

Thank you to the TAs and references to past
