1) cd C:\opencv342\build\x64\vc14\bin or equivalent folder for OpenCV installation

2) Create new folder STOP-SIGN-Training
cd C:\OpenCV2\opencv\build\x64\vc14\bin\STOP-SIGN-Training

3) create folders under folder STOP-SIGN-Training
data
info
neg

4) Take a real picture of the STOP Sign and save it in this folder ex. stop-sign.jpg (try to not shrink resize it if possible)
5) In the neg folder download 1088 negative gray scale pictures 100x100 pixels
6) Make sure to collect their names (you can use a Python script). File contents should be a list of files in the neg folder like:
neg/1.jpg
neg/10.jpg
neg/100.jpg
neg/1000.jpg
neg/1001.jpg
neg/1002.jpg
neg/1003.jpg
neg/1004.jpg
neg/1005.jpg
neg/1006.jpg 

7) opencv_createsamples -img stop-sign.jpg -bg bg.txt -info info/info.lst -pngoutput info -maxxangle 0.5 -maxyangle 0.5 -maxzangle 0.5 -num 1088

8) ..\opencv_createsamples.exe -info info/info.lst -num 1088 -w 20 -h 20 -vec positives.vec
9) ..\opencv_traincascade.exe -data data -vec positives.vec -bg bg.txt -numPos 950 -numNeg 544 -numStages 10 -w 20 -h 20 -minHitRate 0.998 -maxFalseAlarmRate 0.3
10) The above script should run for atleast 25 minutes and increasingly go through 10 Stages with more time being taken
11) Copy the cascade.xml file from the data folder (this is the HAAR CASCADE FILE GENERATED)
12) Use it with live.py and a webcam to detect the STOP sign.