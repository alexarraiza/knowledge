# Flutter snippets that I found useful and use often

## Colors

### How to know if black or white contrasts a color

First way of doing it:

```dart
if (ThemeData.estimateBrightnessForColor(color) == Brightness.dark) {
    return Colors.white;
}
return Colors.black;
```

Second way of doing it:

```dart
color.computeLuminance() > 0.5 ? Colors.black : Colors.white
```
