====================================
Lab 1: The Artemis Board and Bluetooth
====================================

:Author: Nita Kattimani
:Course: Fast Robots ECE 4160
:Date: 02/05/2025
:Lab Number: 1
:Lab Title: The Artemis Board and Bluetooth

.. contents::
    :depth: 2
    :local:

1. Prelab
----------

### Setup

Briefly describe the steps you took to set up your computer, including installing the required tools and configuring your environment.

- **Arduino IDE setup:** 
- **Virtual environment:**  
- **Python version:**  
- **MAC address output:** (Provide any relevant output/screenshots.)

Example:

.. code-block:: console

    Artemis Board MAC Address: C0:C2:8A:89:98:08

### Codebase Overview

Explain your understanding of the provided codebase. Focus on the role of BLE, key files, and classes.

- **Key files:** `ble_arduino.ino`, `base_ble.py`, `cmd_types.py`
- **Classes:** `BLECStringCharacteristic`, `RobotCommand`
- **Bluetooth overview:** Provide a summary of how communication is established between the Artemis and the computer.

2. Lab Tasks
------------

### Configurations

Describe any changes made to configurations such as the MAC address, UUIDs, and YAML files.

- **MAC Address:** Updated in `connections.yaml`
- **UUIDs:** Provide your generated UUIDs and where they were updated.

.. code-block:: python

    # Generated UUID example
    BLE_UUID_TEST_SERVICE = "9A48ECBA-2E92-082F-C079-9E75AAE428B1"

### Task 1: ECHO Command

Describe what you did to send and receive string values. Include results, screenshots, or output.

- **Steps:** (Briefly explain the steps)
- **Results:** (Provide outputs such as screenshots of the Jupyter terminal)

Example result:

.. code-block:: console

    Sent: "HiHello"
    Received: "Robot says -> HiHello :)"

### Task 2: Sending and Receiving Floats

Explain the process of sending and extracting float values on the Artemis.

- **Steps:** 
- **Results:** 

.. code-block:: console

    Float values received: 1.23, 4.56, 7.89

### Task 3: GET_TIME_MILLIS Command

- **Steps:** 
- **Results:** Timestamped string example:

.. code-block:: console

    Received: "T:123456"

### Notification Handler and Data Rate Analysis

Explain how you measured the data transfer rate using the notification handler.

- **Data transfer rate:**  
- **Time samples:** (Provide sample output.)

.. code-block:: console

    Time samples collected: [123456, 123789, 124123, ...]

- **Effective data rate:** (Provide your calculations and a brief discussion.)

### Array Storage and Temperature Readings

- **Array setup:** Describe how you stored time stamps and temperature readings.
- **Command:** Explain the process of adding the `SEND_TIME_DATA` and `GET_TEMP_READINGS` commands.
- **Results:** Show how you parsed the data in Python.

### Comparison of Methods

- **Differences:** Compare the two methods of transmitting data.
- **Advantages and disadvantages:** Discuss scenarios where each method might be preferable.
- **Storage:** Calculate how much data the Artemis board can store (RAM: 384 kB).

4. Discussion
-------------

- **What you learned:** Summarize key takeaways from the lab.
- **Challenges:** Explain any issues you faced and how you solved them.
- **Unique solutions:** Describe any novel approaches you used.

5. Conclusion
-------------

Provide a brief conclusion that summarizes your overall experience with Lab 1.

6. References (if applicable)
-----------------------------

List any external references, tutorials, or documentation that you used.

Appendix (Optional)
-------------------

- Include any additional information, such as large code snippets, logs, or extended results.
