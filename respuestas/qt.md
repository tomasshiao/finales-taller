# QT Cheatsheet

## Setup

```cpp
#include <QWidget>
#include <QPainter>

class UnWidget : public QWidget {
  Q_OBJECT

public:
  UnWidget(QWidget *parent = nullptr) : QWidget(parent) {}

protected:
  void paintEvent(QPaintEvent *event) override {
    QPainter painter(this);
    // Dibujo
  }
};
```

## Primitivas de las Figuras

### Líneas

```cpp
QPen pen(Qt::black);
pen.setWidth(2); // Ancho de la línea
painter.setPen(pen);
painter.drawLine(QPoint(x1, y1), QPoint(x2, y2));
```

### Rectángulos

```cpp
QPen pen(Qt::black);
QBrush brush(Qt::yellow);
painter.setPen(pen);
painter.setBrush(brush);
painter.drawRect(QRect(x, y, width, height));
```

### Elipses

```cpp
QPen pen(Qt::black);
QBrush brush(Qt::blue);
painter.setPen(pen);
painter.setBrush(brush);
painter.drawEllipse(QRect(x, y, width, height));
```

### Polígonos

```cpp
QPolygon polygon;
polygon << QPoint(x1, y1) << QPoint(x2, y2) << QPoint(x3, y3);
painter.drawPolygon(polygon);
```

### Arcos

```cpp
QPen pen(Qt::black);
painter.setPen(pen);
painter.drawArc(QRect(x, y, width, height), startAngle, spanAngle); // Ángulos en 1/16 de grado
```

## Transformaciones

```cpp
painter.translate(x, y); // Trasladar el origen
painter.rotate(angle); // Rotar el canvas
painter.scale(scaleX, scaleY); // Redimensión del canvas
```

## Sistema de Coordenadas

- QT usa terna levogia, (0,0) está en la esquina superior izquierda
- `x` aumenta hacia la derecha; `y`, hacia abajo.

## Ejemplos

### Escena con diferentes figuras

```cpp
void UnWidget::paintEvent(QPaintEvent *event) {
  QPainter painter(this);

  // Rectángulo Azul
  painter.setBrush(Qt::blue);
  painter.drawRect(50, 50, 100, 50);

  // Elipse Roja
  painter.setBrush(Qt::red);
  painter.drawEllipse(150, 50, 50, 100);

  // Línea Negra
  painter.setPen(Qt::black);
  painter.drawLine(50, 150, 250, 150);
}
```

### Diagonales rojas

```cpp
#include <QWidget>
#include <QPainter>

class DiagonalWindow : public QWidget {
public:
    DiagonalWindow(QWidget *parent = nullptr) : QWidget(parent) {}

protected:
    void paintEvent(QPaintEvent *event) override {
        QPainter painter(this);

        // Get window dimensions
        int width = this->width();
        int height = this->height();

        // Draw diagonals in red
        QPen pen(Qt::red);
        painter.setPen(pen);

        // First diagonal
        painter.drawLine(0, 0, width, height);

        // Second diagonal
        painter.drawLine(0, height, width, 0);
    }
};
```

### Triángulo Amarillo

```cpp
#include <QWidget>
#include <QPainter>
#include <QPolygon>

class TriangleWindow : public QWidget {
public:
    TriangleWindow(QWidget *parent = nullptr) : QWidget(parent) {}

protected:
    void paintEvent(QPaintEvent *event) override {
        QPainter painter(this);

        // Get window dimensions
        int width = this->width();
        int height = this->height();

        // Create a yellow triangle
        QPolygon triangle;
        triangle << QPoint(0, height) << QPoint(width / 2, 0) << QPoint(width, height);

        QPen pen(Qt::NoPen); // No border
        QBrush brush(Qt::yellow);
        painter.setPen(pen);
        painter.setBrush(brush);

        painter.drawPolygon(triangle);
    }
};
```
