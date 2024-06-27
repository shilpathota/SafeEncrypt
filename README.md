# SafeEncrypt
This Project focuses on Some Services and how the encryption mechanisms can be leveraged to enhance the security of the services

## Table Of Contents
1.	Introduction
2.	Functional Specifications
3.	Use Case Diagram
4.	Activity Diagram
5.	Sequence Diagram
6.	Class Diagram
7.	Object Diagram
8.	Programming Environment and Tools
9.	Code
10.	Results of the Project
11.	Issues to Future Studies
12.	Conclusion
13.	References
14.	Appendix

## Introduction:
In today's digital age, data security is of paramount importance. With the ever-increasing amount of sensitive data being exchanged between services and stored in databases, it is essential to ensure that this data remains confidential and secure. This is even more critical in Banking Services. This project proposal outlines the development of a robust and intelligent data encryption and validation service for enhancing data security in various software applications.<br>
The project will encompass the following key components:
-	Implement robust encryption techniques for securing sensitive data during transmission and storage which includes 
o	Salt Hashing Technique
o	Cipher Encryption of Advanced Encryption Standard
o	Exchange Mapping Technique
And develop decryption mechanism for authorized access
-	Monitor each service interaction, scan request - response and detect the sensitive data based on the predefined flags in database
-	Integrate with the custom logic into encryption and decryption process to add extra layer of security like tokenization or data masking
-	Ensure that the service can be seamlessly integrated into existing software architectures and is scalable to handle increased data traffic.
-	Develop a validation system to ensure that all data exchanged adheres to predefined security standards and policies. This includes data type validation, length checks, and security compliance.
-	Stores and retrieves the sensitive data like passwords in Tool Harshicorp Vault which can be accessed only from integrations like GitHub
## Why is this service important?
In Banking applications, where there are lot of sensitive and restricted data like SSN, Date Of Birth, Account Number etc., This service plays crucial role in monitoring the application which has more than 100 services and each being independent and provides request and responses to every other service.
This project aims to address the critical need for data security by creating a Secure Data Encryption and Validation Service. By automatically detecting sensitive data, applying robust encryption, and integrating custom security logic, this service will significantly enhance data 
A validation system will be developed to ensure that all exchanged data adheres to predefined security standards and policies. This includes rigorous data type validation, length checks, and compliance with security protocols. The proposed service addresses the critical need for data security by automating the detection of sensitive information, applying robust encryption, and integrating custom security logic. This project is positioned to be a valuable asset for organizations seeking to fortify their sensitive information and comply with stringent data protection regulations.<br>

## Functional Specifications:
<table><tr><th>
Controller</th>	<th>Method</th>	<th>Endpoint	</th><th>Functionality</th>	<th>Behavior</th></tr>
<tr>Sensitive Data Detection	<td>POST</td>	/sensitive-data/scan	Scans data for sensitive information	Analyzes request payload for sensitive data patterns, generates alerts, and returns results.</tr>
<tr>Security Validation	POST	/security-validation/validate-data	Validates data for security compliance	Applies data type validation, length checks, and other security compliance checks, returns validation result.</tr>
<tr>Custom Logic Encryption	POST	/custom-encryption/hash-password	Hashes a password for secure storage	Accepts a password, applies one-way hashing algorithm, and returns hashed password.</tr>
<tr>Custom Logic Encryption	POST	/custom-encryption/exchange-mapping	Applies exchange mapping to data	Accepts data, applies exchange mapping, and returns mapped data.</tr>
<tr>Custom Logic Encryption	POST	/custom-encryption/compare-password	Compares original and hashed passwords	Accepts original and hashed passwords, compares them, and returns the result.</tr>
<tr>Custom Logic Encryption	POST	/custom-encryption/aes-encrypt	Encrypts data using AES	Accepts data, applies AES encryption, and returns encrypted data.</tr>
<tr>Custom Logic Encryption	POST	/custom-encryption/aes-decrypt	Decrypts data using AES	Accepts encrypted data, applies AES decryption, and returns decrypted data.</tr>
<tr>Admin	POST	/admin/rotate-key	Rotates encryption keys for security	Accepts parameters for key rotation, initiates rotation, and returns success or failure.</tr>
<tr>Monitoring	GET	/monitoring/metrics	Provides application metrics	Retrieves and returns various metrics data.</tr>
<tr>Monitoring	GET	/monitoring/info	Offers general information about the app	Retrieves and returns general information.</tr>
<tr>Monitoring	GET	/monitoring/health	Checks and reports overall health status	Conducts health checks, returns overall health status.</tr></table><br>
<i>Table 2.1 – Functional Specifications</i>
## Use Case Diagram
### Description:
Actor – The Client or the service which calls this service is an actor who does the request<br>
The Actor Interacts with the Security Config to get the authentication based on the role he is assigned for interacting with the other services<br>
The Client requests the Encryption of data with Exchange mapping to get the complex algorithm set as security for his data and he gets the encrypted text<br>
The client requests the encryption of data which he might decrypt in the other interactions which uses vault to get the secret key<br>
The Client interacts with the system with the encrypted data to decrypt the data and use in his flow which uses vault to get the encryption key<br>
The client interacts with the application with the compare password endpoint to validate if the entered endpoint is as expected which uses vault to get the encryption key<br>
The client asks to rotate key if he is the admin and wants to change the key on regular basis and updates the vaul<br>
The Client request for scanning of the sensitive data which in turn calls the sensitive data scanner to help with the operation and get the scan done for his data<br>
 The Client requests for Validate data for the data provided if it meets the compliance requirement and uses the validator to validate if they meet customized criteria<br>
The client requests for the Monitoring application which in turn calls the actuator to get the data for respective endpoints<br>
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/b6603145-4b4a-416e-9bb3-e33b1abd1142)

<i>Fig 3.1 – Use Case Diagram</i><br>
## Activity Diagram:
The Activity Diagram has the client which requests the controllers based on the operation client performs and gets the response<br>
The request is made by the client to the Monitoring application controller layer which in turn calls the service layer to determine the actuator response and then form the response to be given to the client and gives the response<br>
The request for compare password is made which checks the encryption key and gets the hashing done for the provided text and returns if the comparison is true or false<br>
The Request to encrypt the data is performed which calls the vault to get the encryption key and then perform the algorithm to encrypt and provides the response<br>
The request to rotate the key is made which updates the new key to the vault and returns the success response<br>
The request to scan the sensitive data is made and the call is made to the scanner to validate against the patterns which sends the response as sensitive data found or not found<br>
The Request to validate the data for compliance is made and it uses the validators to check for the compliance and the response as the data is valid or invalid is sent as the decision<br>
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/2c1262f1-ce60-4412-9780-63cbdb5999fe)

<i>Fig 4.1 – Activity Diagram</i><br>
## Sequence Diagram:
The Sequence Diagram represents the actor who is the client starts the interaction by interacting with Security Config for authentication for Login and use the authentication to determine the role if he gets the success response he can access role related endpoints<br>
The Client reaches to the Admin controller with the rotateKey() method with the new key in his request body and it in turn updates the vault data using the getter and setter method<br>
The Client reaches the CustomLogic Encryption Controller with multiple operations as hashPassword() which hashes his text and provides him the hashed text<br>
The client interacts with the CustomLogic Encryption Controller asking to comparePassword() which returns the Boolean value<br>
The client also sends the string to the encrypted with aesEncrypt() which returns the encrypted string<br>
The client sends the encrypted text to aesDecrypt() which returns the decrypted text<br>
The client calls the exchangeMapping() for the interaction with the controller to perform powerful encryption and it returns him the encrypted text which cannot be decrypted<br>
The client monitors the application using the getHealth() which returns the Health Object of the application<br>
The Client monitors the application using the getMetrics() which returns the Metrics Object<br>
The client requests for the information about the application using getInfo() which returns the info object<br>
The Client requests for scanForSensitiveData() by providing the data to be scanned and it calls the findSensitiveData() which executes the logic and determine if the sensitive data and gives the list of sensitive Data that is found<br>
The client requests for Security Validation Controller to validateData() and it checks with the validator to determine if the data object is valid or invalid<br>
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/6195819c-2148-4523-ac19-c8150e74dddb)

<i>Fig 5.1 – Sequence Diagram</i><br>
## Class Diagram:
The Class diagram shows the Security Config Class which is the Configuration class and is annotated with @Configuration and it has methods for loading the user data and configuring the security configurations<br>
The controllers uses Security config to determine if the request is of valid user<br>
The SensitiveDataDetectionController is the controller class which exposes scan endpoint for the method scanForSensitiveData which includes the SensitiveDataScanner to determine if the data matches the sensitive information and it uses 2 methods containsSensitiveData and findSensitiveData which has the constant that gives list of patterns to check in the data<br>
The SecurityValidationController has the method validateData() to validate if the SecurityData Object passed by the user is compliant with the validators ValidNameValidator and ValidPasswordValidator which uses customized annotations<br>
The monitoringController uses the Actuator endpoints to get the health, metrics and info of the application to determine the status of the application using the methods getHealth(), getInfo() and getMetrics()<br>
The CustomLogicEncryptioncontroller has the methods hashPassword() that returns string that is hashed, comparePassword() which takes 2 arguments and compare the hashed password with the password entered by the user. The aesEncrypt() encrypts the string and gives the encrypted string. The encrypted string is passed and decrypted using aesDecrypt(). The exchangeMapping() uses the secret key algorithm and complex algorithm to convert the string sent and this cannot be reversed and is used for sensitive data
The AdminController uses the rotateKey() which gives previliges to the admin user to rotate the key and send to the vault<br>
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/dcf0039a-6c3f-4f3c-8e9f-40ed7c4210e0)

<i>Fig 6.1 – Class Diagram</i> <br>
## Object Diagram:
In this Object Diagram, the Security Validation controller uses the Security Data object to get the request mapped to the object and respective fields are validated against the annotations provided in securityData object
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/bf2f72b1-af8a-4ee3-beb6-ef6f195b1f39)

<i>Fig 7.1 – Object Diagram</i><br>

## Programming Environment and Tools:
<table>
<tr><th>
Tools/ Technologies</th><th>	Type</th>	<th>Version</th></tr>
<tr><td>Java</td><td>	Programming Language</td>	<td>17</td></tr>
<tr><td>Maven	</td><td>Build Tool</td>	<td>3.9.5</td></tr>
<tr><td>Eclipse</td><td>	IDE</td>	<td>2023-06</td></tr>
<tr><td>Harshicorp Vault</td><td>	Software</td>	<td>1.15.2</td></tr>
<tr><td>Spring Boot	</td><td>Framework</td>	<td>3.1.5</td></tr>
<tr><td>Swagger	</td><td>UI/Documentation</td>	<td>2.0.2</td></tr>
  </table><br>
<i>Table 8.1 – Tools and Technologies</i>

### Code:
This is the project Structure
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/2bd683ea-4db1-47a6-b4fd-db153395e1ef)

<i>Fig 9.1 – Project Structure</i><br>

#### 1.	com.secure.safe/SafeEncrypt/src/main/java/com/secure/safe/SafeEncryptApplication.java
•	This is the main application class, often referred to as the entry point of the application.<br>
•	It contains the main method to bootstrap the application.<br>
•	It initializes the Spring application context and kicks off the application.<br>
#### 2.	com.secure.safe.configuration/Securityconfig.java:
•	This class is responsible for configuring security settings for the application.<br>
•	It include settings related to authentication, authorization, and other security-related configurations.<br>
#### 3.	com.secure.safe.configuration/VaultData.java:
•	This class is used for handling interactions with HashiCorp Vault.<br>
•	It contain methods for storing and retrieving sensitive data securely from the vault.<br>
#### 4.	com.secure.safe.controller/AdminController.java:
•	This controller class is responsible for handling requests related to administrative tasks.<br>
•	It  include endpoints for rotating the keys which uses the Admin secvice for the operations<br>
#### 5.	com.secure.safe.controller/CustomLogicEncryptionController.java:
•	This controller is involved in managing custom logic related to data encryption.<br>
•	It handle requests for applying additional encryption or security measures beyond standard techniques.<br>
•	It also handles requests for hashing the password, Comparing the password, Exchange Mapping technique using secret key obtained from vault<br>
#### 6.	com.secure.safe.controller/MonitoringController.java:
•	This controller is dedicated to handling requests related to monitoring the application.<br>
•	It include endpoints for Health, Info and Metrics which in turn calls the actuator for getting the details<br>
#### 7.	com.secure.safe.controller/SecurityValidationController.java:
•	This controller class is responsible for validating security-related aspects of the application.<br>
•	It contain endpoints for validating user input, ensuring compliance with security standards, etc.<br>
•	This uses the Validators for Name and Password validations <br>
#### 8.	com.secure.safe.controller/SensitiveDataDetectionController.java:
•	This controller is focused on detecting sensitive data within the application.<br>
•	It include endpoints for scanning and identifying sensitive information based on predefined criteria.<br>
•	It uses the SensitiveDataScanner to perform these operations<br>
#### 9.	com.secure.safe.service/AdminService.java:
•	This service class contains business logic related to administrative tasks.<br>
•	It handles user management, role assignments, or other administrative functionalities.<br>
#### 10.	com.secure.safe.service/CustomUserDetailsService.java:
•	This service class is responsible for providing custom user details for authentication purposes.<br>
•	It implement the UserDetailsService interface and override methods to load user details.<br>
•	Here we are using the basic User and Admin <br>
#### 11.	com.secure.safe.util/PasswordComparisonRequest.java:
•	This utility class represent a request object for comparing passwords.<br>
•	It contain fields representing the passwords to be compared.<br>
#### 12.	com.secure.safe.util/SecurityData.java:
•	This utility class store the Object and the variables related to the application Validation endpoint.<br>
#### 13.	com.secure.safe.util/SensitiveDataScanner.java:
•	This utility class is responsible for scanning data for sensitive information based on predefined rules and patterns<br>
#### 14.	com.secure.safe.util/ValidName.java:
•	This utility class represent an annotation for validating a valid name.<br>
#### 15.	com.secure.safe.util/ValidPassword.java:
•	This utility class represent an annotation for validating a secure password.<br>
#### 16.	com.secure.safe.validators/ValidNameValidator.java:
•	This class is a validator for ensuring that a given name is valid according to predefined criteria.<br>
#### 17.	com.secure.safe.validators/ValidPasswordValidator.java:
•	This class be a validator for ensuring that a given password is secure according to predefined criteria.<br>
#### 18.	/SafeEncrypt/src/main/resources:
•	This directory typically contains application configuration files.<br>
•	application.properties and bootstrap.properties store configuration settings for the application related to server port, vault configuration and Log configuration<br>

## Project Output:
Here are the screenshots of the application which uses swagger for UI of the services
## Sensitive Data Controller- 
### Scan – 
This endpoint is exposed and is used by the users/ client to scan the data for sensitive information. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/edb0e1df-b472-4df1-8c9d-9a92cc08081e)

<i>Fig 10.1 – Swagger UI - Scan Endpoint</i><br>
## Security Validation Controller
### Validate Data – 
This endpoint is exposed and is used by the users/ client to validate the data for any deviations from the compliance. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>
![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/a07d7b7c-fcd7-4848-9026-406a5ca07c85)

 
<i>Fig 10.2 – Swagger UI – Validate Data Endpoint</i><br>
Custom Logic Encryption Controller:
## Exchange Mapping – 
This endpoint is exposed and is used by the users/ client to encrypt the sensitive information which cannot be decrypted. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>
 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/2c95eb97-04a5-4c3f-87a8-18faa1063773)

<i>Fig 10.3 – Swagger UI – Exchange Mapping Endpoint</i><br>
## Hash Password – 
This endpoint is exposed and is used by the users/ client to hash the password to further store it. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>
![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/61f0186a-48fb-4b8d-a16a-9fca54241799)

 
<i>Fig 10.4 – Swagger UI – Hash Password Endpoint</i><br>
## Compare Password-
This endpoint is exposed and is used by the users/ client to compare the password with the encrypted password using encryption. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>
![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/a85c76a4-2bb0-4b17-8839-414cdacf00a1)

 
<i>Fig 10.5 – Swagger UI – Compare Password Endpoint</i><br>
## AES Encrypt – 
This endpoint is exposed and is used by the users/ client to perform encryption using AES technique. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>

 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/ee0601c9-162e-4e4e-b641-6995e0f6ebe3)

<i>Fig 10.6 – Swagger UI – AES Encrypt Endpoint</i><br>
## AES Decrypt – 
This endpoint is exposed and is used by the users/ client to perform decryption using AES technique. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>

 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/08450e2b-32fa-4f0f-b3e7-837e6b6057ee)

<i>Fig 10.7 – Swagger UI – AES Decrypt Endpoint</i><br>
## Admin Controller – 
Rotate Key – <br>
This endpoint is exposed and is used by the admins/ client to rotate the key and store in vault. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>

![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/86734b9e-237e-409c-bb9f-87912880bc29)
 
<i>Fig 10.8 – Swagger UI – Rotate Key Endpoint</i><br>
## Monitoring Controller – 
### Metrics Endpoint– 
This endpoint is exposed and is used by the users/ client to get the metrics information of the application. 
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>
![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/69bec50c-ff58-45ab-9a47-48353df732d3)

 
<i>Fig 10.9 – Swagger UI - Metrics Endpoint</i>
### Info Endpoint – 
This endpoint is exposed and is used by the users/ client to get the Info of the application<br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>
![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/c02efb8c-074b-443a-bb62-9d55eca832b6)

 
<i>Fig 10.10 – Swagger UI - Info Endpoint</i>
### Health Endpoint – 
This endpoint is exposed and is used by the users/ client get the health information of the application and the tools it is integrated with. <br>
<b>Request Type: </b>POST<br>
<b>Response Type:</b> String<br>
<b>Response Status Codes :</b><br>
200 -  Success<br>
500 – Internal Server Error<br>
400 – Bad Request<br>

 ![image](https://github.com/shilpathota/SafeEncrypt/assets/36531617/daea478a-278a-4c5e-8710-1a2f4e27805c)

<i>Fig 10.11 – Swagger UI - Health Endpoint</i>
## Issues to Future Studies
•	Leveraged to run on a high available system using multiple instances and pods and auto scaling enabled as this is a critical service used by all the services
•	Admin functions can be leveraged based on the use cases and enable Role based authentication System and Oauth2.0
•	The service to be implemented across organizations by leveraging it with all the customized scanning capabilities added

