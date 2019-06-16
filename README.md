# utl-pivot-excel-columns-and-output-a-database-table
Pivot excel columns and output a database table
    Pivot excel columns and output a database table                                                                 
                                                                                                                    
    This problem can be done with one 'proc transpose', instead of three steps.                                     
                                                                                                                    
    github                                                                                                          
    https://tinyurl.com/y4zn8xnt                                                                                    
    https://github.com/rogerjdeangelis/utl-pivot-excel-columns-and-output-a-database-table                          
                                                                                                                    
    SAS Forum                                                                                                       
    https://tinyurl.com/y6s6t3o9                                                                                    
    https://communities.sas.com/t5/SAS-Programming/Reshape-data-to-conduct-Descriptive-Analysis/m-p/566135          
                                                                                                                    
    The single tranpose could output the pivot to a excel sheet without                                             
    creating a physical SAS table with no change in the code.                                                       
                                                                                                                    
    You can use 'Sheet1$'n but I prefer to create                                                                   
    the 'named range' sales.                                                                                        
                                                                                                                    
    SOAPBOX ON;                                                                                                     
      No matter how much time and expense SAS spends on 'proc import/export' it                                     
      will never be as flexible as the passthru, libname, connection, R xlsx or R XLconnect.                        
      SAS needs to make sure whatever enhancement they make to 'proc import/export', they                           
      also make to the classic interfaces. The lotus corporation has stopped                                        
      enhancing it spreadsheet application, so why is SAS beating a dead horse?                                     
      Hopefully SAS will eventually deprecate 'proc import/export"?                                                 
    SOAPBOX OFF                                                                                                     
                                                                                                                    
                                                                                                                    
    *_                   _                                                                                          
    (_)_ __  _ __  _   _| |_                                                                                        
    | | '_ \| '_ \| | | | __|                                                                                       
    | | | | | |_) | |_| | |_                                                                                        
    |_|_| |_| .__/ \__,_|\__|                                                                                       
            |_|                                                                                                     
    ;                                                                                                               
                                                                                                                    
    * Workbbok supplied by op                                                                                       
                                                                                                                    
    d:/xls/sales.xlsx (supeflous variables removed)                                                                 
                                                                                                                    
     XEL.SALES total obs=9                                                                                          
                                                                                                                    
      ID  201305  201306  201307  201308  201309  201310  201311  201312  201401                                    
                                                                                                                    
       0     .       .       .       .       .       .       .       .       3                                      
       1     .       9       4       .       3       .       3       .       .                                      
       2     8       .       .       .       .       .       .       .       .                                      
       3     .       .       5       .       .       .       6       7       .                                      
       4     .       .       .       8       .       6       .       .       .                                      
       5     .       6       7       .       .       .       .       .       .                                      
       6     .       .       .       .       .       8       .       8       .                                      
       7     .       .       .       .       .       .       .       .       .                                      
       8    -2       .       0       1       2       6       1       1       6                                      
                                                                                                                    
    *            _               _                                                                                  
      ___  _   _| |_ _ __  _   _| |_                                                                                
     / _ \| | | | __| '_ \| | | | __|                                                                               
    | (_) | |_| | |_| |_) | |_| | |_                                                                                
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                               
                    |_|                                                                                             
    ;                                                                                                               
                                                                                                                    
    Up to 40 obs WORK.WANT total obs=23                                                                             
                                                                                                                    
    Obs    ID    MONTH     QTY_SOLD                                                                                 
                                                                                                                    
      1     0    201401        3                                                                                    
      2     1    201306        9                                                                                    
      3     1    201307        4                                                                                    
      4     1    201309        3                                                                                    
      5     1    201311        3                                                                                    
      6     2    201305        8                                                                                    
      7     3    201307        5                                                                                    
      8     3    201311        6                                                                                    
      9     3    201312        7                                                                                    
     10     4    201308        8                                                                                    
     11     4    201310        6                                                                                    
     12     5    201306        6                                                                                    
     13     5    201307        7                                                                                    
     14     6    201310        8                                                                                    
     15     6    201312        8                                                                                    
     16     8    201305       -2                                                                                    
     17     8    201307        0                                                                                    
     18     8    201308        1                                                                                    
     19     8    201309        2                                                                                    
     20     8    201310        6                                                                                    
     21     8    201311        1                                                                                    
     22     8    201312        1                                                                                    
     23     8    201401        6                                                                                    
                                                                                                                    
                                                                                                                    
    * you can add the dropped variables to the 'by' statement;                                                      
    * I leave it to the op to create year - you could do it with a previous view of the sheet.                      
    * I don't believe 'proc import' can create a view;                                                              
                                                                                                                    
    libname xel "d:/xls/sales.xlsx";                                                                                
    proc transpose data=                                                                                            
         xel.sales(drop=product colour size style sex discontinued cost profit total_qty_sold)                      
         out=want(drop=_name_  rename=(_label_=month COL1=qty_sold) where=(qty_sold ne .));                         
    by id;                                                                                                          
    var _:;                                                                                                         
    run;quit;                                                                                                       
    libname xel clear;                                                                                              
                                                                                                                    
                                                                                                                    
