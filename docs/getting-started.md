# Getting Started

## Prerequisites

This guide assumes that you know how to create a basic mod for Rain World (or already have), and modify JSON files. If you do not know how to create a Rain World Mod, you can follow the [Slugbase tutorial](https://slimecubed.github.io/slugbase/articles/template.html) for a basic tutorial, and then come back here.

This part of the documentation will guide you on how to set up the JSON file for your achievement, the necessary coding required will be covered in the next section.

## Custom Achievements

In order to create a custom achievement for your mod, first, in your mod's main folder, create a folder called `achievements` and inside of that create a file called `myachievement.json`. The path should be `MODNAME/achivements/myachievement.json`. The name does not matter, and will not conflict with another mod that has a json file with the same name. The contents of your json file must be a single json object, and the "id" field filled out.
```json
{
    "id": "MyID"
}
```
The id must be unique, so choose something fun!

While this will make a page show up in the achievement menu, there will not be anything useful in it. Let's change that.

The following properties are able to be added to the Json file: `name`, `imageFolder`, `flat`, `description`, and `origin`. `depthIllustrations` and `idleDepths` also exist, and information about them can be found below this section.
```json
{
    "id": "MyID",
    "name": "A New achivement",
    "imageFolder": "",
    "flat": "my achivement image",
    "description": "This is my awesome\nnew achivement",
    "origin": "My Mod"
}
```
- `name`: This will set the display name of the achievemnt on the page. If not included, the empty string (nothing) will be used instead.
- `imageFolder`: This sets the path to the folder containing the images to be shown with your achievement. This is relative to `StreamingAssets` or your mod's folder, and defaults to `illustrations` if not included.
- `flat`: This is the image that will be shown when a user is on the lowest graphics settings, or `depthIllustrations` is not included. If this is not included, no image will be shown. The image will be centered in the middle of the screen.
- `description`: The achievement's description. If this is not included, no description will be shown. A `\n` can be used to make a new line.
- `origin`: This lets you indicate which mod this achievement is from. If this is not included, then there will be no indication which mod it has come from. Otherwise, the text "From: My Mod" will be shown under the name of the achievement in this case, because we have set the `origin` property to "My Mod".

## Advanced Illustrations

As stated before, there is also an option to add the `depthIllustrations` and `idleDepths` properties. This will allow you to add a series of images, to achieve the same effect that slugcat select menu arts have. They consist of multiple layered images that will drift around a bit.

`depthIllustrations` is a list of objects, each with their own properties. `idleDepths` is a list of floats. The syntax is as follows, adding on to the previous example:
```json
{
    "id": "MyID",
    "name": "A New achivement",
    "imageFolder": "",
    "flat": "my achivement image",
    "description": "This is my awesome\nnew achivement",
    "origin": "My Mod",
    "idleDepths": [
        1,
        1.5
    ],
    "depthIllustrations": [
        {
            "image": "MyImage1",
            "depth": 1,
            "shader": "basic"
        }
    ]
}
```
- `depthIllustrations`: These are the images that will be used to make the scene for your achievement's page. It is a list of groups of properties for each image, where they are grouped together by a set of curly braces. The images listed first will be positioned behind the images listed last. .
    - `image`: The name of the image that will be used. The image must be in the same directory as the `imageFolder` property. It is important to keep the dimensions of the images 1488x868, as that is the expected image resolution so that they can be centered in the middle of the screen
    - `depth`: The depth of the image. This will partially influence how much it moves around, the lower the number is the more the image tends to move. This also comes into play for image blurring. The scene will focus on semi-random depths when being interacted with via the user moving their mouse, and the specific depths listed in `idleDepths` when the scene is left idle.
    - `shader`: The type of shader to be used. It can be "basic", "normal", "lighten", "lightedges", "rain", "overlay", "softlight", or "multiply". If a shader is used that makes use of red highlights under the image, then the image height must be doubled to 1736, with the red part taking up the bottom half of the image.
- `idleDepths`: This is a list of depths that the scene will randomly choose from, and cycle through, to focus on while idling. Images that have depths close to depths listed here will have almost no blur while that depth is focused on.