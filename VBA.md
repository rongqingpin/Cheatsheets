### MS Access and Visual Basic

Visual basic syntax:  

```
If x = N Then
    statement
ElseIf x = N2 Then
End If

For ii = i0 To i2 Step di
	...
    Exit For
Next ii

Do While ...
    ...
Loop
```

`Not a`: a as boolean  

`x_object = Null`, `x_number = 0`, `x_string = ""`: initialize  

`"" & ""`

Built-in functions:  

`IsNull(x)`  

`Now()`: current data and time  
`date2 = DateAdd("s", dt, date1)`: increment by dt seconds  
`Format(date1, "short date")`: short date without hr-min-sec  

`Val(string)`: to number  
`Str(number)`: to string  

`Len(string)`  

---

Events, function and variable definitions:  

```
Option Compare Database

' public variables that can be accessed across objects
Public x As DataType ' Integer, String, Double, ...

Public Function y(x1 As DataType, x2 As ..., ...) As DataType
    ' private variables that can only be accessed in this object
    Dim x As DataType
    Dim x() As DataType ' initialize a private array x
    Dim z

    x = ...
    ReDim x(i1 To i2) ' array x with dimension 1 by (i2-i1+1)
    z = Shell("software.exe \path\filename.type") ' execute command line
    
    sub_name(...) ' call sub named sub_name
    y = func_name(...) ' call function named func_name
End Function

Private Sub Form_Open(Cancel As Integer) ' upon opening
On Error GoTo Form_Open_Err
    If ...
        statement
    Else
        Cancel = True ' form closed 
    End If
Form_Open_Exit:
    Exit Sub
Form_Open_Err:
    ...
    Resume Form_Open_Exit
End Sub

Private Sub Form_Load() ' upon loading the data in this form
    statement ' can include Me.variables
    y2 = y(x1, x2, ...)
End Sub

Private Sub button_Click() ' button is the name of the button
    statement
End Sub

Private Sub field_AfterUpdate() ' upon updating field in form
    statement
End Sub
```

---

MS Access SQL queries:  

```
fx = "SELECT ... " & Me.field.Value ' string of SQL
Me.x.RowSource = fx ' update combo box source using value of field
Me.x.Requery
Me.x = Me.x.ItemData(0) ' default display 1st item in list
```

```
Dim x As Field2
Set x = Me.Recordset("fieldname") # get the value of specified field in current record
y = x(0) # if multiple records, stored in x starting with 0
```

Note: to use DAO, make sure `DAO object library` is selected in VBA console - Tools - References

```
Dim rst As DAO.Recordset 
Dim fx As String 
fx = "SELECT ... AS x0 ..."
Set rst = CurrentDb.OpenRecordset(fx)
x = rst!x0

Do While Not rst.EOF
    rst.MoveNext
Loop

rst.close
Set rst = Nothing
```

---

MS Access Form and record operations:  

`DoCmd.RunCommand acCmdSaveRecord`  
`DoCmd.RunCommand acCmdPrint`  
`DoCmd.OpenForm "formName", , , , , , x`: passed x to the form opened  
`DoCmd.GoToRecord , , <record>`: `<record>=acNewRec` to open new record in form, or `acLast` to last record  
`DoCmd.OutputTo acOutputForm, "form_name", "PDFFormat(*.pdf)", "", False, "", , acExportQualityPrint`: output to pdf  
`DoCmd.close`: close form  

```
Me.Filter = "criterion"
Me.FilterOn = True
```

MS Access elements:  

`MsgBox "message", vbExclamation + vbOKOnly, "Box Header"`: open up messagebox  
`Me.checkbox1 = True`: mark checkbox as checked  
`Me.field.Enabled = False`: disable combo-box  
`Me.field.Locked = True`

Operations on files:  

`Me.ffile.filename`: `ffile` is the field name of an attachment  
`file.SaveToFile filename`: `file` is a specific record in attachment; filename is the desired string which contains directory

Settings for MS Access:
- To avoid user changing frontend design & hide backend
    - Change form property settings
    - Access Options - Current Database
        1. hide navigation pane
	    2. turn off shortcut manual, full menu
	    3. disable layout view, disable design changes to datasheet
        4. disable special keys
      Then save as ACCDE
- To open form on entering Access: specify in Access Options - Current Database
