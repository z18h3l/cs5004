java cA Short Course on QT
A cross-platform application framework
Download QT
Installation
1. Run the qt installer you’ve just downloaded.
2. Sign up to acquire a QT account.
3. Accept the license.
Installation
4. Specify installation folder.
5. Select QT 6.x desktop development.
6. Proceed with installation.
Project
Step 1 Create a Qt Project using the wizard.
Project
Select Qt Widgets Application. Step 2
Specify project name and location.
Project
Step 3
Avoid using folder names with a space character (or any foreign characters). 
Define the build system
Project
Step 4
Select qmake as the build system.
Use the default base class.
Project
Step 5
Project
Optionally, specify a translation language
Select a Kit
Project
Step 6
Select Manage button to customise the Kit for your project.
Select MinGW 64-bit kit
Project
Step 7
Click the MinGW 64-bit kit
Qt versions
Project
Step 8
Under QT versions, select the latest version (e.g. Qt 6.5.1)
Compilers
Project
Step 9
Under Compilers tab, select MinGW for C++ and C. You may remove the other existing 
compilers for the project (if there are any) as we don’t need them.
Debuggers
Project
Step 10
Under Debuggers, we will use the one that comes with MinGW. Click Apply, then OK buttons.
Project
Click Next to proceed.
Project
Click Finish.
Project
Files comprising the start-up codes.
This is the Edit view
Project
Build directory.
A build directory is automatically created for the LetterRecognition project.
Select Form, mainwindow.ui
Project
Step 11
Design view
Project
Step 12
Add a horizontal layout
Project
Step 13
Add a label
Project
Step 14
Project
Step 15
horizontalSlider_maxEpochs
Property value
Widgets
Add a horizontal slider.
Add an LCD number.
Project
Step 16
horizontalSlider_maxEpochs
lcdNumber_maxEpochs
Widgets
Property value
Project
Step 17 Switch to Edit mode, then add a new header file to the project.
Project
Switch to Edit mode, then add a header file to the 
project.
Click next, then finish.
Switch to globalVariables.h, then add an external 
variable declaration.
Project
Step 18
#ifndef GLOBALVARIABLES_H
#define GLOBALVARIABLES_H
extern int maxEpochs;
#endif // GLOBALVARIABLES_H
Switch to Design view by clicking main.cpp
Project
Step 19
#include 
#include "mainwindow.h"
int maxEpochs;
int main(int argc, char *argv[])
{
QApplication a(argc, argv);
MainWindow w;
w.show();
return a.exec();
}
Associate a function with the horizontal slider by 
right-clicking it, then selecting Go to slot, then 
the valueChanged() function.
Project
Step 20
#include "mainwindow.h"
#include "ui_mainwindow.h"
////////////////////////////////////////
#include "globalVariables.h“
MainWindow::MainWindow(QWidget *parent) :
QMainWindow(parent),
ui(new Ui::MainWindow)
{
ui->setupUi(this);
}
MainWindow::~MainWindow()
{
delete ui;
}
void MainWindow::on_horizontalSlider_maxEpochs_valueChanged(int value)
{
ui->lcdNumber_maxEpochs->setSegmentStyle(QLCDNumber::Filled);
ui->lcdNumber_maxEpochs->display(value);
maxEpochs = value;
}
Write the implementation for the valueChanged() 
signal.
Project
Step 21
We now have an interface for the maxEpochs
global variable.
Project
Step 22
Add an LCD for displaying a calculated floating 
point value.
Project
Step 1
lcdNumber_result
Improves readability
Add a pushButton.
Project
Step 2
pushButton_Calculate
Right-click the pushButton, then 
select Go to slot to assign a 
function to it’s clicked() signal.
Write the implementation for the clicked() signal, 
inside mainwindow.cpp.
Project
Step 3
void MainWindow::on_horizontalScrollBar_valueChanged(int value)
{
ui->lcdNumber_maxEpochs->setSegmentStyle(QLCDNumber::Filled);
ui->lcdNumber_maxEpochs->display(value);
maxEpochs = value;
}
void MainWindow::on_pushButton_Calculate_clicked()
{
float result=0.0;
result = maxEpochs * 2.2; //some hypothetical formula
ui->lcdNumber_result->display(result);
update();
QCoreApplication::processEvents();
}
Sample run.
Project
Step 4
pushButton_Calculate
Performs a simple calculation: 
30 * 2.2
Project
Mouse cursor How to change the mouse cursor to indicate busy 
calculation activity.
Add the following header first, in order to access 
the mouse cursor methods:
#include 
QApplication::setOverrideCursor(QCursor(Qt::WaitCursor));
//perform lengthy operations here…
QApplication::restoreOverrideCursor();
Add more widgets
Project
Step 5
pushButton
plainTextEdit_results
How to update the gui’s display while running a 
loop?
Project
Widget’s 
display 
contents By calling processEvents(), the display of the 
widget named ui->plainTextEdit_results will be 
updated for each iteration.
By calling processEvents(), the display of the 
widget named ui->plainTextEdit_results will be 
updated for each iteration.
void MainWindow::on_pushButton_clicked()
{
QString msg;
for(int i=1; i plainTextEdit_results->setPlainText(msg);
QCoreApplication::processEvents(); // qApp->processEvents();
QThread::msleep(50); //delay of 50 msec.
}
} 
void MainWindow::on_pushButton_clicked()
{
QString msg;
for(int i=1; i plainTextEdit_results->setPlainText(msg);
QCoreApplication::processEvents(); // qApp->processEvents();
QThread::msleep(50); //delay of 50 msec.
}
} 
Example:
requires requires #include  #include 
Assignment #2
Letter Recognition using Deep Neural 
Nets with Softmax Units
 Learning Objective: Implement backpropagation 
learning algorithm for a deep network classifier system. 
Consider different weight-update formula variations, 
hyperparameter settings, optimization strategies to get the 
best network configuration. Apply modern training 
techniques.
Letter Recognition Problem
UCI’s Machine Learning Repository
Classification Task: Identify 
each of a large number of black and-white rectangular pixel 
displays as one of the 26 capital 
letters in the English alphabet. 
Source: character images based 
on 20 different commercial 
fonts and each letter within 
these 20 fonts was randomly 
distorted to produce a file of 
20,000 unique stimuli. 
http://archive.ics.uci.edu/ml/datasets/Letter+Recognition
Data Set
History:
 P. W. Frey and D. J. Slate (Machine Learning Vol 6 #2 March 91): 
"Letter Recognition Using Holland-style Adaptive Classifiers".
 The best accuracy obtained was a little over 80%
Challenge: Using modern deep network training techniques, we would 
like to find out what is the best accuracy we can obtain.
DATA SET: 
Number of Instances: 20,00代 写data、C/C++
代做程序编程语言0
 Missing Attribute Values: None
INPUTS: 
16 primitive numerical attributes (statistical moments and edge 
counts) 
UCI’s Machine Learning Repository
http://archive.ics.uci.edu/ml/datasets/Letter+Recognition
Data Set
INPUTS: 
16 primitive numerical attributes (statistical moments and edge counts)
UCI’s Machine Learning Repository
Hand-crafted Input Features
INPUTS: 
16 primitive numerical attributes (statistical 
moments and edge counts)
UCI’s Machine Learning Repository
http://archive.ics.uci.edu/ml/datasets/Letter+Recognition
The attributes (before scaling to 0-15 range) are:
1. The horizontal position, counting pixels from the left edge of the image, of the center
of the smallest rectangular box that can be drawn with all "on" pixels inside the box.
2. The vertical position, counting pixels from the bottom, of the above box.
3. The width, in pixels, of the box.
4. The height, in pixels, of the box.
5. The total number of "on" pixels in the character image.
6. The mean horizontal position of all "on" pixels relative to the center of the box and
divided by the width of the box. This feature has a negative value if the image is "leftheavy"
as would be the case for the letter L.
7. The mean vertical position of all "on" pixels relative to the center of the box and divided
by the height of the box.
Hand-crafted Input Features
UCI’s Machine Learning Repository
8. The mean squared value of the horizontal pixel distances as measured in 6 above. This attribute will 
have a higher value for images whose pixels are more widely separated in the horizontal direction as 
would be the case for the letters W or M.
9. The mean squared value of the vertical pixel distances as measured in 7 above.
10. The mean product of the horizontal and vertical distances for each "on" pixel as measured in 6 and 7 
above. This attribute has a positive value for diagonal lines that run from bottom left to top right and a 
negative value for diagonal lines from top left to bottom right.
11. The mean value of the squared horizontal distance times the vertical distance for each "on" pixel. 
This measures the correlation of the horizontal variance with the vertical position.
12. The mean value of the squared vertical distance times the horizontal distance for each "on" pixel. 
This measures the correlation of the vertical variance with the horizontal position.
13. The mean number of edges (an "on" pixel immediately to the right of either an "off“ pixel or the 
image boundary) encountered when making systematic scans from left to right at all vertical positions 
within the box. This measure distinguishes between letters like "W" or "M" and letters like 'T' or "L."
14. The sum of the vertical positions of edges encountered as measured in 13 above. This feature will 
give a higher value if there are more edges at the top of the box, as in the letter "Y.“
15. The mean number of edges (an "on" pixel immediately above either an "off" pixel or the image 
boundary) encountered when making systematic scans of the image from bottom to top over all 
horizontal positions within the box.
16. The sum of horizontal positions of edges encountered as measured in 15 above. http://archive.ics.uci.edu/ml/datasets/Letter+Recognition
Hand-crafted Input Features
INPUTS: 
16 primitive numerical attributes (statistical moments and edge counts) 
scaled to fit into a range of integer values from 0 through 15. 
1. lettr capital letter (26 values from A to Z)
2. x-box horizontal position of box (integer)
3. y-box vertical position of box (integer)
4. width width of box (integer)
5. high height of box (integer)
6. onpix total # on pixels (integer)
7. x-bar mean x of on pixels in box (integer)
8. y-bar mean y of on pixels in box (integer)
9. x2bar mean x variance (integer)
10. y2bar mean y variance (integer)
11. xybar mean x y correlation (integer)
12. x2ybr mean of x * x * y (integer)
13. xy2br mean of x * y * y (integer)
14. x-ege mean edge count left to right (integer)
15. xegvy correlation of x-ege with y (integer)
16. y-ege mean edge count bottom to top (integer)
17. yegvx correlation of y-ege with x (integer)
UCI’s Machine Learning Repository
http://archive.ics.uci.edu/ml/datasets/Letter+Recognition
Letter Recognition Data Set
 INPUTS: 
16 primitive numerical attributes (statistical moments and edge 
counts) 
scaled to fit into a range of integer values from 0 through 15. 
TRAINING and TEST SET:
 We typically train on the first 16,000 items and then use the 
resulting model to predict the letter category for the remaining 
4,000. See the article cited for more details.
UCI’s Machine Learning Repository
http://archive.ics.uci.edu/ml/datasets/Letter+Recognition
Note: We can normalize the inputs (e.g. between [0 to 1]), before feeding them 
to the network.
Note: We can normalize the inputs (e.g. between [0 to 1]), before feeding them 
to the network.
NN architecture
use Softmax
units
At the output 
layer
Minimum of 2 hidden layers
Dataset: Dataset: complete_data_set.txt complete_data_set.txt
Build folder
 Copy the dataset into the build folder to make it 
accessible to the program.
Read the dataset contained in 
complete_data_set.txt
Load the saved weights 
contained in weights.txt
Save the weights resulting from 
training. Filename: weights.txt
Max Epochs (may use either 
a slider or a spinner widget)
Learning rate (may use either a 
slider or a spinner widget)
Train the network using iterative 
minimization of error
Randomly initialize the weights 
of the network.
As we have learned, shuffling the 
training data is important so we 
have a data shuffling button 
here.
L2 regularization
SSE on Training data Percentage of Good 
Classification on Training data
Percentage of Good 
Classification on Training data
SSE on Test data Percentage of Good 
Classification on Test data
Percentage of Good 
Classification on Test data
Single input data pattern
Classification result
Test the input data using the 
network
What should I set to compile a Qt program after 
moving it to another directory?
1. Firstly, delete any file with the extension .pro.user, as they are
created specific to the user’s directory structure, and must be
regenerated after moving a project to another folder.
• e.g. LetterRecognition.pro.user
2. When you are in Qt creator you should rerun qmake. Go to the
left pane where you typically find "Projects" otherwise select
projects. Go to the project name and do a right click, select
"Run qmake".
3. It’s important to note that a path name (very deep directory
structure) that is very long could cause some problems. Simply
reduce the name or move the folder closer to the root dir.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
