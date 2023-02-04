# Signatures-Capture-MDA
Integrate a Canvas App inside a Model-Driven App Form to create and edit a signature field. 
USE CASE
Integrate a Canvas App inside a Model-Driven App Form to create and edit a signature field. 

TOOLS 
Dataverse
Model-Driven App
Canvas App
ModelDrivenFormIntegration Control

DESIGN
We have two Dataverse tables: Executives Accounts Table that will be used to create a Full name and ID for new Accounts. The other table is the Signatures table which will hold the Signature title and the signature value which is in base 64 format. The relationship between the two tables is 1 to N, where the Executives Account is the One side of the relationship and the Signatures table is the Many side of the relationship.

IMPLEMENTATION
Create the tables and the relationship
Create the Form for the Executives' table
Create the Canvas App
Create the Model-Driven App
Add the Canvas App to the Executives Table Information Main Form
