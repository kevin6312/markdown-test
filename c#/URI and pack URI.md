(Uniform Resource Identifier)URI �Τ@�귽�ѧO���A�~�Ӷ��h�� System.Uri�D
�N�O�H���󪺤覡�h�O���@����ơA�Ӹ�Ƥ��e�N�O����@�Ӹ귽�]�o�귽�i��O
�@�ӹ��ɡB�Τ@�Ӹ�Ʈw�B�Υ��� WPF ���귽��)�D

URI ���O�M XCode���� **NSURL** ���O�ܹ��A�Ӧb�U���ڱN��U�A��
* Uri�p��ϥΡGUri���غc�r��
* pack:�GPack URI �r��ϥΪ������G


###Uri�p��ϥΡGUri���غc�r��
�b�U�����d�Ҥ�, �N�إ�URI������.

    Uri myPicUri = new Uri("http://www.xxx.com/thePicture.png");  //��������Y�@�ӹ���
    Uri myBlogUri = new Uri("http://cypress-soho.blogspot.tw/");  //���쥻������
    
���p�����ۨ��{��(Assembly)�����귽�ɡA���N�ݭn [Pack URI](http://msdn.microsoft.com/zh-tw/library/aa970069.aspx)

###pack�GPack URI �r��ϥΪ������G

Pack URI�]�t�F�G�Ӥ���G���v/���|�D��榡�p�U

    pack://*authority*/*path*
    
��WPF�䴩��ر��v:**appliction:///**�M**siteoforigin:///** , *application:///*���v
�i�ѧO�sĶ�ɴ��v�������ε{���귽�ɮסD��*siteofiorigin:///*���v�i�ѧO�ӷ������D

![�ʸ� URI �Ϫ�](http://i.msdn.microsoft.com/dynimg/IC146093.png)

�ӥt�~�ݭn�`�N Pack URI�i���ѵ�*�}�񦡫ʸ˺D��(OPC)*�ϥ�,�G�ݭn�ŦXOPC�n�D, �H�P
"/"�r���������N��","�r��. �ҥH�b�����ϥΤW,�r�ꬰ�H*application:,,,*�Ө�*application:///*


    Uri myPng = new Uri("pack://application,,,/cat.png");		//����Assembly����cat.png
    
