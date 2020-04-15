##Интерфейс Movable и его реализации MovablePoint и MovableCircle
Предположим, что у нас есть набор объектов с некоторым общим поведением: они могут двигаться вверх, вниз, влево или вправо. Конкретная реализация поведения (например, как двигаться и как далеко двигаться) зависит от самих объектов. Один из распространенных способов реализации данных методов поведения - это определить интерфейс с именем Movable с абстрактными методами moveUp(), moveDown(), moveLeft() и moveRight(). Классы, которые реализуют интерфейс Movable, обеспечат фактическую реализацию этих абстрактных методов.
***
Реализуйте два конкретных класса - MovablePoint и MovableCircle, которые реализуют интерфейс Movable.
***
<http://online.platforma.institute/asset-v1:digitalspirit.ru+1+1+type@asset+block@ExerciseOOP_Movable.png>
***
Код для интерфейса Movable прост:
```
public interface Movable {  // saved as "Movable.java"
    public void moveUp();
    //...
}
```
Для класса MovablePoint объявите переменные экземпляра x, y, xSpeed и ySpeed с доступом к пакету, как показано с помощью «~» на диаграмме классов (т.е. классы в одном пакете могут обращаться к этим переменным напрямую). Для класса MovableCircle используйте MovablePoint для обозначения его центра (который содержит четыре переменные x, y, xSpeed и ySpeed). Другими словами, MovableCircle составляет MovablePoint + радиус.
```
public class MovablePoint implements Movable { // saved as "MovablePoint.java"
    // instance variables
    int x, y, xSpeed, ySpeed;     // package access

    // Constructor
    public MovablePoint(int x, int y, int xSpeed, int ySpeed) {
        this.x = x;
        //...
    }
    //...

    // Implement abstract methods declared in the interface Movable
    @Override
    public void moveUp() {
        y -= ySpeed;   // y-axis pointing down for 2D graphics
    }
    //...
}
```
```
public class MovableCircle implements Movable { // saved as "MovableCircle.java"
    // instance variables
    private MovablePoint center;   // can use center.x, center.y directly
    //  because they are package accessible
    private int radius;

    // Constructor
    public MovableCircle(int x, int y, int xSpeed, int ySpeed, int radius) {
        // Call the MovablePoint's constructor to allocate the center instance.
        center = new MovablePoint(x, y, xSpeed, ySpeed);
        //...
    }
    //...

    // Implement abstract methods declared in the interface Movable
    @Override
    public void moveUp() {
        center.y -= center.ySpeed;
    }
    //...
}
```
Напишите тестовую программу и попробуйте проверить следующий код:
````
Movable m1 = new MovablePoint(5, 6, 10, 15);     // upcast
System.out.println(m1);
m1.moveLeft();
System.out.println(m1);

Movable m2 = new MovableCircle(1, 2, 3, 4, 20);  // upcast
System.out.println(m2);
m2.moveRight();
System.out.println(m2);
````
Напишите новый класс с именем MovableRectangle, который состоит из двух MovablePoints (представляющих верхний левый и нижний правый углы) и реализующих Movable Interface. Убедитесь, что две точки имеют одинаковую скорость.
***
<http://online.platforma.institute/asset-v1:digitalspirit.ru+1+1+type@asset+block@ExerciseOOP_MovableRectangle.png>
***
В чем разница между интерфейсом и абстрактным классом?