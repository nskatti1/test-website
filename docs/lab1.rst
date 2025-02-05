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

Part B
-----------------------------------

This part tests **Bluetooth communication** between the Artemis board and the computer.

### Task 1: ECHO Command

The first task involved sending a string from the computer to the Artemis board using the `ECHO` command. The Artemis board receives the string, augments it, and sends it back.

**Code for the ECHO command:**

.. code-block:: c++

    case ECHO:
        char char_arr[MAX_MSG_SIZE];
        if (robot_cmd.get_next_value(char_arr)) {
            tx_estring_value.clear();
            tx_estring_value.append(char_arr);
            tx_characteristic_string.writeValue(tx_estring_value.c_str());
            Serial.print("Robot says -> ");
            Serial.println(tx_estring_value.c_str());
        }
        break;

Example response in the serial monitor:  
`Robot says -> HiHello :)`

---

### Task 2: SEND_THREE_FLOATS Command

The second task required sending three float values from the computer to the Artemis board. The board extracts these floats and prints them.

**Code for extracting and printing three floats:**

.. code-block:: c++

    case SEND_THREE_FLOATS:
        float float_a, float_b, float_c;
        if (robot_cmd.get_next_value(float_a) &&
            robot_cmd.get_next_value(float_b) &&
            robot_cmd.get_next_value(float_c)) {
            Serial.print("Three Floats: ");
            Serial.print(float_a);
            Serial.print(", ");
            Serial.print(float_b);
            Serial.print(", ");
            Serial.println(float_c);
        }
        break;

---

### Task 3: GET_TIME_MILLIS Command

The `GET_TIME_MILLIS` command makes the Artemis board reply with the current time in milliseconds as a string.

**Code for GET_TIME_MILLIS:**

.. code-block:: c++

    case GET_TIME_MILLIS:
        tx_estring_value.clear();
        tx_estring_value.append("Time: ");
        tx_estring_value.append((double)millis());
        tx_characteristic_string.writeValue(tx_estring_value.c_str());
        Serial.println(tx_estring_value.c_str());
        break;

Example output: `Time: 123456`

---

### Task 4: Time Data Loop (GET_TIME_MILLIS_LOOP)

In this task, the Artemis board sends the current time repeatedly in a loop for a few seconds. This helps determine the data transfer rate.

**Code for looping time data:**

.. code-block:: c++

    case GET_TIME_MILLIS_LOOP:
        double t = (double) millis();
        while ((double)millis() - t < 1000) {
            tx_estring_value.clear();
            tx_estring_value.append("Time: ");
            tx_estring_value.append((double)millis());
            tx_characteristic_string.writeValue(tx_estring_value.c_str());
        }
        break;

---

### Task 5: SEND_TIME_DATA Command

In this task, the board stores timestamps in an array and sends the array to the computer. The array is defined globally so it can be accessed across functions.

**Code for storing and sending time data:**

.. code-block:: c++

    case SEND_TIME_DATA:
        float time_array[20];
        for (int i = 0; i < 20; i++) {
            time_array[i] = (float)millis();
        }
        for (int i = 0; i < 20; i++) {
            tx_estring_value.clear();
            tx_estring_value.append("Time: ");
            tx_estring_value.append(time_array[i]);
            tx_characteristic_string.writeValue(tx_estring_value.c_str());
        }
        break;

---

### Task 6: GET_TEMP_READINGS Command

The final task added a second array to store temperature readings alongside timestamps. The board sends both arrays, and each timestamp corresponds to a temperature reading.

**Code for GET_TEMP_READINGS:**

.. code-block:: c++

    case GET_TEMP_READINGS:
        float time_array[20], temp_array[20];
        for (int i = 0; i < 20; i++) {
            time_array[i] = (float)millis();
            temp_array[i] = getTempDegF();  // Example function to get temperature
        }
        for (int i = 0; i < 20; i++) {
            tx_estring_value.clear();
            tx_estring_value.append("Time: ");
            tx_estring_value.append(time_array[i]);
            tx_estring_value.append("s Temp: ");
            tx_estring_value.append(temp_array[i]);
            tx_estring_value.append(" degrees");
            tx_characteristic_string.writeValue(tx_estring_value.c_str());
        }
        break;

**Note:** The `getTempDegF()` function retrieves the current temperature reading from the Artemis board.

---

### Task 7: Discussion on Data Methods

The method used in Task 4 sends data individually, while Task 5 sends data in arrays. The array-based method has a higher data transfer rate but uses more memory on the Artemis board.

- **Advantages of Task 4:**  
  - Lower memory usage on the Artemis board.
  
- **Advantages of Task 5:**  
  - Faster data transfer rates.

The Artemis board has 384 kB of RAM. Calculations should be done to determine how much data can be stored based on sampling frequency and data size.


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
