# Abstract Factory

```mermaid

classDiagram
    class Application {
        -factory GUIFactory
        -button Button
        +Application(f: GUIFactory)
        +createUI()
        +paint()
    }

    class GUIFactory {
        <<interface>>
        +createButton() Button
        +createCheckbox() Checkbox
    }

    class WinFactory {
        +createButton() Button
        +createCheckbox() Checkbox
    }

    class MacFactory {
        +createButton() Button
        +createCheckbox() Checkbox
    }

    class Button {
        <<abstract>>
    }

    class Checkbox {
        <<abstract>>
    }

    class WinButton
    class WinCheckbox
    class MacButton
    class MacCheckbox

    Application --> GUIFactory
    GUIFactory <|.. WinFactory
    GUIFactory <|.. MacFactory

    WinFactory ..> WinButton
    WinFactory ..> WinCheckbox
    MacFactory ..> MacButton
    MacFactory ..> MacCheckbox

    Button <|-- WinButton
    Button <|-- MacButton
    Checkbox <|-- WinCheckbox
    Checkbox <|-- MacCheckbox
```

## Creates entire product families without specifying their concrete classes

Abstract Factory defines an interface for creating all distinct products
but leaves the actual product creation to concrete factory classes.
Each factory type corresponds to a certain product variety.

The client code calls the creation methods of a factory object
instead of creating products directly with a constructor call (new operator).

Since a factory corresponds to a single product variant,
all its products will be compatible.

Client code works with factories and products only through their abstract interfaces.
This lets the client code work with any product variants,
created by the factory object.
You just create a new concrete factory class and pass it to the client code.

```mermaid
flowchart TD
Main -->|calls method in Application of interface Button and Checkbox| Application
Application -->|injected through interface| Factory
Factory -->|interface| Button[returns Button]
Button --> Factory
Factory -->|interface| Checkbox[returns Checkbox]
Checkbox --> Factory
```

## Summary

Can change both the factory and each of the widgets
