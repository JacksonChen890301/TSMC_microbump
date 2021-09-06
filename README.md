# 3D元件分析(microbump)
  本處紀錄了2020~2021年間於microbump的研究計畫中所有的code以及詳細的註解，有任何問題歡迎詢問我本人。
  
## 問題概述
+ 由於電子封裝產業逐漸以 3D 封裝為主，銲錫微凸塊(microbump)此種用於垂直連接晶片的結構也被廣泛使用。此技術以覆晶封裝為基礎，用銲錫微凸塊來連接堆疊各層矽晶片。不同層之矽晶片則以矽穿孔(Through Silicon Via, TSV)做訊號傳遞，透過此垂直整合的結構減少封裝體積以及訊號延遲與失真。然而此元件在回流焊接(reflow)製程中，會有焊錫頸縮以及介面金屬共化物(Intermetallic Compound, IMC)產生的現象(如下圖)，造成元件壽命的減少和性能的下降。
  
<div align=center><img src=https://upload.cc/i1/2021/09/06/tIixk0.png></div>

+ 為了解決上述問題，實驗端重複reflow的製程，並透過電阻量測判斷元件的狀態。當實驗端發現量測出的電阻值相較於reflow前高於某個比例時，就會將整個元件用非破壞性檢測(CT電腦斷層，如下圖)得出元件內部形貌的影像資料。整個研究的最終目的就是找出microbump的變化和電阻等性質的關聯性。

<div align=center><img src=https://user-images.githubusercontent.com/55709819/132184994-79661609-f2e0-4c89-83ae-7d05acc236ad.png width="500"></div>
<div align=center>(a)CT原始影像</div>

<div align=center><img src=https://user-images.githubusercontent.com/55709819/132185063-ad18e186-05fd-4b80-ba6a-b56ea8a7c749.png></div>
<div align=center>(b)裁切後的影像</div>

## 電阻值模擬
+ 因為實驗端測電阻是得出整個晶片的電阻，相當於數百顆bump串連後的電阻，無法針對單一bump做量測。為了能夠討論每顆bump個別的狀態，必須用模擬的方式取得單一bump的電阻(ANSYS)。
+ ANSYS對資料的要求比較嚴謹，因為是透過不同物質的電阻率計算出結果，所以圖像還必須根據已知的物質對每個pixel做標籤，標記該pixel屬於某個物質才能計算。至於那些pixel屬於甚麼物質就必須灰度的分布(下圖)來判斷。
<div align=center><img src=https://user-images.githubusercontent.com/55709819/132188061-73e50780-36c3-413b-b34b-c966ce60d796.png></div>

## Machine Learning
+ 經由ANSYS得到單一bump的電阻後，因為ANSYS計算時間非常長，圖像的要求又嚴格，而且不容易歸納出電阻跟bump形貌的關聯，因此以下用CNN為主軸的神經網路來學習ANSYS計算出的電阻，後續會用一些演算法來反推電阻跟bump形貌的相關性。












