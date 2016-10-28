# Decorator
### Structural Design Pattern

#### Обобщение
Decorator Pattern-ът е шаблон, който се използва в обектно-ориентираното програмиране. Този шаблон може да бъде използван за разширяването на функционалността на опеределен клас по времето на изпълнение на програмата, като запазва интерфейса му. Той е много подходящ, когато се следва Single responsibility принципът, според който един клас трябва да е отговорен за една единствена операция.

#### Структура
* Component – интерфейсът на обектите, към които могат да се добавят допълнителни функционалности или качества динамично;
* ConcreteComponent – обектът, към който ще се добавя нова функционалност;
* Decorator – пази референция към компонент обекта и създава интерфейса, който съвпада с този на компонента;
* ConcreteDecorator – прибавя нови функционалности към обекта;

#### Диаграма
![pattern structure](../Images/decorator-diagram.gif)

#### Demo
~~~c#
using System;

namespace DecoratorPattern
{
    /// <summary>
    /// Launccher class for Structural 
    /// Decorator Design Pattern.
    /// </summary>
    class Launcher
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        static void Main()
        {
            // Create ConcreteComponent and two Decorators
            ConcreteComponent c = new ConcreteComponent();
            ConcreteDecoratorA d1 = new ConcreteDecoratorA();
            ConcreteDecoratorB d2 = new ConcreteDecoratorB();

            // Link decorators
            d1.SetComponent(c);
            d2.SetComponent(d1);

            d2.Operation();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Component' abstract class
    /// </summary>
    abstract class Component
    {
        public abstract void Operation();
    }

    /// <summary>
    /// The 'ConcreteComponent' class
    /// </summary>
    class ConcreteComponent : Component
    {
        public override void Operation()
        {
            Console.WriteLine("ConcreteComponent.Operation()");
        }
    }

    /// <summary>
    /// The 'Decorator' abstract class
    /// </summary>
    abstract class Decorator : Component
    {
        protected Component component;

        public void SetComponent(Component component)
        {
            this.component = component;
        }

        public override void Operation()
        {
            if (component != null)
            {
                component.Operation();
            }
        }
    }

    /// <summary>
    /// The 'ConcreteDecoratorA' class
    /// </summary>
    class ConcreteDecoratorA : Decorator
    {
        public override void Operation()
        {
            base.Operation();
            Console.WriteLine("ConcreteDecoratorA.Operation()");
        }
    }

    /// <summary>
    /// The 'ConcreteDecoratorB' class
    /// </summary>
    class ConcreteDecoratorB : Decorator
    {
        public override void Operation()
        {
            base.Operation();
            AddedBehavior();
            Console.WriteLine("ConcreteDecoratorB.Operation()");
        }

        void AddedBehavior()
        {
        }
    }
}


~~~

###### Output
ConcreteComponent.Operation()  
ConcreteDecoratorA.Operation()  
ConcreteDecoratorB.Operation()  
