# 如何新增一筆聯絡人資料到通訊錄
接著上一篇![如何存取iPhone 通訊錄裡的資料](http://xcnote.blogspot.tw/2013/12/iphone.html)，接著就是要新增一筆資料寫入通訊錄了。其實很簡單，只要呼叫 ABPersonCreate(); 便可產生一筆空白資料，多項資料(MultiProperty)比單項資料(Property)多了一道處理程序；直接來看範例～

	 NSString *firstName, *lastName, ... ;
	 NSDictionary *emails;
	 ...

	 //產生 AddressBook 物件
	 ABAddressBookRef addressBookObj = ABAddressBookCreateWithOptions(NULL, NULL);

	 //產生一筆空白聯絡人資料
	 ABRecord record = ABPersonCreate();

	 //處理單項資料 (property)
	 ABRecordSetValue(record, kABPersonFirstNameProperty, CFBridgingRetain(firstName) , nil);
	 ABRecordSetValue(record, kABPersonLastNameProperty, CFBridgingRetain(lastName) , nil);

	 //處理多項資料 (MultiProperty)
	 NSArray *allLabels = [emails allKeys];
	 ABMutableMultiValueRef multiValue = ABMultiValueCreateMutable(kABMultiStringPropertyType);
	 for(NSString *label in allLabels) {
	 	NSString *value = [emails objectForKey:label];
	 	ABMultiValueAddValueAndLabel(multiValue, CFBridgingRetain(value), CFBridgingRetain(label), NULL);
	 }
	 ABRecordSetValue(record, kABPersonEmailProperty, multiValue, nil);

	 //寫入&儲存
	 ABAddressBookAddRecord(addressBookObj,record,nil);
	 ABAddressBookSave(addressBookObj);

在上面的例子中，是直接產生一筆空白的聯絡人資料；若是換成即有存在的舊資料，也是可以的，但在處理多項資料時，若遇到已經存在的label，不可使用 ABMultiValueAddValueAndLabel，請改用 ABMultiValueReplaceValueAtIndex 去處理；

除了，直接寫入通訊錄外， framework 另外提供了預設的聯絡人的輸入UI，共有二套，一為 "ABNewPersonViewController"；另一為 "ABUnknownPersonViewController"；差別在於後者可以選擇覆寫即有的資料。

ABNewPersonViewController 的範例～

	 ABNewPersonViewController *newPersonVC = [[ABNewPersonViewController alloc] init];
     ABRecordRef aNewRecord = ABPersonCreate();
    
     newPersonVC.newPersonViewDelegate = self;
     newPersonVC.addressBook = addressBookObj;
     newPersonVC.displayedPerson = aNewRecord;
    
     [currentNavigationViewController pushViewController:newPersonVC animated:YES];

ABNewPersonViewController 的範例～

	 ABUnknownPersonViewController *unknowPersonVC = [[ABUnknownPersonViewController alloc]init];
     unknowPersonVC.unknownPersonViewDelegate = self;
     unknowPersonVC.displayedPerson = aOldRecord;
     unknowPersonVC.allowsAddingToAddressBook = YES;
     unknowPersonVC.allowsActions = YES;

     [currentNavigationViewController pushViewController:unknowPersonVC animated:YES];






