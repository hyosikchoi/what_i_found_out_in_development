# Delegate 패턴

* 객체지향 디자인 패턴 중 하나로, 한 객체가 다른 객체를 대신하여 특정 작업을 수행할 수 있도록 하는 패턴입니다.

* 보통 어떤 객체가 다른 객체를 호출할 때, 해당 객체에 직접 접근하는 것이 일반적입니다. 하지만 이런 경우, 호출하는 객체와 호출되는 객체가 강하게 결합되어 유지보수성이 저하될 수 있습니다. 또한, 호출되는 객체의 변경이 호출하는 객체에 영향을 미칠 수 있습니다.

* Delegate 패턴은 이러한 문제점을 해결하기 위해, 호출되는 객체를 호출하는 객체로부터 분리시키는 것입니다. 호출하는 객체는 호출되는 객체를 직접 호출하는 대신, 호출되는 객체를 대신하여 특정 작업을 수행할 수 있는 **대리자(Delegate) 객체**를 사용합니다. 이렇게 함으로써, 호출되는 객체와 호출하는 객체가 강하게 결합되는 것을 방지할 수 있습니다.

* Delegate 패턴의 구조는 **대리자 객체(Delegate)**와 **호출되는 객체(Real Subject)** 그리고 **호출하는 객체(Client)**로 구성됩니다. 대리자 객체는 호출되는 객체와 같은 인터페이스를 구현하고, 호출되는 객체를 감싸서 호출하는 객체에게 대신 작업을 수행합니다.


* Delegate 패턴은 다음과 같은 장점을 가집니다.

1. 객체 간의 결합도를 낮출 수 있습니다.
2. 호출되는 객체의 변경이 호출하는 객체에 영향을 미치지 않습니다.
3. 코드의 재사용성을 높일 수 있습니다.
4. 호출하는 객체가 호출되는 객체의 내부 구조를 알 필요가 없습니다.

하지만, Delegate 패턴을 사용하면서 주의할 점도 있습니다.

1. 대리자 객체가 많이 생성될 경우, 성능 문제가 발생할 수 있습니다.
2. 대리자 객체와 호출되는 객체의 인터페이스가 일치해야 하기 때문에, 구현 상의 제약이 생길 수 있습니다.

```kotlin

interface Printer {
    fun print()
}

class RealPrinter : Printer {
    override fun print() {
        println("Printing...")
    }
}

class PrinterDelegate(private val printer: Printer) : Printer {
    override fun print() {
        println("Before printing...")
        printer.print()
        println("After printing...")
    }
}

fun main() {
    val printer: Printer = PrinterDelegate(RealPrinter())
    printer.print()
}

```

위 코드에서 PrinterDelegate는 Printer 인터페이스를 구현하고, 생성자에서 Printer 객체를 주입받아 사용합니다. PrinterDelegate는 Printer의 기능을 대신 수행하기 위해, Printer 객체를 멤버 변수로 가지고 있습니다. PrinterDelegate에서는 Printer 객체의 기능을 수행하기 전과 후에 추가적인 로직을 실행합니다. 이를 통해, PrinterDelegate는 Printer 객체의 기능을 대신 수행하면서, 기존의 Printer 객체를 변경하지 않고, 새로운 기능을 추가할 수 있습니다. 이를 통해, PrinterDelegate는 결합도가 낮아지고, 코드 재사용성이 높아집니다.


