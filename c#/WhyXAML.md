

為何撰寫 比較有變化視窗程式要學 XAML?

是因為若要開發比較有變化的視窗程式! 所以, 一定要使用 XAML, 比較簡單!

在早期, 有寫過微軟的視窗程式的人應該都知道 MFC4.0, 而Visual C++ 6.0 是活的最久的開發工具.
(我在2011年還用了VC6.0 替客戶開發了一整套的應用程式, 只因為要支援 XP SE; 而 .NET3 需要 XP SP3)
在 MFC 的時代, 控制項就那些, 很沒有彈性, 且一點變化也沒有; 而且我們在撰寫時, 隨時要注意有沒有 Memory leak.
Memory leak 的測試很花時間, 有時需測到2天2夜才會結果;

進入了 dot COM 時代了, 學了 IUnknown 的觀念, 微軟加強了函數庫的管理和取得的方便性, 和讓 VB/VC/VJ 可共用的函數庫,
也使用了可以互通的資料結構(也就是 Automation 資料型態: VARIANT). 但其實整個視窗開發並沒有很大的變化(只有對網頁ActiveX加強了).

來到了 dot NET 的時代, 微軟使用了 Common Language Runtime (CLR) 機制, 來作資源回收、輾轉呼叫、事件舉發與處理和例外處理.
若對 CLR 很陌生, 沒關係~ 就把它想像成 Java Virtual Mechine 就好了, 只不過是 CLR 是微軟作的, Java VM 是 Sun 作的.

而 dot NET 所開發出來的執行檔(EXE)或動態連結檔(DLL), 在微軟文件稱它叫作 Assembly; 它並不是機器原生碼(Machine Native code), 
也就是, 執行電腦內沒有 dot NET 的環境, 它是無法執行的; 和 JAVA 一樣.

Assembly 包含了
* __Manifest :__ 包含了全球唯一的識別名稱、版本、文化(Culture)資訊...等等
* __Type Metadata :__ 包含了內部所有類別(Class)、資料型別(Type)...等等
* __MSIL :__ Microsoft Intermediate Language, 中介語言; 剛提到了 dot NET 開發出來的執行檔並不是機器原生碼, 而所有的程式都會被 Compile 成 MSIL;
而當程式被執行時, CLR 會去開啟 JIT-Compile (Just In Time Compile, 即時編譯器), 透過 JIT-Compile, 產生CPU可執行的機器原生碼.
* __Resource :__ 指在開發時, 專案內的圖檔、XAML檔和相關資源檔...等等

前面一大堆, 並都沒提到為何使用 XAML 比較容易開發有變化的視窗程式, 先來看下圖
![用XAML開發的程式](http://2.bp.blogspot.com/-5BPqAnuOQLk/UZ8dIHff1GI/AAAAAAAAAEg/tMYnuO1XAcI/s1600/xaml.png)
在圖片中,有三個按鈕, 滑鼠在按鈕上會有玻璃特效, 被選取的按鈕有藍色的框, 還有被點擊時, 按鈕有旋轉的特效.. 以上都是 XAML便可達成,
請參考[這裡](http://msdn.microsoft.com/en-us/library/bb613598.aspx)
C# 的指令, 一行都沒加.

在 dot NET 3.0 時(包含3.0之前),只有 Form 視窗程式, 而 Form 視窗程式要作到上述的特效, 那指令可要寫不少; 
而在 3.5 之後, 開始支援 Windows presentation framework (WPF)才開始使用 XAML 語法. 
現在, 在 Visual C# 新增一個專案, 仍有 Window Form 和 WPF 可以選擇, 就直接使用 WPF 視窗吧~ 便何況, Visual 2012 己經附了 Expression Blend,
不需要另外購買了.






