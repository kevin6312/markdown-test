(Uniform Resource Identifier)URI 統一資源識別元，繼承階層為 System.Uri．
就是以物件的方式去記錄一筆資料，而資料內容就是指到一個資源（這資源可能是
一個圖檔、或一個資料庫、或任何 WPF 的資源檔)．

URI 類別和 XCode中的 **NSURL** 類別很像，而在下面我將協助瞭解
* Uri如何使用：Uri的建構字串
* pack:：Pack URI 字串使用的概念：


###Uri如何使用：Uri的建構字串
在下面的範例中, 將建立URI的物件.

    Uri myPicUri = new Uri("http://www.xxx.com/thePicture.png");  //指到網路某一個圖檔
    Uri myBlogUri = new Uri("http://cypress-soho.blogspot.tw/");  //指到本部落格
    
但如何指到自身程式(Assembly)內的資源檔，那就需要 [Pack URI](http://msdn.microsoft.com/zh-tw/library/aa970069.aspx)

###pack：Pack URI 字串使用的概念：

Pack URI包含了二個元件：授權/路徑．其格式如下

    pack://*authority*/*path*
    
而WPF支援兩種授權:**appliction:///**和**siteoforigin:///** , *application:///*授權
可識別編譯時期己知的應用程式資源檔案．而*siteofiorigin:///*授權可識別來源網站．

![封裝 URI 圖表](http://i.msdn.microsoft.com/dynimg/IC146093.png)

而另外需要注意 Pack URI可提供給*開放式封裝慣例(OPC)*使用,故需要符合OPC要求, 以致
"/"字元必須取代為","字元. 所以在正式使用上,字串為以*application:,,,*來取*application:///*


    Uri myPng = new Uri("pack://application,,,/cat.png");		//指到Assembly內的cat.png
    
