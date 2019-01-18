### MS Access and Visual Basic

Visual basic syntax:  
```
If x = N Then
    statement
ElseIf x = N2 Then
End If
```
`Not a`: a as boolean  
`x_object = Null`, `x_number = 0`, `x_string = ""`: initialize  

Built-in functions:  
`IsNull(x)`  
`Now()`: current data and time  
`date2 = DateAdd("s", dt, date1)`: increment by dt seconds  
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

    y = ...
End Function

Private Sub Form_Open(Cancel As Integer) ' upon opening
    If ...
        statement
    Else
        Cancel = True ' form closed 
    End If
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

Form and record operations:  
`DoCmd.RunCommand acCmdSaveRecord`  
`DoCmd.OpenForm "formName", , , , , , x`: passed x to the form opened  
`DoCmd.GoToRecord , , acNewRec`: open new record in form  
`DoCmd.close`: close form  

MS Access SQL queries:  
```
fx = "SELECT ... " & Me.field.Value ' string of SQL
Me.x.RowSource = fx ' update combo box source using value of field
Me.x.Requery
Me.x = Me.x.ItemData(0) ' default display 1st item in list
```
Note: to use DAO, make sure `DAO object library` is selected in VBA console - Tools - References
```
Dim rst As DAO.Recordset 
Dim fx As String 
fx = "SELECT ... AS x0 ..."
Set rst = CurrentDb.OpenRecordset(fx)
x = rst!x0
rst.close
Set rst = Nothing
```

MS Access elements:  
`MsgBox "message", vbExclamation + vbOKOnly, "Box Header"`: open up messagebox  
`Me.checkbox1 = True`: mark checkbox as checked
