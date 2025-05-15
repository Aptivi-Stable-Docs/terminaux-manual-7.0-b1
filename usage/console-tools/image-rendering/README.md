---
description: Images in the terminal!
icon: image
---

# Image Rendering

In addition to all of the features that Terminaux provides, it also provides an extra library that your terminal applications can use, called `Terminaux.Images`, that supports Windows, macOS, and Linux. It doesn't use [`System.Drawing`](https://learn.microsoft.com/en-us/dotnet/core/compatibility/core-libraries/6.0/system-drawing-common-windows-only) due to its exclusivity to Windows.

With the help of ImageMagick, you can render the images to your console, as long as your console's dimensions is greater than the requested width and height of the image. Using the `ImageProcessor` class, you can either use a file path, a byte array, a MagickImage instance, or a stream that contains image data that ImageMagick can process, which you can find a list of suppored extensions [here](https://imagemagick.org/script/formats.php).

Here are the examples of how to render a picture to column 5 row 3 of the console with the image width of 40 and height of 20:

{% code title="Using a file path" lineNumbers="true" %}
```csharp
string rendered = ImageProcessor.RenderImage("path/to/file", 40, 20, 4, 2);
TextWriterRaw.WriteRaw(rendered);
```
{% endcode %}

{% code title="Using a byte stream" lineNumbers="true" %}
```csharp
byte[] bytes = File.ReadAllBytes("path/to/file");
string rendered = ImageProcessor.RenderImage(bytes, 40, 20, 4, 2);
TextWriterRaw.WriteRaw(rendered);
```
{% endcode %}

{% code title="Using a stream" lineNumbers="true" %}
```csharp
var imageStream = File.OpenRead("path/to/file");
string rendered = ImageProcessor.RenderImage(imageStream, 40, 20, 4, 2);
TextWriterRaw.WriteRaw(rendered);
```
{% endcode %}

{% code title="Using a MagickImage instance" lineNumbers="true" %}
```csharp
MagickImage myMagickImage = (...)
string rendered = ImageProcessor.RenderImage(myMagickImage, 40, 20, 4, 2);
TextWriterRaw.WriteRaw(rendered);
```
{% endcode %}

{% hint style="info" %}
You don't need to install ImageMagick to your system; it's embedded in the Magick.NET package!
{% endhint %}

You can demonstrate this by running the `Terminaux.Console` app (build from source) and running the `RenderImage` test fixture:

<figure><img src="../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
In some cases, you don't actually need to specify the left and the top position of the upper left corner of the image, such as interactive TUIs that print text and informational boxes.
{% endhint %}

You can also get colors for each pixel in the image using a file path, a byte array, or a stream that contains image data that ImageMagick can process, using the `GetColorsFromImage()` function that returns a 2D array representing the full image width and height.

{% hint style="info" %}
Depending on the image size, it may take time to process the color data for each pixel. For the best results, try to make your images as small as possible.
{% endhint %}

If you don't want to provide an image file, stream, or array of bytes, or if you're making a UI concept, you can use the placeholder graphic renderer that can be easily be used like this:

{% code title="Rendering a placeholder" lineNumbers="true" %}
```csharp
string rendered = ImageProcessor.RenderImage(40, 20, 4, 2);
TextWriterRaw.WriteRaw(rendered);
```
{% endcode %}

{% hint style="info" %}
You can optionally specify a background color that the image renderer will use to render a transparent image with the background color that you've specified by passing a Color instance to the last argument of the `RenderImage()` functions. If not specified, it'll use your current background color.
{% endhint %}

{% hint style="info" %}
You can also use the `OpenImage()` function, which returns a `MagickImage` instance. It accepts either a file path, an array of bytes, or a stream.
{% endhint %}
