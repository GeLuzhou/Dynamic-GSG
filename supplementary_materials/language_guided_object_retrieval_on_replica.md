## Specific Prompt
### The prompt used for generating candidate objects consists of a query and the whole scene graph:
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
### Examples
Please note that the object list in the index is smaller than the original object list because we filtered out inaccurately identified objects before querying.
#### Replica room0
LLM accepts the following inputs:

query
```
This is a pillow on the couch.
```
object list
```
[
    {'idx': 1, 'name': 'sofa chair', 'category': 'Asset'}, 
    {'idx': 2, 'name': 'stool', 'category': 'Standalone'}, 
    {'idx': 3, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 5, 'name': 'coffee kettle', 'category': 'Ordinary'}, 
    {'idx': 6, 'name': 'stool', 'category': 'Standalone'}, 
    {'idx': 7, 'name': 'lamp', 'category': 'Ordinary'}, 
    {'idx': 8, 'name': 'potted plant', 'category': 'Ordinary'}, 
    {'idx': 9, 'name': 'closet door', 'category': 'Standalone'}, 
    {'idx': 10, 'name': 'window', 'category': 'Standalone'}, 
    {'idx': 11, 'name': 'tissue box', 'category': 'Ordinary'}, 
    {'idx': 13, 'name': 'end table', 'category': 'Asset'}, 
    {'idx': 15, 'name': 'coffee table', 'category': 'Asset'}, 
    {'idx': 17, 'name': 'book', 'category': 'Ordinary'}, 
    {'idx': 18, 'name': 'cabinet', 'category': 'Asset'}, 
    {'idx': 19, 'name': 'poster', 'category': 'Standalone'}, 
    {'idx': 20, 'name': 'potted plant', 'category': 'Ordinary'}, 
    {'idx': 22, 'name': 'window', 'category': 'Standalone'}, 
    {'idx': 23, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 24, 'name': 'sofa chair', 'category': 'Asset'}, 
    {'idx': 25, 'name': 'closet door', 'category': 'Standalone'}, 
    {'idx': 26, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 28, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 29, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 30, 'name': 'coffee table', 'category': 'Asset'}, 
    {'idx': 31, 'name': 'cup', 'category': 'Ordinary'}, 
    {'idx': 32, 'name': 'sofa chair', 'category': 'Asset'}, 
    {'idx': 33, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 34, 'name': 'blinds', 'category': 'Standalone'}, 
    {'idx': 35, 'name': 'sofa chair', 'category': 'Asset'}, 
    {'idx': 36, 'name': 'radiator', 'category': 'Standalone'}, 
    {'idx': 37, 'name': 'coffee table', 'category': 'Asset'}, 
    {'idx': 38, 'name': 'armchair', 'category': 'Asset'}, 
    {'idx': 39, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 40, 'name': 'lamp', 'category': 'Ordinary'}, 
    {'idx': 41, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 42, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 43, 'name': 'book', 'category': 'Ordinary'}, 
    {'idx': 44, 'name': 'blinds', 'category': 'Standalone'}, 
    {'idx': 45, 'name': 'couch', 'category': 'Asset'}, 
    {'idx': 46, 'name': 'potted plant', 'category': 'Ordinary'}, 
    {'idx': 47, 'name': 'bag', 'category': 'Ordinary'}, 
    {'idx': 49, 'name': 'end table', 'category': 'Asset'}, 
    {'idx': 50, 'name': 'book', 'category': 'Ordinary'}, 
    {'idx': 52, 'name': 'coffee table', 'category': 'Asset'}
]
```
scene graph
```
{   
    1: [3, 26, 28, 29], 
    18: [5, 11, 17, 20], 
    15: [7, 8], 
    45: [23, 41, 42], 
    30: [31, 43, 46], 
    35: [33], 
    38: [39], 
    52: [40, 50]
}
```
and generates the following results:
```
[
    {"idx": "23", "name": "pillow"},
    {"idx": "41", "name": "pillow"},
    {"idx": "42", "name": "pillow"}
]
```
For the above scene graph input example, the explanation is:
```
{
    'Asset' object {'idx': 1, 'name': 'sofa chair'} contains 'Ordinary' objects {'idx': 3,'name': 'pillow'}, {'idx': 26, 'name': 'pillow'}, {'idx': 28, 'name': 'pillow'}, {'idx': 29, 'name': 'pillow'}
    'Asset' object {'idx': 18, 'name': 'cabinet'} contains 'Ordinary' objects {'idx': 5, 'name': 'coffee kettle'}, {'idx': 11, 'name': 'tissue box'}, {'idx': 17, 'name': 'book'}, {'idx': 20, 'name': 'potted plant'}
    'Asset' object {'idx': 15, 'name': 'coffee table'} contains 'Ordinary' objects {'idx': 7, 'name': 'lamp'}, {'idx': 8, 'name': 'potted plant'}
    'Asset' object {'idx': 45, 'name': 'couch'} contains 'Ordinary' objects {'idx': 23, 'name': 'pillow'}, {'idx': 41, 'name': 'pillow'}, {'idx': 42, 'name': 'pillow'}
    'Asset' object {'idx': 30, 'name': 'coffee table'} contains 'Ordinary' objects {'idx': 31, 'name': 'cup'}, {'idx': 43, 'name': 'book'}, {'idx': 46, 'name': 'potted plant'}
    'Asset' object {'idx': 35, 'name': 'sofa chair'} contains 'Ordinary' objects {'idx': 33, 'name': 'pillow'}
    'Asset' object {'idx': 38, 'name': 'armchair'} contains 'Ordinary' objects {'idx': 39, 'name': 'pillow'}
    'Asset' object {'idx': 52, 'name': 'coffee table'} contains 'Ordinary' objects {'idx': 40, 'name': 'lamp'}, {'idx': 50, 'name': 'book'}
}
```
#### Replica office0
LLM accepts the following inputs:

query
```
This is a tissue box on the table.
```
object list
```
[
    {'idx': 1, 'name': 'trash bin', 'category': 'Asset'}, 
    {'idx': 2, 'name': 'trash bin', 'category': 'Asset'}, 
    {'idx': 3, 'name': 'sofa chair', 'category': 'Asset'},  
    {'idx': 4, 'name': 'chair', 'category': 'Asset'}, 
    {'idx': 6, 'name': 'closet door', 'category': 'Standalone'}, 
    {'idx': 7, 'name': 'tv', 'category': 'Ordinary'}, 
    {'idx': 8, 'name': 'coffee table', 'category': 'Asset'}, 
    {'idx': 9, 'name': 'folded chair', 'category': 'Asset'}, 
    {'idx': 12, 'name': 'stuffed animal', 'category': 'Ordinary'}, 
    {'idx': 13, 'name': 'trash bin', 'category': 'Asset'}, 
    {'idx': 14, 'name': 'refrigerator', 'category': 'Asset'}, 
    {'idx': 15, 'name': 'potted plant', 'category': 'Ordinary'}, 
    {'idx': 16, 'name': 'couch', 'category': 'Asset'}, 
    {'idx': 17, 'name': 'power outlet', 'category': 'Ordinary'}, 
    {'idx': 18, 'name': 'book', 'category': 'Ordinary'}, 
    {'idx': 19, 'name': 'tissue box', 'category': 'Ordinary'}, 
    {'idx': 20, 'name': 'paper bag', 'category': 'Ordinary'}, 
    {'idx': 22, 'name': 'person', 'category': 'Ordinary'}, 
    {'idx': 23, 'name': 'tissue box', 'category': 'Ordinary'}, 
    {'idx': 24, 'name': 'mat', 'category': 'Ordinary'}
]
```
scene graph
```
{   
    14: [15], 
    8: [18, 19, 23]
}
```
and generates the following results:
```
[   
    {"idx": "19", "name": "tissue box"},
    {"idx": "23", "name": "tissue box"},
    {"idx": "18", "name": "book"}
]
```
For the above scene graph input example, the explanation is:
```
{
    'Asset' object {'idx': 14, 'name': 'refrigerator'} contains 'Ordinary' objects {'idx': 15, 'name': 'potted plant'}
    'Asset' object {'idx': 8, 'name': 'coffee table'} contains 'Ordinary' objects {'idx': 18, 'name': 'book'}, {'idx': 19, 'name': 'tissue box'}, {'idx': 23, 'name': 'tissue box'}
}
```