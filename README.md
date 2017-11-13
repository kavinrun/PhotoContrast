# PhotoContrast
图像清晰度评价算法
### Nowdays,my teacher tell me to write codes for photocontrast.After a week,I have read many pappers,and now I will write something about this interesting thing.<br>
## There are three ways to contrast the photo,and give the score on it.
* Tenengard
* Laplacian
* Variance
## There are the codes
1.Tenengard
```
#include "zmq.h"
#include "include.h"
#include "Localization.h"
#include <time.h>
#include <fstream>

#include <highgui/highgui.hpp>
#include <imgproc/imgproc.hpp>

using namespace std;
using namespace cv;

int main()
{
	Mat imageSource,imageGrey, imageSobel;
	imageSource = imread("1.jpg");
	
	cvtColor(imageSource, imageGrey, CV_RGB2GRAY); //将图像转换为灰度图
	
	Sobel(imageGrey, imageSobel, CV_16U, 1, 1); //sobel算子,(输入图像，输出图像，输出图像的深度,x方向上的差分阶数,y方向上的差分阶数)
	
	
	//图像的平均灰度
	double meanValue = 0.0;
	meanValue = mean(imageSobel)[0];//求出均值

	stringstream meanValueStream;//将int,double转换成为string型
	string meanValueString;

	meanValueStream << meanValue;//将double型的meanValue转化成meanValueStream并赋值给meanValueString
	meanValueStream >> meanValueString;

	meanValueString = "Articulation(Sobel Method): " + meanValueString;

	//putText在图像上绘制文字,(待绘制图像,待绘制文字,位置,字体,尺寸,颜色,宽度,线型)
	putText(imageSource, meanValueString, Point(20, 50), CV_FONT_HERSHEY_COMPLEX, 0.8, Scalar(255, 255, 25), 2);

	//输出图像结果
	imshow("Articulation", imageSource);
	waitKey();
}
```
2.Laplacian
```

```
3.Variance
```
#include <time.h>
#include <fstream>
#include <iostream>
#include <highgui/highgui.hpp>
#include <imgproc/imgproc.hpp>

using namespace std;
using namespace cv;

int main()
{
	Mat imageSource, imageGrey, meanValueImage, meanStdValueImage;

	for (int i = 0; i <= 100; i++)
	{
		
		char s[20];

		//赋值出0.jpg-100.jpg的图像
		sprintf(s, "%d.jpg", i);
		
		//读取0-100.jpg
		imageSource = imread(s);

		//将图像转换为灰度图
		cvtColor(imageSource, imageGrey, CV_RGB2GRAY);

		/*求灰度图像的标准差
		其中mean/meanStdDev计算结果都是double型的
		mean返回的值是Scalar,就是vector类型的数组.所以当要Scalar的元素,要用[n]方式访问.
		meanStdDev计算的均值和标准差都以Mat形式返回,所以访问结果,要访问Mat的元素.
		*/
		meanStdDev(imageGrey, meanValueImage, meanStdValueImage);
		
		double meanValue = 0.0;
		
		meanValue = meanStdValueImage.at<double>(0, 0);

		//double to string 转化
		stringstream meanValueStream;//将int,double转换成为string型
		string meanValueString;

		meanValueStream << meanValue*meanValue;
		meanValueStream >> meanValueString;

		meanValueString = "Articulation(Variance Method): " + meanValueString;

		//putText在图像上绘制文字, (待绘制图像, 待绘制文字, 位置, 字体, 尺寸, 颜色, 宽度, 线型)
		putText(imageSource, meanValueString, Point(20, 50), CV_FONT_HERSHEY_COMPLEX, 0.8, Scalar(255, 255, 25), 2);

		//输出图像结果
		imshow("Articulation", imageSource);

		//等待
		waitKey();
	}
	return 0;
}

```
