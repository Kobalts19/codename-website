<style>
    img {
        width: 10vw
    }
</style>
# Events/Notetype Scripts
### Events
Events can be found in ``./data/events``. There's currently 3 files used for events: a script file, a JSON file to determine the parameters of it, and an image file for it's icon. *(they all need to have the same name as the event)*

First, we'll go over making the JSON file. The JSON file holds all parameters required for the Event, and each parameter can have different types. Each parameter type is listed here:
```json
{
    "params": [
        {
            "name": "Bool",
            "type": "Bool",
            "defaultValue": false
        },
        {
            "name": "Int",
            "type": "Int(0, 99, 1)",
            "defaultValue": 0
        },
        {
            "name": "Float",
            "type": "Float(0, 99, 1, 2)",
            "defaultValue": 0.00
        },
        {
            "name": "String",
            "type": "String",
            "defaultValue": "nothing"
        },
        {
            "name": "StrumLine",
            "type": "StrumLine",
            "defaultValue": 0
        },
        {
            "name": "ColorWheel",
            "type": "ColorWheel",
            "defaultValue": "#FFFFFF"
        },
        {
            "name": "DropDown",
            "type": "DropDown('entry one', 'entry two')",
            "defaultValue": "entry one"
        }
    ]
}
```
*(you can copy these for your own JSON file)*<br>
There's a lot of them but we'll go over each one.
- **Bool** creates a checkmark and returns true or false.
- **Int()** returns an int. This one has parameters for minimum value, maximum value, and stepper *(non-functional)*
- **Float()** is the same as int, but has an extra parameter for precision.
- **String** returns a string.
- **StrumLine** creates a dropdown menu that contains the current StrumLine in the chart. Returns Ints corresponding the StrumLine index in the group ``strumLines``.
- **ColorWheel** creates a color wheel that returns the color in Int hex format.
- **DropDown()** generates a dropdown menu that contains the entries inside the brackets.

<img src="Events or Notetype Scripts-1.png"/>

Now that we have established the Parameters, we can go over scripting the event now. A basic flash camera event looks something like this:
```hx
function onEvent(e) {
    var params:Array = e.event.params;
    if (e.event.name == "Flash Camera") {
        camGame.flash(params[1], params[0]);
    }
}
```
In this example, we assume that we set our parameters to be the duration of the flash *(float)*, and the color of it *(colorwheel)*. <br>
<img src="Events or Notetype Scripts.png"/>

The order of the parameters in ``e.event.params`` coresponds to the order you've put the params in.

For the icon, place a *(preferabily 16x16)* image in the same directory as the event files.

*Write about .pack files later*

### Notetypes
Making notetypes only consists of 2 files: the script file and the note sprites.

Putting the sprites in ``./images/game/notes`` and naming them after the notetype name will automatically replace the default note sprites with those.

Writing a script for the notetypes is very easy. Though only one script is ran for all existing notetypes instead of each note, you can still code actions for them. <br>
For example here is code for triggering actions when the player presses it:
```hx
function onPlayerHit(event) {
    if (event.noteType == "Damage Note") {
        health -= 0.5;
        boyfriend.playAnim("hurt");
    }
}
```