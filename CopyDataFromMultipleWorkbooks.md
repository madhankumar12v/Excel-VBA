#Just copy and past into Excel sheet
```
Sub CopyDataFromMultipleWorkbooks()
    Dim wb As Workbook
    Dim ws As Worksheet
    Dim newWB As Workbook
    Dim newWS As Worksheet
    Dim lastRow As Long
    
    ' Create a new workbook to hold the data
    Set newWB = Workbooks.Add
    Set newWS = newWB.Worksheets(1)
    
    ' Set the starting row for the data in the new worksheet
    lastRow = 1
    
    ' Loop through all open workbooks
    For Each wb In Workbooks
        ' Loop through all worksheets in the current workbook
        For Each ws In wb.Worksheets
            ws.Activate
            
            ' Select the data on the current worksheet, excluding the header row
            Range("B2").Select
            Range(Selection, Selection.End(xlToRight)).Select
            Range(Selection, Selection.End(xlDown)).Select
            
            ' Copy the data to the new worksheet, starting at the last row
            Selection.Copy
            newWS.Range("B" & lastRow).PasteSpecial xlPasteValues
            
            ' Update the last row variable to account for the data that was just pasted
            lastRow = newWS.Cells(newWS.Rows.Count, "B").End(xlUp).Row + 1
        Next ws
    Next wb
    
    ' Save and close the new workbook
    newWB.SaveAs "E:\.xlsx"
    newWB.Close
End Sub
```
more: 