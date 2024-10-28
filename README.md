--20241018--  
這是我的研究所目前的實驗進度。  
首先"20240813-目前模型想法"這個資料夾就是放目前的研究想法。  
"test_excel"裡面存放將資料轉為要儲存的excel格式，裡面的SBFL錯誤資訊來源為"SBFL錯誤位置.docx"。  
  --使用方法是將"SBFL錯誤位置.docx"每個project的每個SBFL的Top-1、3、5、10轉為0與1表示的list。  
  --是否有成功生成patch的來源是一張紙，之後記得補上，0表示這個bug-id沒有生成patch，1表示有生成patch且沒成功修復，2表示patcht成功修復。  
"SBFL結果整理用"裡面就是將"SBFL錯誤位置.docx"轉為相對應的0與1表示的輔助程式。  
Ranklib的使用過程網址如下  
https://docs.google.com/document/d/1A23tIO1ONeFT0kbQ3oSyrL5WZY5uckyMNyynHH16iyA/edit?usp=sharing  
"實際執行LTR測試結果"表示目前暫時的執行結果。  

--20241022--
修正bug-id編號，詳情請看"所有的bug-id編號.xlsx"  
在"test_excel"中增加"merge_txt_for_fold.ipynb"，用於半輔助將訓練資料分成5-Fold，以及分為訓練以及測試集。  

--20241025--  
完成5個專案的SBFL整理。  
將Chart的結果應用在另外4個的結果，發現全為1，但是label為0的結果，模型排名結果可能性在1.0，不太合理，可能要用normalize。  

--20241028--  
新增"SBFL_excel_normalize"資料夾，用於將特徵改為0到1之間。  