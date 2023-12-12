# Temperature & Humidity Real-Time Data ![](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/screenshots/rpi-logo.png)


## Table of Contents
- [Temperature & Humidity Real-Time Data](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data#temperature--humidity-real-time-data-)
- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Hardware Components](#hardware-components)
- [Software Components](#software-components)
- [Workflow](#workflow)
- [Security and Microsoft Defender for Cloud](#security-and-microsoft-defender-for-cloud)

## Overview
The Raspberry Pi Temperature & Humidity Sensor project led me to turn the Raspberry Pi into a monitoring system. By connecting a temperature and humidity sensor to the Raspberry Pi, the project allows real-time data collection in the chosen environment.

The collected data is then transmitted to an IoT Hub, providing a secure solution for cloud-based storage. Additionally, the project includes a database to store the environmental data, enabling historical analysis and identification.

The true strength of this project lies in its ability to turn raw data into actionable insights. I chose to use Power Bi. With Power BI integration, I can visualize and analyze the temperature and humidity over time. With it, I create dynamic dashboards and reports that allow me to make informed decisions based on the environmental data collected by the Raspberry Pi. Raspberry Pi is a powerful tool when equipped with the right utilities.


## System Architecture
![](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/Diagram/Untitled%20Diagram.drawio%20(1).png)


## Hardware Components

- Raspberry Pi 3
- BME280 Sensor
- LED
![](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/screenshots/Screenshot%202023-12-05%20162941.png)

## Software Components
- Node.js Script for reading data from the BME280 sensor and transmitting it to the IoT Hub
- Azure IoT Hub for secure transfer of data from the Raspberry Pi to the cloud
- Azure Cosmos DB and Azure Storage for storing sensors data
- Azure Functions for processing data from Cosmos DB and IoT Hub
- Power BI Data dashboard

## Workflow
1. Data Collection:
   - 1.1 The BME280 sensor collects temperature and humidity data by interfacing with the the Raspberry Pi through the I2C bus. The BME280 is a sensor that combines temperature, humidity, and pressure sensing in a single device.
   - 1.2 The Node.js script initializes the sensor using the bme280-sensor library, reads sensor data at regular intervals, and constructs a JSON message containing the temperature and humidity values. This data collection process occurs in real-time, providing accurate and up-to-date environmental information.

2. Transmission to IoT Hub:   
   - 2.1 Azure IoT Hub Connection:
The script uses the azure-iot-device library to create an Azure IoT Hub client.
The Client.fromConnectionString function is used to establish a connection to the Azure IoT Hub using the provided connection string.
 ![](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/screenshots/Screenshot%202023-12-05%20164953.png)
 ![](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/screenshots/Screenshot%202023-12-05%20164642.png)
   - 2.2 Message Sending:
The sendMessage function is responsible for packaging the collected sensor data into an Azure IoT Hub message.
The client.sendEvent method sends the message to the Azure IoT Hub.
   ![](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/screenshots/Screenshot%202023-12-05%20165101.png)


   - 2.3 Temperature Alert:
If the temperature exceeds 30°C, a custom property temperatureAlert is added to the message, indicating a potential temperature alert.

   - 2.4 LED Indication:
The blinkLED function provides a visual indication by briefly lighting up an LED connected to the Raspberry Pi GPIO pin when a message is successfully sent.

   - 2.5 Interval Sending:
Messages are sent to Azure IoT Hub at regular intervals (every 15 seconds) using setInterval(sendMessage, 15000).

3. Database Storage:
   - 3.1  Database Storage with Azure Cosmos DB:
For this project, Azure Cosmos DB is used as the database to store sensor data. I have set up an Azure Cosmos DB account and created a new database along with a container (collection) to store the real-time environmental data.

   - 3.2  Database Storage with Azure Storage:
Azure Storage is a cloud-based storage solution provided by Microsoft Azure, one of the leading cloud computing platforms. Azure Storage offers a variety of storage services to meet the needs of different applications and scenarios. This is designed to store and manage unstructured data, such as documents, images, videos, and other binary data. Blobs are organized into containers, and each blob is assigned a unique URL.

4. Power BI Integration:
   ![](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/screenshots/Screenshot%202023-12-05%20171516.png)
   - 4.1 I leverage Power BI as my primary data visualization tool, seamlessly connecting it to Azure IoT Hub for real-time insights into the environmental data collected by the Raspberry Pi. With Power BI, I can effortlessly create interactive dashboards and reports that offer a comprehensive view of temperature and humidity trends over time. The live dashboards provide an instant overview, while customizable reports enable in-depth analysis of historical data. This integration not only simplifies data exploration but also enables quick decision-making based on the actionable insights derived from the intelligent room system. In summary, Power BI serves as a crucial component in transforming raw data into meaningful visualizations, providing a dynamic and interactive platform for monitoring and analyzing the performance of the Temperature & Humidity Monitoring System.


## Security and Microsoft Defender for Cloud

To ensuring the security of my IoT solution, I prioritize encrypted traffic for communications between the device and the cloud. The Azure IoT Hub secures communication, while Power BI interactions happen over encrypted channels. Sensitive information is stored using environmental variables, with consideration for Azure Key Vault.

Following to the "principle of least privilege", to restrict a user's administrator permissions by assigning least privileged roles in Microsoft Entra ID, permissions are minimal across Azure IoT Hub, Cosmos DB, and Azure Storage.

Additionally, I integrate Microsoft Defender for Cloud. Continuous Monitoring, identifying and responding to potential threats in real-time. Security Recommendations offering best practices for an enhanced security posture. Vulnerability Management, identifying and remediating vulnerabilities. Advanced Threat Protection using behavioral analytics for early risk mitigation. Integration with Azure Security Center to unify security management for enhanced visibility.

This project is licensed under the [Apache License](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data/blob/main/Apache%20License).

[(Go to top)](https://github.com/GoranMarjanovic90/Temperature-Humidity-Real-Time-Data#temperature--humidity-real-time-data-)
