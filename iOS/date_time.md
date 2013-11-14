


### NSCalendar 
1. can set to "Gregorian"(公曆) or "Hebrew"(希伯來) calendar - almost is "initWithCalendarIdentifier:NSGregorianCalendar", in Gregorian calendar week start at sunday(1) to Saturday(7); 
2. it can convert to NSDate and NSDateComponents;







#define lmOHGDocData2DicData(arr,DocData) [arr addObject:[NSDictionary dictionaryWithObjectsAndKeys:    \
            [DocData.HostID retain],        OHGGKeyHostID,          \
                                                [DocData.DocID retain],         OHGGKeyDocID,           \
                                                [DocData.DocName retain],       OHGGKeyDocName,         \
                                                [DocData.DocDesc retain],       OHGGKeyDocDescription,  \
                                                [DocData.DeptID retain],        OHGGKeyDeptID,          \
                                                [DocData.DeptName retain],      OHGGKeyDeptName,        \
                                                [DocData.prefer retain],        OHGGKeyDocFavorite,     \
                                                [DocData.DocPhoto retain],      OHGGKeyDocPhotoASCII,   \
                                                [DocData.photoData retain],     OHGGKeyDocImage,nil]]
