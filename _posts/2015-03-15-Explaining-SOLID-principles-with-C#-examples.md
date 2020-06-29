---
title: Explaining SOLID principles with C# examples
tags: [SOLID, C#, code, examples]
excerpt: SOLID are five basic principles for object-oriented programming and design. If applied, the solution is more likely to be easy to maintain and extend over time
lang: en
ref: SOLID
---

### What is SOLID?

[SOLID](http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29) are five basic principles for object-oriented programming and design. If applied, the solution is more likely to be easy to maintain and extend over time, which helps to create good software architecture. The SOLID acronym stands for:  

* **S** - Single responsibility principle  
* **O** - Open closed principle  
* **L** - Liskov substitution principle  
* **I** - Interface segregation principle  
* **D** - Dependency inversion principle

### Single responsability principle (SRP)

{% highlight c# %}
public class Engine
{
    public IgnitionResult Start(Starter starter, Battery battery)
    {
        //we would put code here to handle the logic for checking
        //whether or not the batter is charged
 
        //then we check the result of our logic
        if (battery.IsCharged)
        {
            //we could put logic here to handle
            //the actual ignition process
            return IgnitionResult.Success;
        }
        else
        {
            //uh oh! the battery is not charged
            //Failure!
            return IgnitionResult.Failure;
        }
    }
}
{% endhighlight %}

What is wrong with the above code? Should we really have all the battery logic inside the start method? and the ignition process? No, we shouldn't, it has multiple responsability.

Single responsabolity principle says that **a class should only have one responsability**. So the solution is moving the logic to the Starter and Battery classes and let the start method just start the engine.

{% highlight c# %}
public class Engine
{
    public IgnitionResult Start(Starter starter, Battery battery)
    {
        return starter.Start(battery);
    }
}
 
public class Starter
{ 
    public IgnitionResult Start(Battery battery)
    {
        //since the Battery class now contains that actual charge validation
        //logic, the Starter merely checks the value of that property
        //and the Battery takes care of the rest
        if (battery.IsCharged)
        {
            //we can put the ignition logic here
            return IgnitionResult.Success;
        }
        else
        {
            return IgnitionResult.Failure;
        }
    }
}
{% endhighlight %}

### Open-closed principle (OCP)

Following the same approach let's see what's wrong with this code:

{% highlight c# %}
class Customer
{
    private int _CustType;

    public int CustType
    {
        get { return _CustType; }
        set { _CustType = value; }
    }

    public double getDiscount(double TotalSales)
    {
            if (_CustType == 1)
            {
                return TotalSales - 100;
            }
            else
            {
                return TotalSales - 50;
            }
    }
}
{% endhighlight %}

If in the future we want to add more customer types, we will need to modify the class adding more ifs. This class should be **closed for modification open for extension**. We fix the code crating a derived class SilverCustomer that will override the discount method. And when we get another Customer type? another derived class!:

{% highlight c# %}
class Customer
{
    public virtual double getDiscount(double TotalSales)
    {
        return TotalSales;
    }
}

class SilverCustomer : Customer
{
    public override double getDiscount(double TotalSales)
    {
        return base.getDiscount(TotalSales) - 50;
    }
}
{% endhighlight %}

### Liskov substitution principle (LSP)

**Derived classes should be perfectly substitutable for their base classes**.

{% highlight c# %}
namespace SolidDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Apple apple = new Orange();
            Console.WriteLine(apple.GetColor());
        }
    }
 
    public class Apple
    {
        public virtual string GetColor()
        {
            return "Red";
        }
    }
 
    public class Orange : Apple
    {
        public override string GetColor()
        {
            return "Orange";
        }
    }
}
{% endhighlight %}

In the above code an Orange cannot replace an Apple so the code doesn't follow the Liskov principle. How can we fix it? Creating a generic base class for both fruits.

{% highlight c# %}
namespace SolidDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Fruit fruit = new Orange();
            Console.WriteLine(fruit.GetColor());
            fruit = new Apple();
            Console.WriteLine(fruit.GetColor());
        }
    }
 
    public abstract class Fruit
    {
        public abstract string GetColor();
    }
 
    public class Apple : Fruit
    {
        public override string GetColor()
        {
            return "Red";
        }
    }
 
    public class Orange : Apple
    {
        public override string GetColor()
        {
            return "Orange";
        }
    }
}
{% endhighlight %}

### Interface segregation principle (ISP)

The goal behind ISP is that **no client consuming an interface should be forced to depend on methods it does not use**. For example, you might have a class that implements an interface called IPersist.

{% highlight c# %}
public interface IPersist
{
	bool Save(BookingDetails reservation);
}

public class BookingLog : IPersist
{
	public bool Save(BookingDetails reservation)
	{
	   // saving code.
	   return true;
	}

	public void Log(BookingDetails reservation)
	{
	   // log code
	}

	public void SendLogNotification(BookingDetails reservation)
	{
	   // notifying code
	}
}
{% endhighlight %}

Now if we update IPersist to include the two new methods we have in ReservationLog class, it might be useful for more implementations of IPersist.

{% highlight c# %}
public interface IPersist
{
	bool Save(BookingDetails reservation);
	void Log(BookingDetails reservation);
	void SendLogNotification(BookingDetails reservation);
}
{% endhighlight %}

Well...that was a mistake, now we are forcing all the classes that implement IPersist to implement methods they are not using. We are clearly breaking the interface segregation principle. In fact, IPersist is not just persisting (saving) now is also logging.

{% highlight c# %}
public class BookingDatabase : IPersist
{
	public bool Save(BookingDetails reservation)
	{
	   // code to save on database
	   return true;
	}

	public void Log(BookingDetails reservation)
	{
	   throw new NotImplementedException();
	}

	public void SendLogNotification(ReservationDetails reservation)
	{
	   throw new NotImplementedException();
	}
}
{% endhighlight %}

To fix it is really easy, we need a new interface to separate responsabilities. And then only the classes that need to log will implement the new interface.

{% highlight c# %}
public interface ILog
{
   void Log(ReservationDetails reservation);
   void SendLogNotification(ReservationDetails reservation);
}

public class ReservationLog : IPersist, ILog
{% endhighlight %}

### Dependency inversion principle (DIP)

* **High-level modules should not depend on low-level modules. Both should depend on abstractions.**
* **Abstractions should not depend upon details. Details should depend upon abstractions.**

If we follow the Dependency inversion principle we will be able to build loosely coupled classes.

Let's see an example that violates the principle:

{% highlight c# %}
public class ProductService
{
    private ProductDiscount _productDiscount;
    private ProductRepository _productRepository;
 
    public ProductService()
    {
        _productDiscount = new ProductDiscount();
        _productRepository = new ProductRepository();
    }
 
    public IEnumerable<Product> GetProducts()
    {
        IEnumerable<Product> productsFromDataStore = _productRepository.FindAll();
        foreach (Product p in productsFromDataStore)
        {
            p.AdjustPrice(_productDiscount);
        }
        return productsFromDataStore;
    }
}
{% endhighlight %}

Notice high level modules call low level modules and instantiate their dependencies as they need them. Here ProductService calls ProductRepository, but before startintg it needs to create a new one up using the ‘new’ keyword. **Two dependencies are created in the constructor with the ‘new’ keyword. This breaks the Single Responsibility Principle as the class is forced to carry out work that’s not really its concern.**  

The ProductService is thus tightly coupled to those two concrete classes. Obtaining the correct pricing and data store strategy should not be the responsibility of the ProductService. And whenever those strategies change you must update the ProductService class. It is also difficult to test ProductService in isolation.

In order to remove the hard dependency we will inject in the constructor new abstractions that we will create for the discount and for the repository.

{% highlight c# %}
public class ProductService
{
    private IProductRepository _productRepository;
 
    public ProductService(IProductRepository productRepository)
    {
        _productRepository = productRepository;
    }
 
    public IEnumerable<Product> GetProducts(IProductDiscountStrategy productDiscount)
    {
        IEnumerable<Product> productsFromDataStore = _productRepository.FindAll();
        foreach (Product p in productsFromDataStore)
        {
            p.AdjustPrice(productDiscount);
        }
        return productsFromDataStore;
    }
}
{% endhighlight %}

Now anyone using Product Service will know they need an implementation of IProductRepository and IProductStrategy, but not an specific one.

### Conclusion

I hope the examples I picked were good enough to understand the SOLID principles. This was just an introduction, there is [much more detail available](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod).

