# Save Guard Documentation

  - SaveGuard offers a comprehensive solution to meet the needs of game save operations. In addition to making saving and loading games easy, it also provides the flexibility to create variables within a global container, further simplifying game data management. With its simple integration, flexible data management, and multiplatform support, SaveGuard is the ideal solution for developers seeking efficient and customizable saving and loading features in their games.

 ## Table of Contents

  <blockquote>
  <ol dir="auto">
    <li><a href="#Init">Introduction to SaveGuard:</a><br> 
      1.1 - <a href="#passob">Purpose:</a> <br> 
      1.2 - <a href="#passo1.2">Benefits:</a> <br> 
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

## 3. Adding variables to the GlobalDataContainer<a name="passob"></a>

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















