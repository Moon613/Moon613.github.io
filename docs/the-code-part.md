# Triggering Your Achievement

## How to trigger your achievement

This is very simple to do, but from this point forward you *must* know how to write your own code mods for Rain World.

First, you must reference this mod's DLL file, which contains all the code for the mod. You can find it in `*Your Steam Install Directory*/SteamLibrary/steamapps/workshop/content/312520/*FolderHere*/plugins` if you subscribed to it on the Steam Workshop. Once you have added a reference to it in your project, you can trigger your achievement by calling `Achievement.TriggerAchievement(RainWorld, string)`, which is in the `RWAchievements` namespace. This requires the current RainWorld instance to be passed to it, and the ID of your achievement as a string. It will then become permanently unlocked and available to view in the achievement gallery. This can be done at any time, and keeping track of the requirements to unlock a specific acheivement, or when and where to trigger an unlock, is left up to the individual mods to do.

Triggering your achievement also displays a notification to the user in the bottom right of the screen, in a style meant to imitate Steam's achievement notification system. However, this can be changed with...

## Custom Achievement Notifications

Included is the ability to completely customize what achievement notifications look like, so you can spice them up however you want!

This is also pretty simple to do. All you need to do is create a new class that inherits from the abstract `Popup` class, which is also in the `RWAchievements` namespace. This class is very minimal, so as to not restrict any customization that may be desired. Once you have made your class, you can do anything you like in the `Update` and `GrafUpdate` methods. The Update method is like the Player's Update method, in that it gets called 40 times a second and is a good place for normal logic. The GrafUpdate method is where graphics logic should go, since it is called once a frame.

Now to use your class with your achievement use the overloaded version of the previous method, `Achievement.TriggerAchievement<T>(RainWorld, string)`, where `T` is the name of your class. Your popup will now be used instead of the default. This mod will manage calling the Update and GrafUpdate methods for it. If you do not use a class that inherits from `Popup`, there will be a compiler-time error with your code and it will not compile.