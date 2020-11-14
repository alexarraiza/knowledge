# Flutter snippets that I found useful and use often

### How to know if black or white contrasts a color:

First way of doing it:

```
if (ThemeData.estimateBrightnessForColor(backgroundColor) == Brightness.dark) {
    return Colors.white;
}
return Colors.black;
```

Second way of doing it:

```
color.computeLuminance() > 0.5 ? Colors.black : Colors.white
```
