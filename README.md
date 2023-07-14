# Save Guard Documentation

  - SaveGuard offers a comprehensive solution to meet the needs of game save operations. In addition to making saving and loading games easy, it also provides the flexibility to create variables within a global container, further simplifying game data management. With its simple integration, flexible data management, and multiplatform support, SaveGuard is the ideal solution for developers seeking efficient and customizable saving and loading features in their games.

 ## Table of Contents

  <blockquote>
  <ol dir="auto">
    <li><a href="#Init">Introduction to SaveGuard:</a><br> 
      1.1 - <a href="#passob">Purpose:</a> <br> 
      1.2 - <a href="#passo1.2">Benefits:</a> <br> 
    <li><a href="#passob">Step-by-Step Guide on How to Use SaveGuard:</a><br> 
    <li><a href="#passoc">Adding variables to the GlobalDataContainer:</a><br> 
  <ol dir="auto">
<ol dir="auto">

</blockquote>

## 1. Introduction to SaveGuard:<a name="Init"></a>

  - SaveGuard is a powerful game save and load plugin designed to streamline the process of managing save data in PC and console games. With SaveGuard, developers can easily implement saving and loading functionality in their games, while also benefiting from the flexibility of creating variables within a global container.

 ### * 1.1. Purpose:<a name="passob"></a>

  - The primary purpose of SaveGuard is to provide an intuitive and efficient solution for game save and load operations. With SaveGuard, players can save their progress in the game and resume from where they left off, offering a more immersive and convenient gaming experience. Additionally, SaveGuard offers a unique feature: the ability to create variables within a global container.

### * 1.2. Benefits:<a name="passo1.2"></a>
  
  - Easy integration: SaveGuard offers a simple and fast integration into existing games. Using its SaveSystemFacility ActorComponent, developers can easily add saving and loading functionality to characters, environments, and other game elements.

  - Active User and controller recognition: SaveGuard's Active User system automatically identifies the active player and the controller being used, enabling personalized saving and loading for each player.

  - Flexible data management: SaveGuard allows developers to create and manage variables within a global container. With the GlobalData container, variables of different types such as bool, int, string, float, and more can be created. This eliminates the need for multiple separate variables, simplifying the process of storing and retrieving game information.

  - Multiple save slots: SaveGuard enables players to have multiple save slots, allowing them to save different progress or play with different characters. Managing these slots is straightforward and intuitive.

  - Data corruption protection: SaveGuard verifies and protects save files against corruption, ensuring that game data is reliably saved and loaded.

  - Multiplatform support: SaveGuard is compatible with PC and consoles, allowing developers to create games for various platforms without additional complications.
<blockquote>

SaveGuard offers a comprehensive solution to meet the needs of game save operations. In addition to making saving and loading games easy, it also provides the flexibility to create variables within a global container, further simplifying game data management. With its simple integration, flexible data management, and multiplatform support, SaveGuard is the ideal solution for developers seeking efficient and customizable saving and loading features in their games.
</blockquote>

## 2. Step-by-Step Guide on How to Use SaveGuard:<a name="passob"></a>
<blockquote>

  Before anything else, SaveGuard is primarily composed of C++ classes, although you can access most of its functions through Blueprints. However, it is recommended that you have familiarity with C++ in order to fully leverage the features that SaveGuard offers.

  Please remember to add the SaveGuard module to your Build.cs if you are using C++.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/ed649d85-50a5-41d6-a164-701cfb07c785)

 </blockquote> 

   - When you activate the SaveGuard plugin, it will create a new section in your ProjectSettings. In this section, you will choose the class for the MainSaveGame and the Slot (both come with default assets, but you can modify them based on your local changes).

   ![](https://github.com/quanticdawnstudio/GameBalanceDoc/blob/main/Ima/image.png)
   
Another thing you will need to do is change the default WorldSettings to **`SaveGuardWorldSettings`**.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/27aaf9a2-2fc4-438c-954f-38e53ed9c0e4)

"SaveGuard plugin consists of many classes, but the end user only needs to concern themselves with the **`SaveGuardSystem`**. I will now show you how it works.

Within the SaveGuardSystem class, you only need to concern yourself with two methods, and only if the current system does not allow you to include a variable accepted by the GlobalDataContainer.
The methods are **`SaveGame_Implementation()`** and **`LoadActiveGameSlot_Implementation()`**.
In both methods, there are default structures that should not be altered, but you can add new variables to be stored there. In both methods, there is a commented example that demonstrates how to do it.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/1ef33d5c-f415-41f4-9100-379cfe03de1d)

We will discuss in more detail the most important methods of this class later on.

The SaveGuardSystem class is a UObject, and it needs to be constructed to function properly. Let's go through the step-by-step process of how you can do that:

In your GameMode, after the BeginPlay, you will follow the example below (remember that you can do the same process in C++):

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/25360efc-0fa3-4ca1-8161-49b461e04258)

Once you have completed these steps, your game will initialize the MainSaveGame to create or load slots. However, before doing that, you need to learn how to add variables to the GlobalDataContainer.

## 3. Adding variables to the GlobalDataContainer<a name="passoc"></a>

  - In the first approach, when you want to add a variable, you can follow these steps:

  1 - When you want to add a variable, call the SaveGuardGISubsystem and get its SaveGuardObject.

  2 - Then, call the SetGameSlotInfo method on the SaveGuardObject and provide the parameter to add. Please note that the parameter will be added but not yet saved in the slot; you are simply adding the information.

Here's an example of how you can add a parameter using this approach:

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/c5f7002e-1bf7-415d-9bc9-8a25fd0606e4)

In the SetGameSlotInfo method, you can add the desired information as parameters.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/5f709828-f6b9-4c88-8fa2-aaece0238619)

With the GetParameterValue method, you can retrieve that value and link it to something internal in your project.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/429259fa-495c-4f46-bd39-a17199eae31b)

To change the value, simply call the ChangeGameSlotInfo method.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/3f299f0d-e4ef-41e4-a0d1-190d4f450add)

To remove a parameter, you can simply call the RemoveGameSlotInfo method.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/c48a2840-697a-4751-a7ba-fec0e55cdd11)

Please note that in order to save this information, you need to call the SaveTheGame method in the SaveGuardGISubsystem. You will see that it has an input for SlotIndex, where you can create something to set the Slot if it's the first save, or you can use the active Slot, as shown in the example below.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/468d03a3-c9fd-460d-8fe9-5a5d4fc1dc20)

<blockquote>
  
`To choose the maximum number of slots that your game can have, you will need to modify the default value in SSG_SaveSystem.`
![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/658fbe7e-475b-48ee-8aef-bfc54a5ace0e)

 </blockquote> 

Now let's move on to the easier way, which is using the **`SaveSystemFacility`**.

## 4. SaveSystemFacility:<a name="passod"></a>

The SaveSystemFacility is an ActorComponent that you can attach to any actor. It can perform various tasks and be activated in different ways, as we will see below.

In a collision volume, you added the SaveGuardFacility.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/e4ec6b0b-8bff-4eb8-ae6f-07271b376470)


Upon adding it, you can observe the existence of two UENUMs: Intention and ActivationMode. First, let's explore all the activation modes.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/4e086dd2-fb60-41de-8a59-5c0fabbded28)

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/f42a3d57-8ac1-42d8-86c3-ab872d17b4be)


### *4.1. Activation Modes:<a name="passoe"></a>

#### *4.1.1. Overlap:<a name="passof"></a>

  - When you select "Overlap" as the activation mode, it will automatically activate when it detects an overlap with the specified ActorName. Please note that the name must be entered correctly as recognized by the reflection system. To facilitate this, you can temporarily set the ShowNameOfActorWhenCollider variable to true. This way, when an actor overlaps with the volume, its name will be printed on the screen as a reference for you.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/3a71703c-ca1e-4e0a-9af2-f70cd4eb88a7)

#### *4.1.2. BeginPlay:<a name="passog"></a>

  - The second activation mode is "BeginPlay," which means it will be executed as soon as the game starts. Please note that this activation mode may sometimes cause a crash because, depending on the structure of your game, the SaveGuardSystem may not be initialized before the ActorComponent is activated.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/3f56785d-fe5d-4a0c-8ec7-715a5d09b068)

#### *4.1.3. Hit:<a name="passoh"></a>

  - The third activation method is very similar to "Overlap," with the only difference being that it detects "Hit" instead.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/3993b8f7-3d96-41de-9e38-7a530445797a)


#### *4.1.4. Other Method Activated:<a name="passoi"></a>

  - Lastly, there is the "OtherMethodActivated" option. If you want to activate it based on custom conditions, you can select "OtherMethodActivated" and specify when it will be activated by calling that method in the class.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/68a12c1c-eaca-4632-9a1a-da05a7368cbe)

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/2fa3d133-dc3a-4359-ab9a-bb4aa135aff0)

### *4.2. Intentions:<a name="passoj"></a>

Now that we have covered the activation modes, let's explore the intentions, which determine what we want the SaveSystemFacility to execute when activated.

#### *4.2.1. Send Parameter:<a name="passol"></a>

  - In the "Send Parameter" intention, you can send values to the GlobalDataContainer. It's worth noting that there is a bool variable called "SendAndSaveParameter" which allows you to both send the parameter and make it persistent. However, please note that the slot must already be valid in order to mark it as a bool.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/f2e771df-b8fb-4bf3-b664-7a65b3a4ef71)

#### *4.2.2. Change Parameter:<a name="passom"></a>

  - This intention works similarly to the previous one, with the difference that it is used to change the parameter. In the "ParameterNames" field, you will enter the name of the parameter, and in the "ParameterValues" field, you will enter the corresponding values.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/8ed3d40a-3c50-4831-bc22-20d8c87c23bf)

#### *4.2.3. Delete Parameter:<a name="passon"></a>

  - In the "Delete Parameter" intention, as the name suggests, you will remove a parameter from the GlobalDataContainer.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/476634ad-c1b8-4ae2-bdcd-f4f66e5fd4d3)

#### *4.2.4. Save Game:<a name="passoo"></a>

  - When you select "SaveGame" as the intention, it will by default save to the currently active slot. If it is the first time you are saving, you can set the "IsNewSlot" variable to true and provide the slot name.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/93631751-1158-49fa-b28d-192296069e87)

#### *4.2.5. Load Game:<a name="passop"></a>

  - In the "LoadGame" intention, it will load the game from a valid slot.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/af6568a4-9594-41d2-ae53-d35c44dbb107)

## 5. CheckPoint:<a name="passoq"></a>

  - The SaveGuard has a Checkpoint system. All you need to do is place the BP_Checkpoint in the map and adjust the size of the collision volume. Every time the character overlaps with the BP_Checkpoint, it will be registered in the WorldSettings.

To respawn a character, you can simply call the Respawn() function inside the SaveGuardGISubsystem. In this function, you need to provide the actor that will respawn and specify whether or not to perform a LoadGame.

![image](https://github.com/allanclrolemberg/SaveGuardDocumentation/assets/68305172/3c655339-d006-46f0-9c64-53e58980bb43)

<blockquote>
  
`Additional effects should be created based on the developer's creativity.`
 </blockquote> 





























