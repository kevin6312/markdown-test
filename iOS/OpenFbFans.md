開啟 facebook 粉絲頁,簡單一個指令搞定｡

    [[UIApplication sharedApplication] openURL: [NSURL URLWithString:@"https://www.facebook/com/taiwanbreezeman"]];


若只是這樣,就遜了｡
當 iPhone上有安裝 facebook app,最好能直接打開在 facebook app上｡以下便是範例:

    NSURL *url = [NSURL URLWithString:@"fb://profile/277473558949767"];
    [[UIApplication sharedApplication] openURL:url];


問題來,在 profile 後面那一長串的數字是什麼?? 那便是 facebook 的 profile id｡在我解釋如何取得profile id 前;容我介紹一下,social graph 和 profile id  的關係｡

social graph 這個詞是2007由 facebook 所提出,其概念很簡單,每個人/事/物都是一個點;而關係是一個便是一條線｡你,和親朋好友的關係;和就讀過的學校的關係;和工作的地點的關係;和去過的地點/餐廳或店家的關係;
想像一張白紙,在白紙的中心劃一個點代表你自已,在你自已點的周邊,點上代表著親朋好友/學校/公司/景點或店家的點｡再將代表你的點和這些點以線代表關係,連起來｡便可形成如下圖(來自[Wiki](http://en.wikipedia.org/wiki/Social_graph)),屬於你的 social graph｡

![Social_graph](http://upload.wikimedia.org/wikipedia/commons/0/05/Sna_large.png)

而每一個點都有一個 profile 來描述這個點它代表的人/事/物｡而每個點都擁有一個獨一無二的編號,那就是 profile id｡

好,言歸正傳,取得 profile id 的方法有二種｡
一種是,它就顯示在網址列上:

![在網址上](http://2.bp.blogspot.com/-R_oPRKMEPRw/UXVlXGjiS9I/AAAAAAAAAEA/441QMCS7NeU/s1600/p1.jpg)



而另一種,無法在網址列上找到｡如下圖,是以關鍵字的方式顯示;那就需要 facebook另一個網址來查詢了,查詢網址格式為:"http://graph.facebook.com/{關鍵字}"｡頁面顯示便是profile 的內容,在內容中找尋一個名為 "id" 的字串,後面所帶出來的數字,便是 profile id｡

![透過facebook](http://2.bp.blogspot.com/-GayiutOPdlw/UXVqZmixWhI/AAAAAAAAAEI/7RRYr0zGaVU/s320/p2.jpg)





