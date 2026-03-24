
---
title:  Resize
---


# Main set up.
Qt has a function QMainWindow::resizeEvent(event)  in <QResizeEvent>, void resizeEvent(QResizeEvent *event). This function will handle all resize task.

### Step 1: 
	Declare or override the function "void resizeEvent(QResizeEvent *event) override;"
	in header file like this .
	 mainwindow.h
	```cpp
		#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include <QResizeEvent> //Important.


QT_BEGIN_NAMESPACE
namespace Ui {
class MainWindow;
}
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    explicit MainWindow(QWidget *parent = nullptr);
    ~MainWindow() override;

protected:
    void resizeEvent(QResizeEvent *event) override; //This is where we have to override

private:
    Ui::MainWindow *ui;
};

#endif // MAINWINDOW_H

	```

### Step 2:
	Define in mainwindow.cpp file.
		
		'''cpp
		#include "mainwindow.h"
#include "./ui_mainwindow.h"
#include <iostream>



MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
}

MainWindow::~MainWindow()
{
    delete ui;
}


void MainWindow::resizeEvent(QResizeEvent *event){
    QMainWindow::resizeEvent(event);
    std::cout<<"Width:" << event->size().width() << std::endl <<"height:"<<event->size().height()<<std::endl;
    
}
		''' 