# ClientSecurityAddon

## Description
For securing the Mendix Client from malicious commit actions of entities.

## Typical usage scenario
Use this module if to prevent that the requests from the Mendix client to the runtime are executed to commit objects and bypass nanoflow/microflow validations and checks.

## Features and limitations
Features
- Uses a global before commit event handler for validating commits of object - instead of having to create entity specific before commit event handlers.
- Toolbox actions to allow commits of objects or lists of objects. Alternatively, manually set the boolean in a change object action.

Limitation
- This will not work for microflows that have `Apply entity access` set to `Yes` due to the fact that access rights that are set to none.

## Dependencies
- v1.0.0 for MX 8.18.25 or higher and Mendix 9
- v2.0.0 for Mendix 10.1.1 or higher

## Installation
Download the module and add it to your project.

## Configuration

**1. Constant value**
- Set the constant `MemberNameAllowCommit` to the value that you will use in your project. The name of the attribute to allow commits e.g. `_isCommitAllowed`. Set the value in your project configuration and cloud deployment environment.

**2. After Startup**
- Add the microflow `AfterStartUp` of the module `ClientSecurityAddon` to your applications after startup microflow

**3. Domain model - To secure an entity**
- Add a boolean member with the value of this constant value e.g. `_isCommitAllowed` 
- Specifiy no access rights on this member for any module role.

**4. Microflows - To allow commits in a microflow**

- **One object**: Select or drag and drop the `Object allow commit` activity in your microflow and pass the object that you want to allow a commit for as the parameter to this activity.

- **List of objects**: Select or drag and drop the `List allow commit` activity in your microflow and pass the object that you want to allow a commit for as the parameter to this activity.
 
- **Alternatively**: In a `Create object` / `Change object` activity in your microflow set the member value to `true`.
