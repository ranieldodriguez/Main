# VBA Cheat Sheet

## Basic Concepts

### Set a Worksheet:

    Dim ws As Worksheet

    Set ws = ThisWorkbook.Sheets("Sheet1")

### Find a Column by Header Name:

    Dim col As Range
  
    For Each col In ws.Rows(1).Cells
  
      If col.Value = "HeaderName" Then
      
          ' Do something with the column
          
        Exit For
          
      End If
      
    Next col

### Find the Last Row with Data:

    Dim lastRow As Long

    lastRow = ws.Cells(ws.Rows.Count, 1).End(xlUp).Row

### Loop Through Rows:

    Dim i As Long
    
    For i = 2 To lastRow

    ' Do something with each row
    Next i

## Common Tasks

### Add a New Column:

    Dim newCol As Range
    
    ws.Cells(1, ws.Columns.Count).End(xlToLeft).Offset(0, 1).Value = "NewColumnName"
    
    Set newCol = ws.Cells(1, ws.Columns.Count).End(xlToLeft)

### Copy Headers to Another Sheet:

    Dim newWs As Worksheet
    
    Set newWs = ThisWorkbook.Sheets.Add
    
    newWs.Name = "NewSheet"
    
    ws.Rows(1).Copy Destination:=newWs.Rows(1)

### Delete Rows Based on Condition:

    Dim keywords As Variant
    
    keywords = Array("Keyword1", "Keyword2", "Keyword3")
    
    For i = lastRow To 2 Step -1
    
        For Each keyword In keywords
        
            If InStr(ws.Cells(i, col.Column).Value, keyword) > 0 Then
            
                ws.Rows(i).Delete
                
                Exit For
                
            End If
            
        Next keyword
        
    Next i

### Calculate and Add Values to a New Column:

    Dim effectiveAge As Double
    
    For Each cell In ws.Range(ws.Cells(2, stateCol.Column), ws.Cells(lastRow, stateCol.Column))
    
        If cell.Value = "FIXED" Then
        
            effectiveAge = ws.Cells(cell.Row, timeToFixCol.Column).Value / 86400000 ' Convert ms to days
            
        Else
        
            effectiveAge = ws.Cells(cell.Row, ageInDaysCol.Column).Value
            
        End If
        
        ws.Cells(cell.Row, effectiveAgeCol.Column).Value = effectiveAge
        
    Next cell
