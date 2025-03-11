## specific prompt
To generate each object's category, we use the prompt below:
```
For each line, you will be provided with one idx and several names. Your task is to retrieve the most frequently mentioned name from each line and then determine its "category" with three rules:

1. If the object is a furniture typically placed on the floor and can support other objects or provide storage, label it as "category": "Asset". Do not include objects that are part of the furniture itself. Furniture is defined as large, functional items like tables, cabinets, or sofas—not small portable containers or decorations like baskets, vases, or lamps.
2. For objects that are suspended from the ceiling and those embedded in the wall, label it as "category": "Standalone".
3. For other objects, label it as "category": "Ordinary".

Your response should be in the format of a list of dictionaries, where each dictionary contains the "idx", "name", "category" of the object. Refer to the example below:

Example input:
[
    {"idx": 1, "name" = "sofa chair", "name2" = "couch", "name3" = "sofa chair", "name4" = "sofa chair", "name5" = "sofa chair", "name6" = "sofa chair", "name7" = "sofa chair", "name8" = "sofa chair", "name9" = "sofa chair"},
    {"idx": 2, "name" = "stool", "name2" = "stool", "name3" = "stool", "name4" = "stool", "name5" = "ottoman", "name6" = "stool", "name7" = "ottoman", "name8" = "stool", "name9" = "stool", "name10" = "stool"},
    {"idx": 3, "name" = "coffee kettle", "name2" = "coffee maker", "name3" = "coffee kettle", "name4" = "coffee kettle", "name5" = "coffee kettle", "name6" = "coffee kettle", "name7" = "coffee kettle", "name8" = "coffee kettle", "name9" = "coffee maker", "name10" = "coffee kettle"}
    ...
]

Example output:
[
    {"idx": 1, "name": "sofa chair", "category": "Asset"},
    {"idx": 2, "name": "stool", "category": "Standalone"},
    {"idx": 3, "name": "coffee kettle", "category": "Ordinary"}
]
```

The prompt used for generating candidate objects consists of a query and the whole scene graph:
```
You will be provided with a list of objects in the room and a dictionary representing the hierarchical relationships between these objects. Each 'key' in the dictionary represents a supporting object, and its 'value' is a list of objects placed on top of it. 

Given a query, your task is to identify the target objects, those placed on top of other objects. And then output top three objects based on similarity to the target object, reference to the object list and hierarchical relationships. If a 'key' does not contain the required 'value', search for the corresponding 'value' in other 'keys'. If no exact match is found in the hierarchical relationships, select the most likely target objects based on contextual relevance in the object list.

Your response should be a list of dictionaries, each containing the 'idx', 'name' of the object. Refer to the example below:

The query you receive is a string, like this:
"This is a pillow on the couch."

And here is an example of the list of objects in the room:
[
    {"idx": "1", "name": "couch", "category": "Asset"},
    {"idx": "2", "name": "pillow", "category": "Ordinary"},
    {"idx": "3", "name": "power outlet", "category": "Standalone"},
    {"idx": "4", "name": "cabinet", "category": "Asset"},
    {"idx": "5", "name": "coffee kettle", "category": "Ordinary"},
    {"idx": "6", "name": "pillow", "category": "Ordinary"},
    {"idx": "7", "name": "pillow", "category": "Ordinary"},
    {"idx": "8", "name": "table", "category": "Asset"},
    {"idx": "9", "name": "book", "category": "Ordinary"}
    ...
]

And here is an example of the dictionary regarding the hierarchy of objects:
{
    "1": ["2", "6", "7"],
    "4": ["5"],
    "8": ["9"],
    ...
}

Example output:
[
    {"idx": "2", "name": "pillow"},
    {"idx": "6", "name": "pillow"},
    {"idx": "7", "name": "pillow"},
]
```