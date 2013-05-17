要開啟 plist file，首先要先知道 plist file 的根 (root) 是何種資料型態。"根"的資料型態有二種：Array / Dictionary。

![plist 的根，只能是Array或Dictionary](http://1.bp.blogspot.com/-hpM0zNbsJAA/UWVpB_-Zz4I/AAAAAAAAADc/B_3j2EKlIfQ/s1600/type.png)

依資料型態選擇不同，使用不同類別來開啟。


* ###Array範例:
-----
    NSString *plistPath = [[[NSBundle mainBundle] bundle]
    stringByAppendingPathComponent:@"MyPlist.plist"];
    NSArray *plistArray = [NSArray arrayWithContentsOfFile: plistPath]; //讀取plist file
    NSString *propertyString = [plistArray objectAtIndex:2];            //取得字串物件
    NSInteger *propertyInt = [[plistArray objectAtIndex:2] intValue]; //取得整數值
    Bool propertyBool = [[plistArray objectAtIndex:2] boolValue];    //取得布林值
    float propertyFloat = [[plistArray objectAtIndex:2] floatValue];   //取得浮點數值
    [plistArray writeToFile:plistPath atomically:NO]; //回寫plist file

* Dictionary範例：
----------------

    NSString *plistPath = [[[NSBundle mainBundle] bundle]
    stringByAppendingPathComponent:@"MyPlist.plist"];
    NSDictionary *plistDic = [NSDictionary dictionaryWithContentsOfFile: plistPath]; //讀取plist file
    NSString *propertyString = [plistDic objectForKey:@"姓名"];            //取得字串物件
    NSInteger *propertyInt = [[plistDic objectForKey:@"年齡"] intValue]; //取得整數值
    Bool propertyBool = [[plistDic objectForKey:@"已婚"]  boolValue];    //取得布林值
    float propertyFloat = [[plistDic objectForKey:@"身高"]  floatValue];   //取得浮點數
    
    [plistDic writeToFile:plistPath atomically:NO]; //回寫plist file




