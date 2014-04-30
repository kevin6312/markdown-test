SimpleFTPSample

### PutController

使用到  

	NSURL *url = CFBridgingRelease(CFURLCreateCopyAppendingPathComponent(NULL, (__bridge CFURLRef) url, (__bridge CFStringRef) [filePath lastPathComponent], false));
	NSOutputStream *networkStream = CFBridgingRelease(CFWriteStreamCreateWithFTPURL(NULL, (__bridge CFURLRef) url));
	[self.networkStream setProperty:self.usernameText.text forKey:(id)kCFStreamPropertyFTPUserName]
	[self.networkStream setProperty:self.passwordText.text forKey:(id)kCFStreamPropertyFTPPassword]
