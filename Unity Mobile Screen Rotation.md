# Unity Mobile Screen Rotation

## Add the following code in the every game scene you want to be played in `Landscape Mode`.
### Make sure to add it in the `Start()` section of the `GameManager` script related to the game. To keep it trackable.

```csharp

  // Auto Rotate mobile screen to landscape right
  Screen.orientation = ScreenOrientation.LandscapeLeft;

```


## Add the following code in the every single game scene you want to be played in `Portrait Mode`.
### Make sure to add it in the `Start()` section of the `GameManager` script related to the game. To keep it trackable.

```csharp

    // Auto Rotate mobile screen to portrait
  Screen.orientation = ScreenOrientation.Portrait;

```
