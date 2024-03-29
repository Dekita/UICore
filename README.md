NOTE: The UICore and this documentation is a WIP, be gentle <3 

# HL UICore
Various Widgets, Components, and Helper Functions for Hogwarts Legacy UI Modding

## HL Modding Setup

See: https://modding.wiki/en/hogwartslegacy/developers/PhoenixUProjGuide for initial uproject and custom engine setup information. This is NOT optional. Do this first!!

Before you use the UICore, you should use UModel to extract all texture images from 
`Phoenix/Content/UI` and add them to the uproject for your mods. UModel is recommended over FModel for textures as it takes a few seconds for the entire game compared to FModels seconds per texture. Follow the directions for UModel over on the [modding wiki 102 tutorial](https://modding.wiki/en/hogwartslegacy/developers/hlblueprint102) to get the correct setup for HL.

Once all texture files are exported with UModel, drag and drop the exported UI folder into your projects 'Content' directory within unreal editor. This will begin importing all of the textures and may take a few minutes. You might see a lot of errors flash across your screen from being unable to import all the assets. This should be fine. 


Once all the game textures are in your project, click file->save all. 

Next, locate your project files in windows explorer, and OPEN the UICore Content folder. From the UICore folder, first copy the UI folder/files into your projects folder. This should merge the two Content folders together and may overwrite some files. 

After the UI folder is added to your project copy the DekitaRPG folder. This will add the UICore's custom elements. The reason we do this in two steps, is to ensure that the references from the DekitaRPG files do not break by being added before the referenced files within the UI folder exist.

You should again save all, then close and reopen your project to make sure everything has been correctly imported and saved. 

You are now ready to begin creating ui mods using the UICore as a base. 

## Using UICore

At most, you should add 1 widget to the game viewport, this widget will be your main `UI` widget, which contains the various other component widgets that your ui will use. For this example, create a widget named `UI_MyAwesomeHUD`, once created, open the widget, navigate to the widget blueprint graph, and then class settings. Change the widget parent class to `Screen`. This is the most important step, as it allows our UI widget access to the InputAction keybindings that the game uses. 

Once your main UI widget has been created, there are a few components you should add as a minimum. First, delete all existing widgets (usually a single canvas panel by default), then add a `UIContainer` in its place. This provides named slots for a fullscreen background area, as well as a centered content area that will ensure your ui content scales properly on different screen sizes. 

You probably want some fancy animated background in your ui now, so search for a `W_AnimatedBG` and add one into the UIContainers BGArea slot. You can configure some basic settings for the animated bg, for example a fullscreen or side panel smoke effect. 

Next, search for, and add a `HorizontalBox` to your UIContainers ContentArea. This allows us to split the scalable ui area into segments, usually thirds or halfs (if your wanting to keep in line with HL default screens). 

You are now ready to start designing your UI using the other various components from the UICore. 

Before that though, you should test to make sure your ui displays in game as intended. Within your main mod logic actor, add your `UI_MyAwesomeHUD` to the game viewport, ideally on some key press, and package your mod. 

Once you have confirmed that your UI is indeed shown in game, its time to design!

# Below is some basic documentation for each component (note: WIP)

## AnimatedBG
A simple wrapper around some of the animated backgrounds available within HL.

## AnimatedHeader
A header/banner type widget that allows you to define the text shown.

## AnimatedWindow
A wrapper around some of the animated window type widgets within HL.
You should add a vertical/horizontal box or overlay to the ContentArea of this widget to fill the window with contents. 

## BasicButton
A wrapper around the basic text button within HL.

## CheckboxButton
A wrapper around the checkbox on/off style menu buttons within HL.

## FlamingBG
An animated bg intended to be used as the header within AnimatedWindow widgets. 

## IconStat
Shows a stat, a value, and an icon. 

## InputButton
~ TODO

## NamedDivider
A simple divider with text to act as a seperator/header between content. 

## OptionSelector
A handy widget that allows you to define a list of options, and a default option, which can then be cycled through. Features two side buttons to control the selected option, with animated pips and events for when toggled etc <3

## OptionsList
Creates a list of CheckboxButtons using a map of String->Boolean to determine button names and default values. Provides events for when an option is toggled. 

## RoundButton
A simple round button you can use in your UI's. Featured within the OptionSelector widget. Has events etc for when button is triggered.

## SimpleSlider
A simple slider widget, currently only supports values from 1-9. (filler image goes wonky when using other values) 

## SimpleStat
A simple widget that allows you to place a stat name and value easily. 

## SliderList
~ TODO

## UDButtons / UDLRButtons
An arrangement of round buttons intended to be used for providing up/down or up/down/left/right functionality. 

## UIContainer
Should always be included within your main ui widget. Proides a background and content areas, where the bg area fills the entire screen space, and the content area provides positioning and scaling of the contents within based on your desired screen ratio (1920x1080p by default)

## VerticalScroller
A vertical scrolling widget styled to look better than that of the HL default. (defalut has some issues with the filler image)


# Binding to HL InputActions
Within your main UI widget, as long as it is a child class of type 'Screen', you can override some incredibly handy functions to gain access to the games input. Click on the blueprint graph for your main ui widget, and in the functions panel, select override, and then `Blueprint on UMG Input Action`. This overridden function now gives you access to all of the input actions defined within your UI widgets `UMGFocus->Focus Input Actions` section. Have fun <3 

# Example 
To view a basic working example, instead of adding your custom UI widget to the viewport, instead add the `UI_Example` which you can copy from the `DekitaRPG/UICore` folder into your mod folder and package with your mod. You can also clone this example to use as a your own base ui widget.  
