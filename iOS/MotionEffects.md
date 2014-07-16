# iOS 7 的 MotionEffects

iOS 7 剛出來時，大家第一個會注意到的事在 Lock Screen 有一個會動的背景；那就是 Motion Effects。 <br>
其實它很簡單，我試著在一個UIView 加上一個 UIButton，接著讓 Button 是浮動的。看程式碼就懂了。

	- (void)viewDidLoad
	{
	    [super viewDidLoad];
		// Do any additional setup after loading the view, typically from a nib.
	    
	    aButton.layer.mask.frame = aButton.bounds;
	    aButton.layer.masksToBounds = YES;
	    
	    UIInterpolatingMotionEffect *xAxis = [[UIInterpolatingMotionEffect alloc]
	                                          initWithKeyPath:@"center.x"
	                                          type:UIInterpolatingMotionEffectTypeTiltAlongHorizontalAxis];

	    xAxis.minimumRelativeValue = [NSNumber numberWithFloat:-90.0];
	    xAxis.maximumRelativeValue = [NSNumber numberWithFloat:90.0];
	    
	    UIInterpolatingMotionEffect *yAxis = [[UIInterpolatingMotionEffect alloc]
	                                          initWithKeyPath:@"center.y"
	                                          type:UIInterpolatingMotionEffectTypeTiltAlongVerticalAxis];
	                                          
	    yAxis.minimumRelativeValue = [NSNumber numberWithFloat:-90.0];
	    yAxis.maximumRelativeValue = [NSNumber numberWithFloat:90.0];
	    
	    UIMotionEffectGroup *group = [[UIMotionEffectGroup alloc]init];
	    group.motionEffects = @[xAxis, yAxis];
	    [aButton addMotionEffect:group];
	}



