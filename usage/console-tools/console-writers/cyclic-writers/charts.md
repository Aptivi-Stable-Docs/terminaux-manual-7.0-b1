---
description: We have charts in the terminal!
icon: chart-line-up
---

# Charts

Presenting numbers, especially when comparing device performance benchmark numbers, can sometimes be clearer if you use a chart instead of a table. In order to use charts, you must specify at least the chart elements that can be described as an array of `ChartElement` class instances, which is usually set in the `Elements` property. You can create a new element like this:

```csharp
var element = new ChartElement()
{
    Name = "Element 1",
    Value = 12,
};
```

You must specify at least the name and the value to identify your element. However, elements can either have a random color (if the `Color` property isn't specified) or a specific color. It can also be hidden from view by enabling the `Hidden` property.

## Breakdown chart

This gives you either a horizontal stick or a vertical stick that describes what part of the whole stick has taken per each item. This describes a breakdown of several items that you want to present.

{% tabs %}
{% tab title="Horizontal with showcase" %}
```csharp
var chart = new BreakdownChart()
{
    Left = 1,
    Top = 2,
    InteriorWidth = 60,
    Showcase = true,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Horizontal with no showcase" %}
```csharp
var chart = new BreakdownChart()
{
    Left = 1,
    Top = 2,
    InteriorWidth = 60,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Vertical with showcase" %}
```csharp
var chart = new BreakdownChart()
{
    InteriorWidth = ConsoleWrapper.WindowWidth - 4,
    InteriorHeight = ConsoleWrapper.WindowHeight - 8,
    Left = 2,
    Top = 4,
    Showcase = true,
    Vertical = true,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Vertical with no showcase" %}
```csharp
var chart = new BreakdownChart()
{
    InteriorWidth = ConsoleWrapper.WindowWidth - 4,
    InteriorHeight = ConsoleWrapper.WindowHeight - 8,
    Left = 2,
    Top = 4,
    Vertical = true,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Bar chart

This gives you a horizontal bar chart that allows you to present various numbers in an amazing way for comparison.

{% tabs %}
{% tab title="Showcase" %}
```csharp
var chart = new BarChart()
{
    Left = 1,
    Top = 2,
    InteriorWidth = 60,
    Showcase = true,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="No showcase" %}
```csharp
var chart = new BarChart()
{
    Left = 1,
    Top = 2,
    InteriorWidth = 60,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Stick chart

This gives you a vertical bar chart that allows you to present various numbers in an amazing way for comparison.

{% tabs %}
{% tab title="Showcase" %}
```csharp
var chart = new StickChart()
{
    Left = 1,
    Top = 2,
    InteriorWidth = 60,
    InteriorHeight = 20,
    Showcase = true,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="No showcase" %}
```csharp
var chart = new StickChart()
{
    Left = 1,
    Top = 2,
    InteriorWidth = 60,
    InteriorHeight = 20,
    Elements =
    [
        new()
        {
            Name = "C#",
            Value = 80,
        },
        new()
        {
            Name = "Java",
            Value = 13,
        },
        new()
        {
            Name = "C++",
            Value = 6.9,
        },
        new()
        {
            Name = "Shell",
            Value = 0.1,
        },
    ]
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Stem and Leaf Chart

This shows you a stem and leaf chart that describes the breakdown of the numbers, with the following conditions:

* The stem either represents the digit of tens and greater (if the number is not a decimal) or the numeric part (if the number is a decimal)
* The leaf either represents the digit of ones (if the number is not a decimal) or the decimal part with the precision of two decimal digits (if the number is a decimal)

```csharp
var chart = new StemLeafChart()
{
    Elements =
    [
        789,
        7,
        13,
        14,
        14.4,
        14.8,
        15.4,
        16.7,
        16.8,
        17.26,
        17.4286,
        18.345,
    ],
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>

## Line Charts

This allows you to render a line chart that shows you rises and falls of a specific data to the console.

```csharp
var chart = new LineChart()
{
    InteriorWidth = ConsoleWrapper.WindowWidth - 4,
    InteriorHeight = ConsoleWrapper.WindowHeight - 8,
    Left = 2,
    Top = 4,
    Showcase = true,
    Elements =
    [
        new()
        {
            Name = "September 2023",
            Value = 34.92,
        },
        new()
        {
            Name = "October 2023",
            Value = 36.46,
        },
        new()
        {
            Name = "November 2023",
            Value = 37.63,
        },
        new()
        {
            Name = "December 2023",
            Value = 35.44,
        },
        new()
        {
            Name = "January 2024",
            Value = 32.27,
        },
        new()
        {
            Name = "February 2024",
            Value = 28.83,
        },
        new()
        {
            Name = "March 2024",
            Value = 26.26,
        },
        new()
        {
            Name = "April 2024",
            Value = 24.42,
        },
        new()
        {
            Name = "May 2024",
            Value = 23.34,
        },
        new()
        {
            Name = "June 2024",
            Value = 22.28,
        },
        new()
        {
            Name = "July 2024",
            Value = 21.31,
        },
        new()
        {
            Name = "August 2024",
            Value = 20.56,
        },
        new()
        {
            Name = "September 2024",
            Value = 19.86,
        },
    ],
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Wins and Losses

This chart allows you to visualize wins and losses for a company or for other things in your console.

```csharp
var chart = new WinsLosses()
{
    InteriorWidth = ConsoleWrapper.WindowWidth - 4,
    InteriorHeight = ConsoleWrapper.WindowHeight - 8,
    Left = 2,
    Top = 4,
    Showcase = true,
    Elements =
    [
        ("January 2023", new(){ Name = "Win", Value = 85.29 }, new(){ Name = "Loss", Value = 43.46 }),
        ("February 2023", new(){ Name = "Win", Value = 86.22 }, new(){ Name = "Loss", Value = 44.22 }),
        ("March 2023", new(){ Name = "Win", Value = 89.32 }, new(){ Name = "Loss", Value = 40.20 }),
        ("April 2023", new(){ Name = "Win", Value = 90.01 }, new(){ Name = "Loss", Value = 39.85 }),
        ("May 2023", new(){ Name = "Win", Value = 89.43 }, new(){ Name = "Loss", Value = 42.02 }),
        ("June 2023", new(){ Name = "Win", Value = 87.49 }, new(){ Name = "Loss", Value = 46.22 }),
    ],
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Pie charts

Pie charts visualize data, like all other data charts, but in a pie instead of the usual bars. It uses the values to calculate the arc angles of all elements to then display the whole pie to the console.

```csharp
var chart = new PieChart()
{
    Width = ConsoleWrapper.WindowWidth - 4,
    Height = ConsoleWrapper.WindowHeight - 8,
    Left = 2,
    Top = 4,
    Showcase = true,
    Elements =
    [
        new()
        {
            Name = "September 2023",
            Value = 34.92,
        },
        new()
        {
            Name = "October 2023",
            Value = 36.46,
        },
        new()
        {
            Name = "November 2023",
            Value = 37.63,
        },
        new()
        {
            Name = "December 2023",
            Value = 35.44,
        },
        new()
        {
            Name = "January 2024",
            Value = 32.27,
        },
        new()
        {
            Name = "February 2024",
            Value = 28.83,
        },
        new()
        {
            Name = "March 2024",
            Value = 26.26,
        },
        new()
        {
            Name = "April 2024",
            Value = 24.42,
        },
        new()
        {
            Name = "May 2024",
            Value = 23.34,
        },
        new()
        {
            Name = "June 2024",
            Value = 22.28,
        },
        new()
        {
            Name = "July 2024",
            Value = 21.31,
        },
        new()
        {
            Name = "August 2024",
            Value = 20.56,
        },
        new()
        {
            Name = "September 2024",
            Value = 19.86,
        },
    ],
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>

## Chart of Lines

This kind of chart demonstrates how an item has increased or decreased over either time periods or, more generally, iterations. It uses lines for such demonstration.

```csharp
var chart = new LinesChart()
{
    Width = ConsoleWrapper.WindowWidth - 4,
    Height = ConsoleWrapper.WindowHeight - 8,
    Left = 2,
    Top = 4,
    Showcase = true,
    Elements =
    [
        ("Android 12", [
            new() { Name = "3/2024", Value = 16.97 },
            new() { Name = "4/2024", Value = 16.42 },
            new() { Name = "5/2024", Value = 16.01 },
            new() { Name = "6/2024", Value = 15.80 }
        ]),
        ("Android 13", [
            new() { Name = "3/2024", Value = 26.26 },
            new() { Name = "4/2024", Value = 24.42 },
            new() { Name = "5/2024", Value = 23.34 },
            new() { Name = "6/2024", Value = 22.28 }
        ]),
        ("Android 14", [
            new() { Name = "3/2024", Value = 16.28 },
            new() { Name = "4/2024", Value = 20.38 },
            new() { Name = "5/2024", Value = 23.46 },
            new() { Name = "6/2024", Value = 25.67 }
        ]),
    ],
};
TextWriterRaw.WriteRaw(chart.Render());
```

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
