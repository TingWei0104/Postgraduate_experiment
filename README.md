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
  
--20241105--  
目前進度，已經將這些不同的project各別訓練，但是結果不好。  
目前想法應該是將從學長那邊找到的資料，將訓練集的大小擴大。 
目前先想辦法將資料整理出來的方法，將找到的資料的Top-1、3、5、10整理出來，  
並結合到原本整理出learning to rank的程式中試試看，讓輸出的excel有包含這些資料。    
  
--20241106--
在"20241105-整理學長資料用"資料夾中的"test.ipynb"有產生動態二微陣列的方法，以後可以再來看看怎麼操作，也有建立一個txt將資料寫入的方法。 
之後有補上能一併輸出這是top多少的結果。   
整理好的資料也先不要上傳，怕會讓Github容量炸掉。  
  
--20241111--  
目前問題，學姊的資料可能都有點問題，需要之後再重新整理。  
目前先改成用我的方法看看。 
  
--20241112--
"20241105-整理學長資料用"資料夾中，改成用"Chart整理_excle.ipynb"一次將所有的結果整理成excel，省得麻煩。  
因此"Chart整理.ipynb"以及"test.ipynb"這些程式暫時作廢，放著不動。  
  
目前已經弄出來了，使用的程式為"Chart_整理出top.ipynb"，更改其中的"SBFL_index"變數，來半自動產生出這些top資訊，並存到word檔案中。 
  
出現問題了，top計算出問題了。  
  
--20241112--  
top計算問題已解決，也已經將整個自動化處理完畢。
目前已經將"20241105-整理學長資料用/chart_result"的所有透過"Chart整理_excel.ipynb"的所有東西放到更外部的"20241113"資料夾中，  
反正不是在這個git中就是了。  
  
"20241105-整理學長資料用"裡面的"SBFL_result_to_01.ipynb"就是把"Chart_整理出top.ipynb"整理出來的結果轉為0與1的二維list，用於後續的"create_SBFL_chart_normaliza.ipynb"。  
  
Chart已整理完成，目前將其掛入Ranklib試試看。  

訓練結果如"20241105-整理學長資料用/chart_result/Cahrt應用於Ranklib-20241113.docx"所表示，訓練結果有一些的問題後面有提到一些後續的改善想法。  

--20241115--  
發現Lang沒有"Kulczynski"、"Pearson"，要再回去把前面的都修正。 
修正完成之後打算將Top的數值做調整，改成其他的方式做使用，目前打算把Top-1、3、5、10都有的話設定為1，Top-3、5、10而1沒有，都設定為0.8，以此類推。

--20241118--  
在"20241105-整理學長資料用/XXXX_整理出top.ipynb"中加上懷疑值的list(Sus_value)。  
目前"20241105-整理學長資料用/XXXX_整理出top.ipynb"有bug，如果top-1有超過200會出bug，需要修正，目前已經將chart修正。  

--20241120--  
有問題，此專案先暫時擱置。  

--20250115--
此方法繼續，之後應該是新增一個"新實驗"的資料夾。  
以及會增加astor的3種APR結果(jgenprog、jkali、jMutRepair)。  
label改成:0、1、2、3，  
分別表示"無SBFL且無patch"、"有SBFL且無patch"、"無SBFL且有patch"、"有SBFL且有patch"，  
有patch比較重要，因此"有SBFL且無patch"設為1，"無SBFL且有patch"設為2。  
使用的方法以"20241105-整理學長資料用"這個資料夾有的方法來進行。  
目前先等待astor完成。

之後打算看看astor的"DeepRepair"、"Cardumen"、"3sfix"能不能使用，如果不能的話那就先以先以新增(jgenprog、jkali、jMutRepair)這三個為主。  

--20250120--  
將模型改進後的結果，有加上懷疑值的結果很差。  
因此改成用"SBFL_chart_no_sus.txt"的結果做比較，發現會先針對SBFL都有在Top1找到的梯隊排序APR結果，之後再針對在Top-3找到的梯隊排序APR結果，以此類推。  
後面加上"SBFL_chart_one_top.txt"的結果，從結果上來看能夠針對錯誤定位結果以及APR的修復結果來做整體的排名，這兩種方法都能作為後續的討論。  

--20250206--  
根據"20250116-整理資料並訓練"結果來看，使用"top-1"、"top-3"、"top-5"、"top-10"、"是否生成"，label為0、1、2、3結果有點差。  
而使用"top"以及"是否生成"兩個feature的結果就符合當初的預想結果。  

而現在需要加上每個APR會使用到甚麼特別的資訊，用於生成patch，以找出哪些資訊對於生成patch是相關的。  
因此新增一個資料夾"20250206-新增APR相關特徵"用來處理此問題。  

--20250207--  
加上"20250206-新增APR相關特徵"資料夾，用於新增特徵的資料使用。  
目前已經新增"create_SBFL_chart_normaliza.ipynb"，並且輸出成功。  

此資料夾中新增整理排名結果的程式碼"sort_result.ipynb"，將原始資料做排名，會分成有分頁的整理與沒分頁的處理。  

--20250210--  
使用統計APR結果作為後續的label。  
因此要寫一個新的ipynb檔案來統計這個結果。  

相同的APR，統計一個bug_id的分數，  
如Chart-1使用ACS，共有47個結果，將其結果分母設定為47，分子為有在top1、3、5、10各自設定成1、0.8、0.6、0.4，乘上47個SBFL有在這個位置定位的數量，  
之後乘以這個APR有沒有在這個bug_id生成patch(0,1)，這個數字就是當成這個APR在這個bug_id的成效當成是label。  

可能的問題: 因為SBFL結果都是相同的，因此權重分數在同一個APR上都是一樣的，又因為每個APR，如ACS與Nopol都是用上相同的錯誤定位結果，它們的這個分數也是相同的，可能(0,1)改成以如ACS在chart總共1個plausible patch，就改成乘上1/26;Nopol有9個，就是乘上9/26。(不確定，先把東西做出來再判斷)。  

這個新的ipynb檔案是"20250206-新增APR相關特徵/caculate_XXXXX_label.ipynb"所生成的，並且修正"create_SBFL_XXXXX_normaliza.ipynb"的輸出格式。    

--20250210加筆--  
並把之前的實驗數據放在"20250206-新增APR相關特徵/使用多個APR特徵的結果"，這個資料夾中，以區分新舊。  
分析結果的檔案放在"20250206-新增APR相關特徵/使用多個APR特徵的結果/chart/OLD_Chart應用Ranklib.docx"裡面。
這裡面也有分析模型的方法，之後一定要來這個word檔案看。    
這裡面也有分析模型的方法，之後一定要來這個word檔案看。    
這裡面也有分析模型的方法，之後一定要來這個word檔案看。    
很重要所以說三次。  

--20250212--  
新增完"caculate_XXXXX_label.ipynb"後，"create_SBFL_XXXXX_normaliza.ipynb"所輸出的"test_SBFL_XXXX_normalize.xlsx"。  
現在要修正"20250206-新增APR相關特徵/excel_to_txt.ipynb"的內容。  

將數據執行後，整理分析的結果"20250206-新增APR相關特徵/chart/Chart應用Ranklib.docx"，根據結果來看，完全是錯誤的。 

之後將APR統計分數作為其中一個feature，使用5個feature，label就如同"--20250206--"的說明。  
測試結果在"chart/Chart應用Ranklib.docx"裡面。  
不知道在哪一部分就搜尋: 驗證資料(Chart應用於Chart)、驗證資料(Chart應用於Closure)。  
這兩個地方。  
並且其中有使用Score這個指令，這個指令不像是使用"indri"順便進行排序，會是把每個pid中的每一個編號的預測分數顯示出來。  



考慮結果與"20250206-新增APR相關特徵/使用多個APR特徵的結果/chart/chart排名結果_F3_one_top.xlsx"對照，這個使用方式請看"20250206-新增APR相關特徵/使用多個APR特徵的結果/chart/OLD_Chart應用Ranklib.docx"。  



--20250213--  
考慮top-10就不參考了，因此要改新的資料夾，新增一個"20250213去除top10與修正計算"資料夾。  

