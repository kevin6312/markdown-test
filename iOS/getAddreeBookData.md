# 如何存取iPhone 通訊錄裡的資料

iPhone 內部是使用 SQLite3 作為通訊錄的資料庫，但是因為沙盒的限制(沙盒「sandbox」: 指程式在一個獨立且受限的虛擬環境裡執行，可確保不會受其它干擾，也不干擾其它程式運作)
。所以，你是無法直接讀取的必需透過 XCode 所提供的 AddressBook.framework 來讀取和寫入資料。

而 AddressBook.framework 所提的 API，比較接近 C 語言，無法直接使用 NSArray, NSString 來定義變數；其實，在學XCode以來，在 AddressBook.framework 所定義的變數保留字，一直給我一種“為定義而定義”的感覺，很多餘。但不列出來，再過一陣子，我一定會忘了；在此，先列出在 AddressBook.framework 中所使用的變數保留字。

* ABAddressBookRef :  用來宣告 AddressBook物件變數，AddressBook物件在使用上，和 NSManagedObjectContext 一樣，任何對 iPhone 通訊錄的讀取或儲存，都需要透過 AddressBook物件來完成；而建立一個 AddressBook物件指令為 `ABAddressBookRef addressBookObj = ABAddressBookCreateWithOptions(NULL, NULL);`
* ABRecordRef : 用來宣告 ABPerson 物件變數，一筆資料即為一 ABPerson 物件。例如： 產生一筆空白資料，指令為 `ABRecordRef newPerson = ABPersonCreate();`
* CFTypeRef : 萬用變數宣告，其實它就是 void* ；用於字串、任一數值， 例如： `CFTypeRef firstName;` 
* CFArrayRef : 用來宣告陣列變數；

知道了 AddressBook.framework 常用的變數保留字，就來將 iPhone 通訊錄中的 所有記錄取出來吧～

	 //產生 AddressBook 物件
	 ABAddressBookRef addressBookObj = ABAddressBookCreateWithOptions(NULL, NULL); 
	 //取出所有聯絡人記錄
	 CFArrayRef allPeoples = ABAddressBookCopyArrayOfAllPeople(addressBookObj);
	 int numPeople = CFArrayGetCount(allPeoples);
	 //依續取出每個聯絡人資料
	 for(int i=0 ; i<numPeople; i++ ) {
	 	ABRecordRef onePeople = numPeople[i];
	 	// 取出該聯絡人所有資訊
	 }

有了聯絡人，接著就著手處理聯絡人所包含資訊。首先，資料有分單一資料(Property)和多項資料(MultiProperty)，取出後的處理方法也不一樣；
先釐清一個觀念，CFDictionary(屬性：kABDictionaryPropertyType)是單一資料，雖然，Dictionary 可以包含很多資料；而屬性 kABMultiDictionaryPropertyTyple 才是多項資料；很明顯地，在屬性鍵值有'multi’的字眼，便是多項資料； 取出資料的指令為

	 CFTypeRef valueRef = ABRecordCopyValue(oenPeople, kABDictionaryPropertyType);

而要取出所有資料的方法如下：

	 for(ABPropertyID propKey = kABPersonFirstNameProperty; propKey <= kABPersonSocialProfileProperty; propKey++) {
	 	//先取出數值
	 	CFTypeRef valueRef = ABRecordCopyValue(onePeople,propKey);

	 	ABPropertyType propType = ABPersonGetTypeOfProperty(propKey); 
	 	//判斷是單一資料或多項資料
	 	if(propType & kABMultiValueMask) {
	 		//多項資料處理
	 	} else {
	 		//單一資料處理
	 	}
	 }

接著，讓我們看看在一筆聯絡人記錄中，帶有那些資訊吧～

| ABPropertyID | 描述 |
| ---- | ----- |
| kABPersonFirstNameProperty; | First name - **kABStringPropertyType**  |
| kABPersonLastNameProperty;  | Last name - **kABStringPropertyType**  |
| kABPersonMiddleNameProperty; | Middle name - **kABStringPropertyType**  |
| kABPersonPrefixProperty; | Prefix ("Sir" "Duke" "General") - **kABStringPropertyType**  |
| kABPersonSuffixProperty;   | Suffix ("Jr." "Sr." "III") - **kABStringPropertyType**  |
| kABPersonNicknameProperty; | Nickname - **kABStringPropertyType**  |
| kABPersonFirstNamePhoneticProperty; | First name Phonetic - **kABStringPropertyType**  |
| kABPersonLastNamePhoneticProperty; | Last name Phonetic - **kABStringPropertyType**  |
| kABPersonMiddleNamePhoneticProperty; | Middle name Phonetic - **kABStringPropertyType**  |
| kABPersonOrganizationProperty; | Company name - **kABStringPropertyType**  |
| kABPersonJobTitleProperty;  | Job Title - **kABStringPropertyType**  |
| kABPersonDepartmentProperty; | Department name - **kABStringPropertyType**  |
| kABPersonEmailProperty; | Email(s) - **kABMultiStringPropertyType**  |
| kABPersonBirthdayProperty; | Birthday associated with this person - **kABDateTimePropertyType**  |
| kABPersonNoteProperty;  | Note - **kABStringPropertyType**  |
| kABPersonCreationDateProperty; | Creation Date (when first saved) - **kABDateTimePropertyType**  |
| kABPersonModificationDateProperty;   | Last saved date - **kABDateTimePropertyType** |
| kABPersonAddressProperty; | Street address - **kABMultiDictionaryPropertyType**  |
| kABPersonDateProperty;  | Dates associated with this person - **kABMultiDatePropertyType**  |
| kABPersonKindProperty;  | Person/Organization - **kABIntegerPropertyType**  |
| kABPersonPhoneProperty; | Generic phone number - **kABMultiStringPropertyType**  |
| kABPersonInstantMessageProperty; | Instant Messaging - **kABMultiDictionaryPropertyType**  |
| kABPersonURLProperty;   | URL - **kABMultiStringPropertyType**  |
| kABPersonRelatedNamesProperty;  | Names - **kABMultiStringPropertyType**  |
| kABPersonSocialProfileProperty | **kABMultiDictionaryPropertyType**  |

先來看看多項資料，要怎麼處理？

	 CFTypeRef *multiValueRef = ABRecordCopyValue(onePeople,propKey);

	 //先取得資料的數量
	 int numberOfValues = ABMultiValueGetCount(multiValueRef);

	 //在來依續取出其中的資料
	 for(int i = 0 ; i<numberOfValues ; i++) {
	 	CFTypeRef *singleValureRef = ABMultiValueCopyLabelAtIndex(multiValueRef,i);
	 	//單一資料處理
	 }

問題來了，取出來的數值型別皆為 CFTypeRef，若是很熟悉 CFType，那直接使用吧，但我就不熟，所以，還是要轉換成 XCode 常用的型別；

	 NSString *stringValue = CFBridgingRelease(valueRef);	**//kABStringPropertyType**
	 NSNumber *numberValue = CFBridgingRelease(valueRef);	**//kABIntegerPropertyType**
	 NSDate *dateValue = CFBridgingRelease(valueRef);		**//kABDateTimePropertyType**
	 NSDictionary *dictionaryValue = CFBridgingRelease(valueRef);	**//kABDictionaryPropertyType**



