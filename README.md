# IoT Smart Campus Network: Data Aggregator and Visualization

**Project Name:** CN\_PROJECT\_IoTNet\_DataAggregator
**Subject:** Computer Networks / IoT

## Project Overview

This repository contains the source code and documentation for the Smart Campus IoT Network. The system monitors critical parameters including **Temperature, Humidity, CO2 levels, Noise, Light intensity, and Room Occupancy** across multiple zones (Classrooms and Laboratories).

The project demonstrates a full-stack IoT implementation, featuring a Python-based sensor simulation layer, an MQTT transmission protocol, and a sophisticated Node-RED dashboard for real-time analytics and monitoring.


## System Architecture

The system operates on a Publisher-Subscriber model:

1.  **Data Generation:** The Python script generates synthetic data.
2.  **Transmission:** Data is serialized into JSON and published via MQTT to the **Node-RED embedded broker** under specific topics.
3.  **Visualization & Storage:** Node-RED subscribes, processes the payloads for real-time charts and filtering, and persists all raw data into MongoDB.

## Key Features

* **Advanced User Interface:** Custom-built "Glassmorphism" interface with professional industrial aesthetic.
* **Smart Filtering:** Global dropdown menu allows filtering the entire dashboard view (gauges, charts, status) to a single selected room.
* **Data Persistence:** Sensor data is permanently stored in MongoDB.
* **Real-Time Analytics:** Line charts visualize trends; bar charts track occupancy.
* **Data Logging (History Log):** A custom HTML-based table provides a **transparent, auto-scrolling log** (History Log Manager) of the 20 most recent sensor updates, complete with granular timestamps.

## Technology Stack

* **Runtime Environment:** Node.js
* **Integration Tool:** Node-RED
* **Database:** MongoDB
* **Scripting Language:** Python
* **Communication Protocol:** MQTT

***

## Project Structure

| Folder | Contents | Description |
| :--- | :--- | :--- |
| `dashboard_frontend` | `flows.json` | The final Node-RED flow configuration (Logic, Dashboard, MongoDB connection). |
| `database_config` | `mongo_db_config.txt` | Documentation detailing the MongoDB connection configuration. |
| `data_aquisition` | `sensor_simulator_data.py`, `requirements.txt` | Python scripts for sensor simulation and dependency listing. |

## Installation and Execution Guide

### Prerequisites

* Node.js (for Node-RED)
* Python 3.x
* MongoDB (`mongod` and `mongosh` commands accessible)
* Node-RED and necessary palettes installed (`node-red-dashboard`, `node-red-node-mongodb`, etc.)

### Step 1: Start MongoDB Database

1.  Open a Command Prompt or Terminal.
2.  Start the MongoDB server:
    ```bash
    mongod
    ```
3.  Minimize this window. The server is now running.

### Step 2: Start Node-RED and Load Flow

1.  Open a **new** Command Prompt or Terminal.
2.  Run Node-RED:
    ```bash
    node-red
    ```
3.  Node-RED Editor URL: **[http://localhost:1880/](http://localhost:1880/)**
4.  If needed, import the final flow file: **Menu > Import > Select File** and choose `dashboard_frontend/flows.json`.
5.  Click **Deploy**.

### Step 3: Start the Sensor Simulator

1.  Open a **new** Command Prompt or Terminal.
2.  **Navigate** to the simulator directory (your local path):
    ```bash
    cd C:\Users\Hina\CN_PROJECT_IoTNet_DataAggregator\data_aquisition
    ```
3.  Run the simulation script:
    ```bash
    python sensor_simulator_data.py
    ```

### Step 4: Access the Dashboard UI

Open your browser to view the live interface:

* **Live Dashboard UI:** **[http://localhost:1880/ui](http://localhost:1880/ui)**

## Database Verification

Use the following commands in a separate `mongosh` session to verify that data is being logged by Node-RED (assuming your database name is `campus`):

| Action | Command |
| :--- | :--- |
| **Start `mongosh`** | `mongosh` |
| **Select Database** | `use campus` |
| **View all Collections** | `show collections` |
| **View Data Samples** | `db.<Your_Collection_Name>.find().limit(5)` |