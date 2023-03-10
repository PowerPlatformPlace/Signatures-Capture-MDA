# Signatures-Capture-MDA
Integrate a Canvas App inside a Model-Driven App Form to create and edit a signature field. 
USE CASE
Integrate a Canvas App inside a Model-Driven App Form to create and edit a signature field. 

# TOOLS 
Dataverse
Model-Driven App
Canvas App
ModelDrivenFormIntegration Control

# DESIGN
We have two Dataverse tables: **Executives Accounts Table** that will be used to create a Full name and ID for new Accounts. The other table is the **Signatures table** which will hold the Signature title and the signature value which is in base 64 format. The relationship between the two tables is 1 to N, where ***the Executives Account is the One side of the relationship and the Signatures table is the Many side of the relationship.***

# IMPLEMENTATION
- [x] Create the tables and the relationship.
- [x] Create the Form for the Executives' table
- [x] Create the Canvas App
- [x] Create the Model-Driven App
- [x] Add the Canvas App to the Executives Table Information Main Form

# CODE
**Get the MDA record id from the form where the Canvas App is Embeded**

```sj
UpdateContext({lclVarHostMDAformId: GUID(First([@ModelDrivenFormIntegration].Data).ItemId)})
```

**Capture the Signature in base64 format from the PenInput control**

```sj
Set(
    sig64,
    Substitute(
        JSON(
            PenInput1_1.Image,
            IncludeBinaryData
        ),
        """",
        ""
    )
)
```
**Create New Signature**

```sj
Patch(
        Signatures,
        Defaults(Signatures),
        {
            'EID - EXC Account': LookUp(
                'EXC Accounts',
                'EXC Accounts' = lclVarHostMDAformId
            ),
            'Signatures Field': sig64,
            'Sig Name': txtNewTitle.Text
        }
    )
   ;
    ModelDrivenFormIntegration.RefreshForm(true)
```

**Update Existing Signature**

```sj
UpdateIf(
            Signatures,
            'Sig Name' = GallerySigs.Selected.'Sig Name',
            {
                'Signatures Field': sig64,
                'Sig Name': TextInput1.Text
            }
        )
       ;
       ModelDrivenFormIntegration.RefreshForm(true)

