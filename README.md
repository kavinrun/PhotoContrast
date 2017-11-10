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
	
	//double to string

	stringstream meanValueStream;//将int,double转换成为string型
	string meanValueString;

	meanValueStream << meanValue;
	meanValueStream >> meanValueString;

	meanValueString = "Articulation(Sobel Method): " + meanValueString;

	//	putText在图像上绘制文字,(待绘制图像,待绘制文字,位置,字体,尺寸,颜色,宽度,线型)
	putText(imageSource, meanValueString, Point(20, 50), CV_FONT_HERSHEY_COMPLEX, 0.8, Scalar(255, 255, 25), 2);

	imshow("Articulation", imageSource);//输出图像结果
	waitKey();
}
```
