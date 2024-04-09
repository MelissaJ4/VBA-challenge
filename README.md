# VBA-Challenge
Module 2
# VBA-Challenge
# Module 2
# Repo includes Excel screenshots
# Repo includes text file of the VBA used

# VBA copy below

Sub Stocks()

'Have the Macro loop through each worksheet
'Looping code from in-class credit card example
'LastRow VBA from Census in-class assignment
'Finding opening and closing price difference help from another student (Walgama)

    Dim ws As Worksheet
    For Each ws In ThisWorkbook.Worksheets
    
      ' Set an initial variable for holding the stock name
      Dim ticker As String
    
      ' Set an initial variable for holding the total per stock name
      Dim TotalStockVolume As Double
      TotalStockVolume = 0
    
      ' Keep track of the location for each stock name in the summary table
      Dim Summary_Table_Row As Long
      Summary_Table_Row = 2
      
      
      'Yearly change is Column F (OpenPrice)- Column C (ClosePrice)
      'Percentage is YC/OpenPrice x 100
      Dim OpenPrice As Double
      OpenPrice = ws.Cells(2, 3).Value
      Dim ClosePrice As Double

      
      Dim YearlyChange As Double
      Dim PercentChange As Double
      PercentChange = 0
      
      'Label Headers for new data
            ws.Range("A1:Z1").Font.Bold = True
            ws.Range("A1:Z1").HorizontalAlignment = xlCenter
            ws.Cells(1, 10).Value = "TickerSymbol"
            ws.Cells(1, 11).Value = "YearlyChange"
            ws.Cells(1, 12).Value = "PercentChange"
            ws.Cells(1, 13).Value = "TotalStockVolume"
            ws.Cells(1, 16).Value = "TickerName"
            ws.Cells(1, 17).Value = "TotalValue"
            ws.Cells(2, 15).Value = "Greatest % Increase"
            ws.Cells(3, 15).Value = "Greatest % Decrease"
            ws.Cells(4, 15).Value = "Greatest Total Volume"
            
            
     lastrow = ws.Cells(Rows.Count, 1).End(xlUp).Row
      
      ' Loop through all stocks
      
      
    For Row = 2 To lastrow
      
    
        ' Check if we are still within the same ticker symbol, if it is not...
            If ws.Cells(Row + 1, 1).Value <> ws.Cells(Row, 1).Value Then
        
              ' Set the ticker
              ticker = ws.Cells(Row, 1).Value
        
              ' Add to the total stock volume
              TotalStockVolume = TotalStockVolume + ws.Cells(Row, 7).Value
              
              'Find ClosePrice to combine it with OpenPrice
              ClosePrice = ws.Cells(Row, 6).Value
              
              'Find difference between open and close prices for yearly change
              YearlyChange = (ClosePrice - OpenPrice)
              
              'Find the PercentChange YC/OP x 100
              PercentChange = (YearlyChange / OpenPrice)
              
              ' Print the stock in the Summary Table
              ws.Range("J" & Summary_Table_Row).Value = ticker
        
              ' Print the stock amount in the Summary Table
              ws.Range("M" & Summary_Table_Row).Value = TotalStockVolume
              
              'Print Yearlychange in the Summary Table
              ws.Range("K" & Summary_Table_Row).Value = YearlyChange
              
              'Print the PercentChange in the Summary Table
              ws.Range("L" & Summary_Table_Row).Value = PercentChange
              ws.Range("L" & Summary_Table_Row).NumberFormat = "0.00%"

              ' Add one to the summary table row
              Summary_Table_Row = Summary_Table_Row + 1
              
              ' Reset the stock
              TotalStockVolume = 0
        
            ' If the cell immediately following a row is the same stock...
            Else
        
              ' Add to the stock total
              TotalStockVolume = TotalStockVolume + ws.Cells(Row, 7).Value
               
                
            End If

     Next Row
     
         'Conditional Formatting for the YearlyChange column
         'Colors found at https://www.excel-pratique.com/en/vba/colors
         
        LastRow_Summary_Table = ws.Cells(Rows.Count, 10).End(xlUp).Row
        
        For Row = 2 To LastRow_Summary_Table
           
             If ws.Cells(Row, 11).Value >= 0 Then
         
               ' Color the positive stock green
               ws.Cells(Row, 11).Interior.ColorIndex = 43
         
         
           ' Check if the YearlyChange is less than or equal to 0...
             ElseIf Cells(Row, 11) < 0 Then
         
               ' Color the negative stock red
               ws.Cells(Row, 11).Interior.ColorIndex = 46
         
         End If

     Next Row
     
      LastRow_Summary_Table = ws.Cells(Rows.Count, 11).End(xlUp).Row
        
        For Row = 2 To LastRow_Summary_Table
           
             If ws.Cells(Row, 12).Value >= 0 Then
         
               ' Color the positive stock green
               ws.Cells(Row, 12).Interior.ColorIndex = 43
         
         
           ' Check if the YearlyChange is less than or equal to 0...
             ElseIf Cells(Row, 12) < 0 Then
         
               ' Color the negative stock red
               ws.Cells(Row, 12).Interior.ColorIndex = 46
         
         End If

     Next Row

 
Next ws

End Sub
