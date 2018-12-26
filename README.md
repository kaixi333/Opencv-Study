# Opencv-Study
学习opencv

#include <opencv2\opencv.hpp>
#include <iostream>
#include <math.h>

using namespace std;
using namespace cv;

Mat src, dst;
char output[] = "OutBlack";

int main(void)
{
	src = cv::imread("../../image/image_close.jpg", 1);
	if (src.empty())
	{
		printf("could not loading image ...");
		return -1;
	}
	namedWindow("Black", CV_WINDOW_NORMAL);
	resizeWindow("Black", 800, 600);
	imshow("Black", src);

	//先膨胀后腐蚀
	/*Mat kernrl = getStructuringElement(MORPH_OPEN, Size(15, 15), Point(-1, -1));
	morphologyEx(src, dst, CV_MOP_OPEN, kernrl);
	namedWindow(output, CV_WINDOW_AUTOSIZE);
	imshow(output, dst);*/

	//先腐蚀后膨胀
	/*Mat kernrl = getStructuringElement(MORPH_OPEN, Size(15, 15), Point(-1, -1));
	morphologyEx(src, dst, CV_MOP_CLOSE, kernrl);
	namedWindow(output, CV_WINDOW_AUTOSIZE);
	imshow(output, dst);*/

	/************************************************************
		形态学梯度  膨胀减去腐蚀
		又称为基本梯度（其他还包括-内部梯度，方向梯度）
	************************************************************/ 
	/*Mat kernrl = getStructuringElement(MORPH_OPEN, Size(15, 15), Point(-1, -1));
	morphologyEx(src, dst, CV_MOP_GRADIENT, kernrl);
	namedWindow(output, CV_WINDOW_AUTOSIZE);*/

	/*
		顶帽-top hat
			顶帽是原图和开操作之间的差值图像
	*/
	/*Mat kernrl = getStructuringElement(MORPH_OPEN, Size(15, 15), Point(-1, -1));
	morphologyEx(src, dst, CV_MOP_TOPHAT, kernrl);
	namedWindow(output, CV_WINDOW_AUTOSIZE);*/

	/*
	黑帽
		黑帽是闭操作图像和原图之间的差值图像
	*/
	Mat kernrl = getStructuringElement(MORPH_OPEN, Size(20, 20), Point(-1, -1));
	morphologyEx(src, dst, CV_MOP_BLACKHAT, kernrl);
	namedWindow(output, CV_WINDOW_AUTOSIZE);


	imshow(output, dst);

	waitKey(0);
	return 0;
}
