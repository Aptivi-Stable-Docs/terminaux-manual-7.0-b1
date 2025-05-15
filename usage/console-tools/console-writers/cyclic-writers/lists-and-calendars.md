---
description: Listing items in your console
icon: list-ul
---

# Lists and Calendars

## Tables and Calendars

This allows you to render a table that consists of rows and columns to the terminal. You can use the cell options variable to configure various cells, such as colors. Calendars internally use the table renderer to render the core elements of a calendar, and they support non-Gregorian calendars.

{% tabs %}
{% tab title="Normal tables" %}
```csharp
var Rows = new string[,]
{
    { "Ubuntu Version", "Release Date", "Support End", "ESM Support End" },
    { "12.04 (Precise Pangolin)", new DateTime(2012, 4, 26).ToString(), new DateTime(2017, 4, 28).ToString(), new DateTime(2019, 4, 28).ToString() },
    { "14.04 (Trusty Tahr)", new DateTime(2014, 4, 17).ToString(), new DateTime(2019, 4, 25).ToString(), new DateTime(2024, 4, 25).ToString() },
    { "16.04 (Xenial Xerus)", new DateTime(2016, 4, 21).ToString(), new DateTime(2021, 4, 30).ToString(), new DateTime(2026, 4, 30).ToString() },
    { "18.04 (Bionic Beaver)", new DateTime(2018, 4, 26).ToString(), new DateTime(2023, 4, 30).ToString(), new DateTime(2028, 4, 30).ToString() },
    { "20.04 (Focal Fossa)", new DateTime(2020, 4, 23).ToString(), new DateTime(2025, 4, 25).ToString(), new DateTime(2030, 4, 25).ToString() },
    { "22.04 (Jammy Jellyfish)", new DateTime(2022, 4, 26).ToString(), new DateTime(2027, 4, 25).ToString(), new DateTime(2032, 4, 25).ToString() },
    { "24.04 (Noble Numbat)", new DateTime(2024, 4, 25).ToString(), new DateTime(2029, 4, 25).ToString(), new DateTime(2034, 4, 25).ToString() },
};
var misc = new Table()
{
    Rows = Rows,
    Header = true,
    Left = 4,
    Top = 2,
    InteriorWidth = ConsoleWrapper.WindowWidth - 7,
    InteriorHeight = ConsoleWrapper.WindowHeight - 5,
    Settings =
    [
        new CellOptions(2, 2) { CellColor = ConsoleColors.Red, CellBackgroundColor = ConsoleColors.DarkRed, ColoredCell = true },
        new CellOptions(3, 2) { CellColor = ConsoleColors.Red, CellBackgroundColor = ConsoleColors.DarkRed, ColoredCell = true },
        new CellOptions(4, 2) { CellColor = ConsoleColors.Red, CellBackgroundColor = ConsoleColors.DarkRed, ColoredCell = true },
        new CellOptions(2, 3) { CellColor = ConsoleColors.Red, CellBackgroundColor = ConsoleColors.DarkRed, ColoredCell = true },
        new CellOptions(3, 3) { CellColor = ConsoleColors.Red, CellBackgroundColor = ConsoleColors.DarkRed, ColoredCell = true },
        new CellOptions(4, 3) { CellColor = ConsoleColors.Red, CellBackgroundColor = ConsoleColors.DarkRed, ColoredCell = true },
        new CellOptions(2, 4) { CellColor = ConsoleColors.Yellow, CellBackgroundColor = ConsoleColors.Olive, ColoredCell = true },
        new CellOptions(3, 4) { CellColor = ConsoleColors.Yellow, CellBackgroundColor = ConsoleColors.Olive, ColoredCell = true },
        new CellOptions(2, 5) { CellColor = ConsoleColors.Yellow, CellBackgroundColor = ConsoleColors.Olive, ColoredCell = true },
        new CellOptions(3, 5) { CellColor = ConsoleColors.Yellow, CellBackgroundColor = ConsoleColors.Olive, ColoredCell = true },
    ]
};
TextWriterRaw.WriteRaw(misc.Render());
```

<figure><img src="../../../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Calendar (Gregorian)" %}
```csharp
var calendar = new Calendars()
{
    Year = DateTime.Now.Year,
    Month = DateTime.Now.Month,
    Left = 4,
    Top = 2,
    InteriorWidth = 40,
    InteriorHeight = 10,
};
TextWriterRaw.WriteRaw(calendar.Render());
```

<figure><img src="../../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Calendar (Hijri)" %}
```csharp
var culture = new CultureInfo("ar");
culture.DateTimeFormat.Calendar = new HijriCalendar();
var calendar = new Calendars()
{
    Year = DateTime.Now.Year,
    Month = DateTime.Now.Month,
    Left = 4,
    Top = 2,
    InteriorWidth = 40,
    InteriorHeight = 10,
    Culture = culture
};
TextWriterRaw.WriteRaw(calendar.Render());
```

<figure><img src="../../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## `ListEntry` and `Listing`

These renderables help you create a rendered list of items easily. `Listing` accepts any enumerable with optional functions that convert individual items to string representations, while `ListEntry` is used to render a single entry in the key and the value form.

{% tabs %}
{% tab title="Lists" %}
```csharp
var misc = new Listing()
{
    Objects = new string[]
    {
        "One",
        "Two",
        "Three",
        "Four",
    }
};
TextWriterRaw.WriteRaw(misc.Render());
```

<figure><img src="../../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Dictionaries" %}
```csharp
var misc = new Listing()
{
    Objects = new Dictionary<string, int>
    {
        { "Nitrocid KS", 264 },
        { "VisualCard", 221 },
        { "Terminaux", 214 },
    }
};
TextWriterRaw.WriteRaw(misc.Render());
```

<figure><img src="../../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Leveled lists" %}
```csharp
var misc = new ListEntry()
{
    Entry = "Commit count for September 2024",
    Value = "699",
};
var misc2 = new ListEntry()
{
    Entry = "Nitrocid KS",
    Value = "264",
    Indentation = 1,
};
var misc3 = new ListEntry()
{
    Entry = "VisualCard",
    Value = "221",
    Indentation = 1,
};
var misc4 = new ListEntry()
{
    Entry = "Terminaux",
    Value = "214",
    Indentation = 1,
};
var misc5 = new ListEntry()
{
    Entry = "Commit count for October 2024",
    Value = "536",
};
var misc6 = new ListEntry()
{
    Entry = "Terminaux",
    Value = "216",
    Indentation = 1,
};
var misc7 = new ListEntry()
{
    Entry = "VisualCard",
    Value = "208",
    Indentation = 1,
};
var misc8 = new ListEntry()
{
    Entry = "Textify",
    Value = "112",
    Indentation = 1,
};
TextWriterRaw.WritePlain(misc.Render());
TextWriterRaw.WritePlain(misc2.Render());
TextWriterRaw.WritePlain(misc3.Render());
TextWriterRaw.WritePlain(misc4.Render());
TextWriterRaw.WritePlain(misc5.Render());
TextWriterRaw.WritePlain(misc6.Render());
TextWriterRaw.WritePlain(misc7.Render());
TextWriterRaw.WritePlain(misc8.Render());
```

<figure><img src="../../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Selection

You can render a list of selection elements using this renderable. This uses a part of the selection style renderer code.

{% tabs %}
{% tab title="Single" %}
```csharp
var finalSelections = new InputChoiceInfo[]
{
	new("Choice one", "The first choice"),
	new("Choice two", "The second choice"),
	new("Choice three", "The third choice"),
	new("Choice four", "The fourth choice"),
	new("Choice five", "The fifth choice"),
	new("Choice six", "The sixth choice"),
	new("Choice seven", "The seventh choice"),
	new("Choice eight", "The eighth choice"),
};
var selections = new Selection(finalSelections)
{
	Left = 2,
	Top = 1,
	CurrentSelection = 2,
	Height = 7,
	Width = 30,
};
TextWriterRaw.WriteRaw(selections.Render());
```

<figure><img src="../../../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Multiple" %}
```csharp
var finalSelections = new InputChoiceInfo[]
{
	new("Choice one", "The first choice"),
	new("Choice two", "The second choice"),
	new("Choice three", "The third choice"),
	new("Choice four", "The fourth choice"),
	new("Choice five", "The fifth choice"),
	new("Choice six", "The sixth choice"),
	new("Choice seven", "The seventh choice"),
	new("Choice eight", "The eighth choice"),
};
var selections = new Selection(finalSelections)
{
	Left = 2,
	Top = 1,
	CurrentSelection = 2,
	CurrentSelections = [0, 2, 4, 6],
	Height = 7,
	Width = 30,
};
TextWriterRaw.WriteRaw(selections.Render());
```

<figure><img src="../../../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
