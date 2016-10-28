# Flyweight
### Structural Design Pattern

#### Обобщение
Flyweight Pattern-ът е шаблон, който се използва в обектно-ориентираното програмиране. Използва се за споделяне на сложни и бавни за създаване (ресурсоемки) обекти.

#### Структура
* Flyweight – интерфейсът на обектите;
* Concrete Flyweight;
* Flyweight Factory - осигурява достъпа до Flyweight обектите. Създава обект, ако конкретният още не е използван/създаден или връща вече създаден обект от същия тип;

#### Диаграма  
![pattern structure](../Images/flyweight-diagram.gif)

#### Demo
~~~c#
using System;
using System.Collections;

namespace FlyweightPattern
{
    /// <summary>
    /// Launcher startup class for Structural Flyweight Design Pattern.
    /// </summary>
    class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        static void Main()
        {
            // Arbitrary extrinsic state
            int extrinsicstate = 22;

            FlyweightFactory factory = new FlyweightFactory();

            // Work with different flyweight instances
            Flyweight fx = factory.GetFlyweight("X");
            fx.Operation(--extrinsicstate);

            Flyweight fy = factory.GetFlyweight("Y");
            fy.Operation(--extrinsicstate);

            Flyweight fz = factory.GetFlyweight("Z");
            fz.Operation(--extrinsicstate);

            UnsharedConcreteFlyweight fu = new
                UnsharedConcreteFlyweight();

            fu.Operation(--extrinsicstate);

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'FlyweightFactory' class
    /// </summary>
    class FlyweightFactory
    {
        private Hashtable flyweights = new Hashtable();

        // Constructor
        public FlyweightFactory()
        {
            flyweights.Add("X", new ConcreteFlyweight());
            flyweights.Add("Y", new ConcreteFlyweight());
            flyweights.Add("Z", new ConcreteFlyweight());
        }

        public Flyweight GetFlyweight(string key)
        {
            return ((Flyweight)flyweights[key]);
        }
    }

    /// <summary>
    /// The 'Flyweight' abstract class
    /// </summary>
    abstract class Flyweight
    {
        public abstract void Operation(int extrinsicstate);
    }

    /// <summary>
    /// The 'ConcreteFlyweight' class
    /// </summary>
    class ConcreteFlyweight : Flyweight
    {
        public override void Operation(int extrinsicstate)
        {
            Console.WriteLine("ConcreteFlyweight: " + extrinsicstate);
        }
    }

    /// <summary>
    /// The 'UnsharedConcreteFlyweight' class
    /// </summary>
    class UnsharedConcreteFlyweight : Flyweight
    {
        public override void Operation(int extrinsicstate)
        {
            Console.WriteLine("UnsharedConcreteFlyweight: " +
                              extrinsicstate);
        }
    }
}
~~~

###### Output
ConcreteFlyweight: 21  
ConcreteFlyweight: 20  
ConcreteFlyweight: 19  
UnsharedConcreteFlyweight: 18  
