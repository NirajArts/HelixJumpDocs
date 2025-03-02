# Helix Jump Project Documentation for integration

## Overview

This document provides an overview of the scripts and empty classes used for integrations communication in the Helix Jump project.

## Scripts and Classes

### HelixIntegrationComms.cs

**Filepath:** `Assets/Helix Jump/Scripts/Utility/HelixIntegrationComms.cs`

The `HelixIntegrationComms` class is responsible for handling communication and integration tasks within the Helix Jump game. It is designed as a singleton to ensure easy access to its methods from other scripts.

#### Properties

- `public static HelixIntegrationComms Instance { get; private set; }`
  - A static instance of the `HelixIntegrationComms` class to implement the singleton pattern.
- `public int scoreCount`
  - An integer to keep track of the player's score.

#### Methods

- `void Awake()`
  - Ensures that only one instance of the `HelixIntegrationComms` class exists. If an instance already exists, the new instance is destroyed.
- `void Start()`
  - Called when the script instance is being loaded. It initializes the `helixGameManager` and calls the `OnHelixGameStart` method.
- `public void OnHelixGameStart()`
  - Executed once when the gameplay starts. Logs "Helix Game Start" to the console and includes a placeholder for additional game start code.
- `public void OnHelixScore(int score)`
  - Executed every time the player increments the score. Updates the `scoreCount` variable with the new score and logs the score to the console. Includes a placeholder for additional score-related code.
- `public void OnHelixLevelComplete()`
  - Executed once when a level is failed. Logs "Helix Game Over" to the console and includes a placeholder for additional level completion code.

### HelixGameManager.cs

**Filepath:** `Assets/Helix Jump/Scripts/Utility/HelixGameManager.cs`

The `HelixGameManager` class is responsible for managing the game's state and logic. It interacts with the `HelixIntegrationComms` class to update the score and handle game events.

#### Properties

- `public int score`
  - An integer to keep track of the player's score.

#### Methods

- `void IncrementScore()`
  - Increments the player's score and calls the `OnHelixScore` method of the `HelixIntegrationComms` class.
- `void CompleteLevel()`
  - Handles the logic for completing a level and calls the `OnHelixLevelComplete` method of the `HelixIntegrationComms` class.

## Usage

In the `HelixIntegrationComms` class, the following methods are being called using the static `Instance` property. For example:

```csharp
HelixIntegrationComms.Instance.OnHelixGameStart();
HelixIntegrationComms.Instance.OnHelixScore(10);
HelixIntegrationComms.Instance.OnHelixLevelComplete();
```

### Integration

Open `HelixIntegrationComms.cs` script.
Following is the important part of the code, where the integration code can be included.

```csharp
// This method is excecuted once when the gameplay starts. Add game start code inside this method.
public void OnHelixGameStart()                      // This method is called from in the Start method.
{
Debug.Log("Helix Game Start");

// Add your code below

}

// This method is excecuted every time player increment the score. Add score code inside this method.
public void OnHelixScore(int score)                          // This method is called from HelixGameManager script.
{
    scoreCount = score;                                      // Get the score from HelixGameManager script and assign it to scoreCount variable.
    Debug.Log("Helix Score:" + scoreCount);
    // Add your code below

}

// This method is excecuted once when level is failed/completed. Add level end code inside this method.
public void OnHelixLevelComplete()                  // This method is called from HelixGameManager script.
{
    Debug.Log("Helix Game Over");
    // Add your code below

}
```

### Example with placeholder as `YourSDK`(an Imaginary sdk class).

#### When Game starts

```csharp
public void OnHelixGameStart()
{
    YourSDK.Initialize();
}
```

#### Updating score in realtime

```csharp
public void OnHelixScore(int score)
{
    scoreCount = score;
    YourSDK.UpdateScore(score);
}

```

#### When Game starts

```csharp
public void OnHelixLevelComplete()
{
    YourSDK.FinalizeScore(scoreCount);
}

```

### Menu Button Navigation

To integrate the menu button functionality, follow these steps:

1. Open the `Helix Jump Game.unity` scene.
2. Ito the scene hirarchy, navigate to the `--------UI--------` GameObject.
3. Expand the `Canvas` GameObject.
4. Expand the `EndPanel` GameObject.
5. Select the `Menu Button` GameObject.

The `Menu Button` should lead to the main menu scene. Copy the exact string for the main menu scene name and paste it into the given OnClick event, which calls the method `LoadCustomLevel(string levelName)` from the `HelixGameManager.cs`.

```csharp
public void LoadCustomLevel(string levelName)
{
    SceneManager.LoadScene(levelName);
}

```
