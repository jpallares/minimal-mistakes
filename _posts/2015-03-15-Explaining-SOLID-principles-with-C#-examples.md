---
layout: post
title: Explaining SOLID principles with C# examples
tags: [SOLID, C#, code, examples]
comments: true
share: true
---

###What is SOLID?

[SOLID](http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29) are five basic principles for object-oriented programming and design. If applied, the solution is mroe likely to be easy to maintain and extend over time. whichhelp to create good software architecture. The SOLID acronym stands for:  

* **S** - Single responsibility principle  
* **O** - Open closed principle  
* **L** - Liskov substitution principle  
* **I** - Interface segregation principle  
* **D** - Dependency inversion principle

###**S**ingle responsability principle (SRP)

{% highlight c# %}
public class ServiceStation
{
    public void OpenGate()
    {
        //Open the gate if the time is later than 9 AM
    }
 
    public void DoService(Vehicle vehicle)
    {
        //Check if service station is opened and then
        //complete the vehicle service
    }
 
    public void CloseGate()
    {
        //Close the gate if the time has crossed 6PM
    }
}
{% endhighlight %}

What is wrong with the above code? The service station should not care about the Gate. It has multiple responsability.

Single responsabolity principle says that a class should only have one responsability. So the solution is creating a new class that will take care of the gate, and an interface to inject it. This way we prevent having coupled code.

{% highlight c# %}
public class ServiceStation
{
    IGateUtility _gateUtility;
 
    public ServiceStation(IGateUtility gateUtility)
    {
        this._gateUtility = gateUtility;
    }
    public void OpenForService()
    {
        _gateUtility.OpenGate();
    }
 
    public void DoService()
    {
        //Check if service station is opened and then
        //complete the vehicle service
    }
 
    public void CloseForDay()
    {
        _gateUtility.CloseGate();
    }
}
 
public class ServiceStationUtility : IGateUtility
{
    public void OpenGate()
    {
        //Open the shop if the time is later than 9 AM
    }
 
    public void CloseGate()
    {
        //Close the shop if the time has crossed 6PM
    }
}
 
 
public interface IGateUtility
{
    void OpenGate();
    void CloseGate();
}
{% endhighlight %}

###Open-closed principle (OCP)

Following the same approach let's see what wrong with this code:

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
{% highlight c# %}

{% endhighlight %}
{% highlight c# %}

{% endhighlight %}

>![Visual Studio Shortcuts](../images/VisualStudioShortcuts.png "Visual Studio Shortcuts")

ReSharper is a renowned productivity tool that makes Microsoft Visual Studio a much better IDE. Thousands of .NET developers worldwide wonder how they’ve ever lived without ReSharper’s code inspections, automated code refactorings, blazing fast navigation, and coding assistance.
{: .notice}
