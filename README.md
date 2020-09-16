Download in Marketplace:
[Json To C#](https://marketplace.visualstudio.com/items?itemName=MatthiasBurger.JsonToCSharp)

> There is no update-package from V1 to V1.1 since I made a mistake with deployment. You probably need to uninstall V1 completely and install V1.1 

You can convert JSON to a C# class-structure, by either selecting a part of the json or without selecting, the whole file.
This is just a first, simple solution to get a class-structure out of a JSON. If you have any issues or improvements, add an issue in my [github-issues](https://github.com/matthiasburger/Json2Csharp-Issues/issues) and I will take a look at it. :)

# How to use:

You can find the new menu "Json to C#" in "Extensions".

* in an existing solution, a new .cs-file is opened containing the C# class-structure
* without an existing solution, the opened file is replaced with the generated C# class-structure
* you also can simply copy json from anywhere into your clipboard and directly paste the C# structure with click on "Paste JSON as C#"

# Important:
 * the selected text (or the file if nothing is selected) needs to start with either "[" for an array or "{" for an object. Otherwise no class is generated.

# Example:

filename: any.json
```json
{
"items":
    {
        "item":
            [
                {
                    "id": "0001",
                    "type": "donut",
                    "name": "Cake",
                    "ppu": 0.55,
                    "batters":
                        {
                            "batter":
                                [
                                    { "id": "1001", "type": "Regular" },
                                    { "id": "1002", "type": "Chocolate" },
                                    { "id": "1003", "type": "Blueberry" },
                                    { "id": "1004", "type": "Devil's Food" }
                                ]
                        },
                    "topping":
                        [
                            { "id": "5001", "type": "None" },
                            { "id": "5002", "type": "Glazed" },
                            { "id": "5005", "type": "Sugar" },
                            { "id": "5007", "type": "Powdered Sugar" },
                            { "id": "5006", "type": "Chocolate with Sprinkles" },
                            { "id": "5003", "type": "Chocolate" },
                            { "id": "5004", "type": "Maple" }
                        ]
                }
            ]
    }
}
```

filename: Any.cs
```csharp
namespace None
{
    using System;
    using System.Collections.Generic;
    using System.Globalization;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Converters;
    
    public class Any 
    {
        [JsonProperty("items")]
        public Items Items {get; set;}
    }

    public class Items 
    {
        [JsonProperty("item")]
        public IList<Item> Items {get; set;}
    }

    public class Item 
    {
        [JsonProperty("id")]
        public string Id {get; set;}
        [JsonProperty("type")]
        public string Type {get; set;}
        [JsonProperty("name")]
        public string Name {get; set;}
        [JsonProperty("ppu")]
        public float Ppu {get; set;}
        [JsonProperty("batters")]
        public Batters Batters {get; set;}
        [JsonProperty("topping")]
        public IList<Topping> Toppings {get; set;}
    }

    public class Batters 
    {
        [JsonProperty("batter")]
        public IList<Batter> Batters {get; set;}
    }

    public class Batter 
    {
        [JsonProperty("id")]
        public string Id {get; set;}
        [JsonProperty("type")]
        public string Type {get; set;}
    }

    public class Topping 
    {
        [JsonProperty("id")]
        public string Id {get; set;}
        [JsonProperty("type")]
        public string Type {get; set;}
    }
}
```

# Live preview

![ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-40-29.gif](ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-40-29.gif)

![ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-43-19.gif](ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-43-19.gif)

# Planned issues:
| issue | development state |
| --- | --- |
| settings-menu for adding some settings | |

# Version-History

### V 1.1.1 (16/09/2020)
* Bugfix:
  * simple-type arrays are now converted correctly to e.g. `IList<string>` instead of `IList<SimpleType>` where `SimpleType` was an empty class
  * when a json-file was converted that did not belong to an opened solution, a nullreference-exception was thrown

### V 1.1 (15/09/2020)
* Features: 
  * you can now copy json and on button-click paste the c# result
* Improvement
  * menu is moved from "Tools" to "Extensions" and has a submenu
  * files are auto-saved in the same path as their json and added to project
  * if there's another c#-file in the same directory, the namespace is copied

### V 1.0 (09/09/2020)
* Base Version. Requires an active document that is getting converted. You either can select a part from json, or (without selecting) convert the complete file. Within an open solution, a new .cs-file is created and the result is pasted in - without an active solution, the json is replaced. (I will remove this behaviour in a future version)

