Json2Csharp Visual-Studio-Extension

You can convert JSON to a C# class-structure, by either selecting a part of the json or without selecting, the whole file.
This is just a first, simple solution to get a class-structure out of a JSON. If you have any issues or improvements, add an issue and I will take a look at it. :)

# How to use:

* in an existing solution
  * open the .json-file
  * click "Tools" -> "Json To C#"
  * a new .cs-file is opened containing the C# class-structure

* without an existing solution
  * open the file to convert
  * click "Tools" -> "Json To C#"
  * the opened file is replaced with the generated C# class-structure

# Important:
 * the selected text (or the file if nothing is selected) needs to start with either "[" for an array or "{" for an object. Otherwise no class is generated.

# Example:

filename: any.json
```javascript
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

![ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-40-29.gif](https://matthiasburger.gallerycdn.vsassets.io/extensions/matthiasburger/jsontocsharp/1.0/1599656408078/ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-40-29.gif)

![ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-43-19.gif](https://matthiasburger.gallerycdn.vsassets.io/extensions/matthiasburger/jsontocsharp/1.0/1599656408078/ConsoleApp3_-_Microsoft_Visual_Studio__Administrator__2020-09-09_14-43-19.gif)

# Planned issues:
* saving the new generated .cs to the path of json-file
* generating the correct namespace
* adding the new generated .cs to the solution
* adding a context-menu to paste json from clipboard to c# directly
* settings-menu for adding some settings
