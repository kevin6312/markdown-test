![](http://4.bp.blogspot.com/-FLdSU7yiKfA/UkElDHFHbQI/AAAAAAAAAAo/5epjtkCLkyw/s1600/%E6%9C%AA%E5%91%BD%E5%90%8D-3.jpg)

UITextField 若需要客製化功能，需要加入UITextFieldDelegate, 使用上：

1. 在 header 檔內，加入<UITextfieldDelegate>
2. 在interface builder入，將 UITextField的delegate拉到 File's owner; 若有時候 Controller一直收不到TextField的Event，就大可能是未設定TextField的Delegate;

而在UITextFieldDelegate 中，常用的函數列出如下：

```
- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField;  
//若不允許被編輯，則return NO，  
    
- (void)textFieldDidBeginEditing:(UITextField *)textField;           
//目前物件成為focus 物件

- (BOOL)textFieldShouldEndEditing:(UITextField *)textField;          
//return YES， 允許結束編輯並重設focus物件的狀能
//return NO，不允許結束編輯`

- (void)textFieldDidEndEditing:(UITextField *)textField;
//??
//may be called if forced even if shouldEndEditing returns NO (e.g. view removed from window) or endEditing:YES called

- (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string;   
//return NO，不允許改變文字

- (BOOL)textFieldShouldClear:(UITextField *)textField;        
//當 User按 clear按鈕, 則此函數會被呼叫；return NO 去忽略 clear 命令

- (BOOL)textFieldShouldReturn:(UITextField *)textField;              
//當 User 按 "換行"鈕， 則此函數會被呼叫；return NO 去忽略 換行 命令
``` 


以下有我使用上幾個實例，

#### 範例一

我希望當使用者， `點 TextField 時，能跳出一個對話框、執行一個動畫、或一個選單`；這時候，我可以使用 UITextField Delegate

```
- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField
```
進一步，我要 TextField 的內容，皆選單或程式完成，不要使用者直接輸入；這時候，我在這個函數的最後回傳“NO”，即可。有點像將 `"User Interaction Disabled"`.

#### 範例二

這是滿常見的，在將 TextField 的英文，轉換成大寫 (Upper case string)

```
- (IBAction)textFieldValueChanged:(id)sender {
    firstNameField.text = [firstNameField.text uppercaseString];
}
```

RN:
2013Oct2:新增 範例一﹠範例二






