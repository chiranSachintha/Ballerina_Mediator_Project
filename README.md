# Ballerina Mediator for Micro Integrator

This project provides a Ballerina language-based solution to integrate with Micro Integrator, serving as a class mediator for various transformations and do other works using Ballerina Language. 
It enables users to perform custom data transformations within Micro Integrator using Ballerina.

## Installation and Usage

Follow these steps to integrate the Ballerina mediator with your Micro Integrator project:

1.  Clone the Module: Begin by cloning this repository to your local environment.

    -  git clone (https://github.com/chiranSachintha/Ballerina_Mediator_Project.git)

2.  Add `BallerinaMediator-1.0.0-SNAPSHOT.jar` File to Lib Folder: Copy the `BallerinaMediator-1.0.0-SNAPSHOT.jar` file from the cloned module and paste it into the lib folder of Micro Integrator.

3.  Perform Data Transformations:

      -  Create new functions in the `DataMapper` class within the Ballerina project to implement the required transformations.

4.  Build the Ballerina Project:

     -  Build the Ballerina project using this(https://github.com/chiranSachintha/ballerina-lang/tree/ballerina-mediator) branch.

        `./bal build DataMapper`

5.  Add Jar File to Lib Folder: Once the Ballerina project is built successfully, locate the `Datamapper.jar` file and add it to the lib folder in Micro Integrator.

6.  Create Class Mediator:
    -  Create a class mediator in your Micro Integrator project.
    -  Set the class name as `bal.mediator.BalMediator`

7.  Set Properties:
    -  Set properties for the class mediator based on your requirements.
    -  To set the incoming payload as the first parameter, use the following configuration:<br />
       `<property name="firstArgument" value=payload/>`

8.  Up to six arguments can be passed to the class mediator. For example:<br />
    `<property name="thirdArgument" value="ballerina"/>`<br />
    `<property name="fourthArgument" value="language"/>`

9.  Specify the name of the function written for the transformation:<br />
    `<property name="functionName" value="transform_4"/>`

10.  Access Transformation Result:<br />
    After the transformation, the result is set to the context with the property name `result`. You can access it as follows:<br />
    
    `<log level="custom">`<br />
    `<property expression="$ctx:result" name="result"/>`<br />
    `</log>`

### Example

Here's a sample configuration for the class mediator in Micro Integrator:
```
<api context="/HelloWorld" name="HelloWorld" xmlns="http://ws.apache.org/ns/synapse">
    <resource methods="GET">
        <inSequence>
            <payloadFactory media-type="json">
                <format>{"Hello":"World"}</format>
                <args/>
            </payloadFactory>
            <class name="bal.mediator.BalMediator">
                <property name="firstArgument" value="ballerina"/>
                <property name="secondArgument" value="language"/>
                <property name="functionName" value="transform_2"/>
            </class>
            <log level="custom">
                <property expression="$ctx:result" name="result"/>
            </log>
            <respond/>
        </inSequence>
        <outSequence/>
        <faultSequence/>
    </resource>
</api>

```
<img width="946" alt="Screenshot 2024-02-21 at 16 36 18" src="https://github.com/chiranSachintha/Ballerina_Mediator_Project/assets/33259160/152a037b-ee11-4e78-b725-4c5cda625773"><br />


This configuration will apply the transformation specified in the `transform_2` function of the  `Datamapper` class in the Ballerina project.

### Contribution

Contributions are welcome! Feel free to open issues or pull requests for any improvements or additional features.

Note: For implementation details, please refer to: https://github.com/chiranSachintha/Ballerina_Mediator
