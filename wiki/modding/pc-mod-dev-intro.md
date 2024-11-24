---
prev: false
next: false
description: Learn how to create your own PC mods!
---

# PC Mod Development Intro

_Learn how to get started writing your own PC Mods._

## Getting Started

::: warning
This guide is for making mods for the **PC** version of Beat Saber!

If you want to develop mods for the **Quest Standalone** version of the game, visit the [Quest Mod Development Guide](./quest-mod-dev-intro.md)

Make sure your game is modded before trying to make a mod.  
See instructions for [modding Beat Saber on PC.](/pc-modding.md)

This guide assumes you have a basic to intermediate understanding of C# and Unity.  
You may have difficulty understanding what is covered here if you do not have this foundation.
:::

Beat Saber is made in Unity 2019.3 using C# with .NET framework 4.6  
You will need to download the latest version of [Visual Studio Community](https://visualstudio.microsoft.com/).

## Setup Modding Tools

We will be using the BeatSaberModdingTools extension in this tutorial,
as it comes with modding templates and useful features.  
BeatSaberModdingTools is maintained by Zingabopp.
If you find the tools to be useful, consider throwing some support their way.

You can download it on their [GitHub](https://github.com/Zingabopp/BeatSaberTemplates/releases/latest).  
You will need to download `BeatSaberModdingTools.vsix`. (Expand the Assets dropdown if you cannot find it)

Once downloaded, open the `.vsix` and it will install itself as a Visual Studio Plugin.  
If you have any issues, consult the project's [README](https://github.com/Zingabopp/BeatSaberModdingTools#readme) and [WIKI](https://github.com/Zingabopp/BeatSaberModdingTools/wiki).

## Template setup

First, create a new project using the template.  
We are going to use the `BSIPA4 Plugin (Core)` template, and we'll be calling our mod `BSPlugin1`.
You should change the name to whatever you want to call your mod.

![Modding Template Select](/.assets/images/modding/modding-template-select.png 'Modding Template Select')  
![Modding Template Name](/.assets/images/modding/modding-template-name.png 'Modding Template Name')

You will then need to set your Beat Saber Directory in Visual Studio.
Follow the instructions [on the template readme](https://github.com/Zingabopp/BeatSaberModdingTools#how-to-use),
or see the screenshot below.

![Setup Beat Saber Directory](/.assets/images/modding/setup-bs-directory.png 'Setup Beat Saber Directory')

At this point, **try and build the project**, and it should automatically find the
references for you and the build should succeed.

If your build does not succeed, check that you don't have any missing references.

::: tip
BeatSaberModdingTools will automatically handle references. If your references could not be found, [double-check the instructions](https://github.com/Zingabopp/BeatSaberModdingTools#how-to-use).

If you need to manually add references, right click on `References` in the Project folder, then `Beat Saber Reference Manager...`.
Select your references, then click "Apply".

You can find more information about the reference manager [here](https://github.com/Zingabopp/BeatSaberModdingTools/wiki/Adding-References).
:::

## Inspecting the Code

You should have 5 files open automatically with the template.

| Filename                 | About                                                                          |
| ------------------------ | ------------------------------------------------------------------------------ |
| `manifest.json`          | Information about your mod for BSIPA.                                          |
| `Plugin.cs`              | The main file that is loaded for your mod.                                     |
| `AssemblyInfo.cs`        | File information about your mod. This is mostly managed by Modding Tools.      |
| `PluginConfig.cs`        | A template for enabling config for your mod. This is commented out by default. |
| `BSPlugin1Controller.cs` | A generic MonoBehaviour for your mod.                                          |

### Edit your mod's Manifest

Fill out the `manifest.json` file with your information.  
The `name` and `id` keys are used to identify your mod.
The ID should match the ID used when uploading your mod to BeatMods.

::: warning
Do **not** remove the dependency on BSIPA. As of BSIPA v4.1 this is required for your mod to load.
:::

## Compiling

Build your plugin with `Build -> Build Solution` or <kbd>CTRL + SHIFT + B</kbd>  
Your compiled DLL should automatically be copied to the `Plugins` folder in your Beat Saber directory!
This will be done for both debug and release builds.

::: tip NOTE
When you are ready to release your mod, select the `Release` option to make a Release build of your mod.

Building in Release mode will generate a packaged `.zip` file ready to upload to BeatMods.
:::

## Testing your mod in-game

To test if your mod is loaded in-game, you will need to launch Beat Saber with the BSIPA Console enabled.
Add `--verbose` as a launch argument and run the game.  
For more information on launch arguments, see [here](./#launch-args).

When you launch the game, you should see BSIPA load your mod in the console window.

![Testing console screenshot](/.assets/images/modding/testing-console.png 'Testing console screenshot')

## Next Steps

Here are some useful resources in continuing your modding career.

- If you need help with developing mods, you can ask in `#pc-mod-dev` on the [BSMG Discord](https://discord.gg/beatsabermods).
- If you want to decompile code, check out [dnSpy](https://github.com/dnSpy/dnSpy/releases)
- See the BSIPA Documentation for more information about the [configuration system](https://bsmg.github.io/BeatSaber-IPA-Reloaded/tags/4.1.3/articles/start-dev.html#configuring-your-plugin).
- If you need to patch the game's code for your mod, you should use [Harmony](https://github.com/pardeike/Harmony#readme).
  The `0Harmony.dll` is already installed for modded games.
- For experienced developers, you may be interested in learning about Zenject, the Dependency Injection system used heavily
  by Beat Saber. [SiraUtil](https://github.com/Auros/SiraUtil#readme) is a library that allows you to easily hook
  into this system.
