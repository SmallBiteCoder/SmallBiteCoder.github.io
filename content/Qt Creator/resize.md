






---

title: "Handling Window Resize in Qt"

description: "How to override QMainWindow::resizeEvent to handle UI scaling."

---

  

# Handling Window Resize Events

  

In Qt, `QMainWindow` provides a built-in virtual function called `resizeEvent`. By overriding this, you can execute custom logic—like repositioning widgets or logging dimensions—whenever the user resizes the window.

  

## Step 1: Override the Function in the Header

You must declare the function in your header file under the `protected` section.

  

**mainwindow.h**
```cpp

#ifndef MAINWINDOW_H

#define MAINWINDOW_H

  

#include <QMainWindow>

#include <QResizeEvent> // Required for the event object

  

QT_BEGIN_NAMESPACE

namespace Ui { class MainWindow; }

QT_END_NAMESPACE

  

class MainWindow : public QMainWindow

{

Q_OBJECT

  

public:

MainWindow(QWidget *parent = nullptr);

~MainWindow();

  

protected:

// This is the function we are overriding

void resizeEvent(QResizeEvent *event) override;

  

private:

Ui::MainWindow *ui;

};

  

#endif // MAINWINDOW_H

```

  

## Step 2: Define the Logic in the Source File

  

When implementing the function, it is best practice to call the base class implementation (`QMainWindow::resizeEvent`) first to ensure Qt handles the default layout updates correctly.

  

**mainwindow.cpp**
```cpp

#include "mainwindow.h"

#include "ui_mainwindow.h"

#include <QDebug> // Preferred over std::cout for Qt applications

  

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

  

void MainWindow::resizeEvent(QResizeEvent *event)

{

// 1. Let the parent class do its work first

QMainWindow::resizeEvent(event);

  

// 2. Access the new dimensions

int width = event->size().width();

int height = event->size().height();

  

// 3. Log the output to the Qt Creator console

qDebug() << "Window Resized -> Width:" << width << "Height:" << height;

}

```

  

---

  

### Why use `qDebug()` instead of `std::cout`?

  

1. **No standard library needed:** You don't need `#include <iostream>`.

2. **Qt Creator Integration:** The output is automatically color-coded and appears in the "Application Output" pane.

3. **Format Support:** It can natively print Qt types like `QSize`, `QString`, and `QPoint`.

  

