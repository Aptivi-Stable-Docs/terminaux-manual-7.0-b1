---
description: '"When will I be able to try out Terminaux 7.0?" "Soon, just please wait."'
icon: bars-progress
---

# Progress Bars

Progress bars describe how much of a progress was done for the current task. You can make the progress bar either with text or without text. Progress bars can either be determinate (at which you can know the progress) or indeterminate (at which the process is not determined)

## **Progress bar with text**

This writer allows you to show a progress bar while allowing you to describe what is going on during the process.

{% tabs %}
{% tab title="Determinate" %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var progressBar = new ProgressBar(
    "This is the test progress bar that contains a scrolling marquee.", 0, 100)
{
    Width = ConsoleWrapper.WindowWidth - 8,
};
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(progressBar.Render);
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Indeterminate" %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var progressBar = new ProgressBar(
    "This is the test progress bar that contains a scrolling marquee.", 0, 100)
{
    Width = ConsoleWrapper.WindowWidth - 8,
    Indeterminate = true,
};
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(progressBar.Render);
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## **Progress bar without text**

This writer allows you to show a progress bar without any text.

{% tabs %}
{% tab title="Determinate" %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var progressBar = new ProgressBarNoText(0, 100)
{
    Width = ConsoleWrapper.WindowWidth - 8,
};
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(progressBar.Render);
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Indeterminate" %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var progressBar = new ProgressBarNoText(0, 100)
{
    Width = ConsoleWrapper.WindowWidth - 8,
    Indeterminate = true,
};
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(progressBar.Render);
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## **Simple progress bars**

If you want to just print a progress bar either horizontally or vertically without any extra elements, you can use the `SimpleProgress` renderable.

{% tabs %}
{% tab title="Determinate, horiz." %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var progressBar = new SimpleProgress(0, 100)
{
    Width = ConsoleWrapper.WindowWidth - 8,
};
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(progressBar.Render);
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Indeterminate, horiz." %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var progressBar = new SimpleProgress(0, 100)
{
    Width = ConsoleWrapper.WindowWidth - 8,
    Indeterminate = true,
};
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(progressBar.Render);
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Determinate, vert." %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var container = new Container();
var progressBar1 = new SimpleProgress(0, 100)
{
    Height = 20,
    Vertical = true,
};
container.AddRenderable("Progress bar 1", progressBar1);
container.SetRenderablePosition("Progress bar 1", new(4, 2));

// Render them all
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.AddDynamicText(() => ContainerTools.RenderContainer(container));
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar1.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Indeterminate, vert." %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var container = new Container();
var progressBar1 = new SimpleProgress(0, 100)
{
    Height = 20,
    Vertical = true,
    Indeterminate = true,
};
container.AddRenderable("Progress bar 1", progressBar1);
container.SetRenderablePosition("Progress bar 1", new(4, 2));

// Render them all
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the progress bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.AddDynamicText(() => ContainerTools.RenderContainer(container));
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the progress bar until it's full
    for (int progress = 0; progress < 100; progress++)
    {
        progressBar1.Position = progress;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Slider

This writer allows you to write a slider that moves according to the minimum position, the current position, and the maximum position. This is useful for slider bars.

{% tabs %}
{% tab title="Horizontal" %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var container = new Container();
var slider1 = new Slider(0, 0, 100)
{
    Width = 40,
};
var slider2 = new Slider(0, 0, 10)
{
    Width = 40,
};
var slider3 = new Slider(0, 0, 4)
{
    Width = 40,
};
container.AddRenderable("Slider bar 1", slider1);
container.SetRenderablePosition("Slider bar 1", new(4, ConsoleWrapper.WindowHeight - 3));
container.AddRenderable("Slider bar 2", slider2);
container.SetRenderablePosition("Slider bar 2", new(4, ConsoleWrapper.WindowHeight - 2));
container.AddRenderable("Slider bar 3", slider3);
container.SetRenderablePosition("Slider bar 3", new(4, ConsoleWrapper.WindowHeight - 1));

// Render them all
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the slider bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(() => ContainerTools.RenderContainer(container));
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the slider bar until it's full
    for (int sliderPos1 = 0, sliderPos2 = 0, sliderPos3 = 0; sliderPos1 < 100; sliderPos1++, sliderPos2++, sliderPos3++)
    {
        if (sliderPos2 == 10)
            sliderPos2 = 0;
        if (sliderPos3 == 4)
            sliderPos3 = 0;
        slider1.Position = sliderPos1;
        slider2.Position = sliderPos2;
        slider3.Position = sliderPos3;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Vertical" %}
```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 50,
};
var container = new Container();
var slider4 = new Slider(0, 0, 100)
{
    Height = 10,
    Vertical = true,
};
var slider5 = new Slider(0, 0, 10)
{
    Height = 10,
    Vertical = true,
};
var slider6 = new Slider(0, 0, 4)
{
    Height = 10,
    Vertical = true,
};
container.AddRenderable("Slider bar 4", slider4);
container.SetRenderablePosition("Slider bar 4", new(4, 2));
container.AddRenderable("Slider bar 5", slider5);
container.SetRenderablePosition("Slider bar 5", new(6, 2));
container.AddRenderable("Slider bar 6", slider6);
container.SetRenderablePosition("Slider bar 6", new(8, 2));

// Render them all
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the slider bar
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 1);
    stickScreenPart.AddDynamicText(() => ContainerTools.RenderContainer(container));
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();

    // Finally, increment the slider bar until it's full
    for (int sliderPos1 = 0, sliderPos2 = 0, sliderPos3 = 0; sliderPos1 < 100; sliderPos1++, sliderPos2++, sliderPos3++)
    {
        if (sliderPos2 == 10)
            sliderPos2 = 0;
        if (sliderPos3 == 4)
            sliderPos3 = 0;
        slider4.Position = sliderPos1;
        slider5.Position = sliderPos2;
        slider6.Position = sliderPos3;
        Thread.Sleep(100);
    }
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Spinner

This writer allows you to write a spinner that moves according to the number of times that the spinner has rendered. This is useful for progress bars and others.

```csharp
var stickScreen = new Screen()
{
    CycleFrequency = 80,
};
var marquee = BuiltinSpinners.BouncingBar;
try
{
    // First, clear the screen
    ColorTools.LoadBack();

    // Then, show the counter
    var stickScreenPart = new ScreenPart();
    stickScreenPart.Position(4, ConsoleWrapper.WindowHeight - 2);
    stickScreenPart.AddDynamicText(marquee.Render);
    stickScreen.AddBufferedPart("Test", stickScreenPart);
    ScreenTools.SetCurrent(stickScreen);
    ScreenTools.SetCurrentCyclic(stickScreen);
    ScreenTools.StartCyclicScreen();
    Input.ReadKey();
}
catch (Exception ex)
{
    InfoBoxModalColor.WriteInfoBoxModal($"Screen failed to render: {ex.Message}");
}
finally
{
    ScreenTools.StopCyclicScreen();
    ScreenTools.UnsetCurrent(stickScreen);
    ColorTools.LoadBack();
}
```

<figure><img src="../../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>
