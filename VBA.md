### MS Access and Visual Basic

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
    statement
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

`DoCmd.RunCommand acCmdSaveRecord`  
`DoCmd.OpenForm "formName", , , , , , x`: passed x to the form opened

```
If x = N Then
    statement
ElseIf x = N2 Then
End If
```

```
fx = "SELECT ... " & Me.field.Value ' string of SQL
Me.x.RowSource = fx ' update combo box source using value of field
Me.x.Requery
Me.x = Me.x.ItemData(0) ' default display 1st item in list
```