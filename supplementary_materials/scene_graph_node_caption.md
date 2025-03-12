## Specific Prompt
### To generate each object's category, we use the prompt below:
```
For each line, you will be provided with one idx and several names. Your task is to retrieve the most frequently mentioned name from each line and then determine its "category" with three rules:

1. If the object is a furniture typically placed on the floor and can support other objects or provide storage, label it as "category": "Asset". Do not include objects that are part of the furniture itself. Furniture is defined as large, functional items like tables, cabinets, or sofas, not small portable containers or decorations like baskets, vases, or lamps.
2. For objects that are suspended from the ceiling and those embedded in the wall, label it as "category": "Standalone".
3. For other objects, label it as "category": "Ordinary".

Your response should be in the format of a list of dictionaries, where each dictionary contains the "idx", "name", "category" of the object. Refer to the example below:

Example input:
[
    {"idx": 1, "names" = "sofa chair, couch, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair"},
    {"idx": 2, "names" = "stool, stool, stool, stool, ottoman, stool, ottoman, stool, stool, stool"},
    {"idx": 3, "names" = "coffee kettle, coffee maker, coffee kettle, coffee kettle, coffee kettle, coffee kettle, coffee kettle, coffee kettle, coffee maker, coffee kettle"}
    ...
]

Example output:
[
    {"idx": 1, "name": "sofa chair", "category": "Asset"},
    {"idx": 2, "name": "stool", "category": "Standalone"},
    {"idx": 3, "name": "coffee kettle", "category": "Ordinary"}
    ...
]
```
### Examples
Please note that when generating captions, we limit the processing to ten labels at most.
#### Replica room0
LLM accepts the following inputs:
```
[
    {'idx': 1, 'names': "sofa chair, couch, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, lamp, sofa chair"}, 
    {'idx': 2, 'names': "stool, stool, stool, stool, ottoman, stool, ottoman, stool, stool, stool"}, 
    {'idx': 3, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 5, 'names': "coffee kettle, coffee maker, coffee kettle, coffee kettle, coffee kettle, coffee kettle, coffee kettle, coffee kettle, coffee maker, coffee kettle"}, 
    {'idx': 6, 'names': "stool, stool, stool, stool, stool, stool, stool, stool, stool, stool"}, 
    {'idx': 7, 'names': "lamp, lamp, lamp, lamp, lamp, lamp, lamp, lamp, lamp, lamp"}, 
    {'idx': 8, 'names': "potted plant, potted plant, potted plant, potted plant, potted plant, tissue box, tissue box, tissue box, tissue box, tissue box"}, 
    {'idx': 9, 'names': "closet door, closet door, closet door, closet door, closet door, closet door, closet door, closet door, closet door, closet door"}, 
    {'idx': 10, 'names': "window, window, window, window, window, window, window, window, window, window"}, 
    {'idx': 11, 'names': "tissue box, tissue box, tissue box, toaster"}, 
    {'idx': 12, 'names': "power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet"}, 
    {'idx': 13, 'names': "end table, end table, end table, stool, stool, stool, stool, stool, stool, stool"}, 
    {'idx': 14, 'names': "light switch, light switch, light switch, light switch, light switch, light switch, light switch, range hood, range hood, range hood"}, 
    {'idx': 15, 'names': "coffee table, end table, coffee table, coffee table, coffee table, end table, end table, end table, end table, end table"}, 
    {'idx': 17, 'names': "plate, plate, book, book, book, book, book, book, book, book"}, 
    {'idx': 18, 'names': "cabinet, desk, cabinet, cabinet, cabinet, desk, desk, desk, cabinet, desk"}, 
    {'idx': 19, 'names': "poster, picture, poster, poster, poster, poster, picture, picture, picture, picture"}, 
    {'idx': 20, 'names': "potted plant, potted plant, potted plant, potted plant, potted plant, potted plant, potted plant, potted plant, potted plant, potted plant"}, 
    {'idx': 21, 'names': "blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds"}, 
    {'idx': 22, 'names': "window"}, 
    {'idx': 23, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 24, 'names': "pillow, pillow, sofa chair, pillow, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair"}, 
    {'idx': 25, 'names': "closet door, closet door, closet door, closet door, door"}, 
    {'idx': 26, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 27, 'names': "pillow"}, 
    {'idx': 28, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 29, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 30, 'names': "coffee table, coffee table, coffee table, coffee table, coffee table, coffee table, coffee table, coffee table, coffee table, coffee table"}, 
    {'idx': 31, 'names': "bowl, bowl, cup, candle, bowl, cup, cup, cup, cup, cup"}, 
    {'idx': 32, 'names': "sofa chair"}, 
    {'idx': 33, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 34, 'names': "blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds"}, 
    {'idx': 35, 'names': "sofa chair, sofa chair, armchair, sofa chair, armchair, armchair, sofa chair, sofa chair, sofa chair, sofa chair"}, 
    {'idx': 36, 'names': "radiator"}, 
    {'idx': 37, 'names': "coffee table"}, 
    {'idx': 38, 'names': "folded chair, sofa chair, chair, sofa chair, armchair, armchair, armchair, armchair, armchair, sofa chair"}, 
    {'idx': 39, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 40, 'names': "lamp, lamp, lamp, lamp, lamp, lamp, lamp, lamp, lamp, lamp"}, 
    {'idx': 41, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 42, 'names': "pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow, pillow"}, 
    {'idx': 43, 'names': "book, book, book, book, book, book, book, book, book, book"}, 
    {'idx': 44, 'names': "blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds, blinds"}, 
    {'idx': 45, 'names': "couch, couch, couch, couch, couch, couch, couch, couch, couch, couch"}, 
    {'idx': 46, 'names': "potted plant, potted plant, potted plant, potted plant, potted plant, plate"}, 
    {'idx': 47, 'names': "bag, bag, trash bin, bag, bag, backpack, trash bin, bag, bag, bag"}, 
    {'idx': 48, 'names': "cup, candle, cup"}, 
    {'idx': 49, 'names': "end table, coffee table, coffee table, end table"}, 
    {'idx': 50, 'names': "book, book, book, book, book, book, book, book, book, book"}, 
    {'idx': 52, 'names': "coffee table, coffee table, book, book, end table"}, 
    {'idx': 53, 'names': "lamp"}
]
```
and generates the following results:
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
    {'idx': 12, 'name': 'power outlet', 'category': 'Standalone'},
    {'idx': 13, 'name': 'end table', 'category': 'Asset'}, 
    {'idx': 14, 'name': 'light switch', 'category': "Standalone'},
    {'idx': 15, 'name': 'coffee table', 'category': 'Asset'}, 
    {'idx': 17, 'name': 'book', 'category': 'Ordinary'}, 
    {'idx': 18, 'name': 'cabinet', 'category': 'Asset'}, 
    {'idx': 19, 'name': 'poster', 'category': 'Standalone'}, 
    {'idx': 20, 'name': 'potted plant', 'category': 'Ordinary'}, 
    {'idx': 21, 'name': 'blinds', 'category': 'Standalone'},
    {'idx': 22, 'name': 'window', 'category': 'Standalone'}, 
    {'idx': 23, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 24, 'name': 'sofa chair', 'category': 'Asset'}, 
    {'idx': 25, 'name': 'closet door', 'category': 'Standalone'}, 
    {'idx': 26, 'name': 'pillow', 'category': 'Ordinary'}, 
    {'idx': 27, 'name': 'pillow', 'category': 'Ordinary'}, 
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
    {'idx': 48, 'name': 'cup', 'category': 'Standalone'}, 
    {'idx': 49, 'name': 'end table', 'category': 'Asset'}, 
    {'idx': 50, 'name': 'book', 'category': 'Ordinary'}, 
    {'idx': 52, 'name': 'coffee table', 'category': 'Asset'}, 
    {'idx': 53, 'name': 'lamp', 'category': 'Ordinary'}
]
```
#### Replica office0
LLM accepts the following inputs:
```
[
    {'idx': 1, 'names': "trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin"}, 
    {'idx': 2, 'names': "trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin"}, 
    {'idx': 3, 'names': "sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair, sofa chair"}, 
    {'idx': 4, 'names': "folded chair, chair, folded chair, folded chair, folded chair, folded chair, chair, chair, sofa chair, chair"}, 
    {'idx': 6, 'names': "closet door, closet door, closet door, closet door, closet door, closet door, closet door, closet door, closet door, closet door"}, 
    {'idx': 7, 'names': "tv, tv, tv, tv, projector screen, tv, tv, tv, tv, tv"}, 
    {'idx': 8, 'names': "table, table, desk, desk, coffee table, coffee table, coffee table, coffee table, coffee table, table"}, 
    {'idx': 9, 'names': "sofa chair, sofa chair, folded chair, folded chair, folded chair, folded chair, folded chair, folded chair, folded chair, folded chair"}, 
    {'idx': 10, 'names': "picture, picture, picture, picture, picture, picture, picture, picture, picture, picture"}, 
    {'idx': 11, 'names': "projector, speaker, speaker"}, 
    {'idx': 12, 'names': "stuffed animal, stuffed animal, stuffed animal, stuffed animal, stuffed animal, bag, bag, cushion, cushion, stuffed animal"}, 
    {'idx': 13, 'names': "potted plant, trash bin, trash can, trash bin, trash bin, trash bin, trash bin, trash bin, trash bin, storage bin"}, 
    {'idx': 14, 'names': "monitor, projector screen, projector screen, refrigerator, refrigerator, refrigerator, refrigerator, refrigerator, refrigerator, refrigerator"}, 
    {'idx': 15, 'names': "potted plant, potted plant, potted plant, potted plant, plant, plant, potted plant, potted plant, potted plant, potted plant"}, 
    {'idx': 16, 'names': "storage bin, sofa chair, sofa chair, sofa chair, couch, couch, couch, couch, couch, couch"}, 
    {'idx': 17, 'names': "power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet, power outlet"}, 
    {'idx': 18, 'names': "mouse, mouse, mouse, book, book, book, plate, towel, laptop, laptop"}, 
    {'idx': 19, 'names': "tissue box, cup, cup, cup, cup, tissue box, tissue box, tissue box, tissue box, tissue box"}, 
    {'idx': 20, 'names': "paper bag, paper bag, paper bag"}, 
    {'idx': 21, 'names': "bottle, cup, cup, cup, bottle"}, 
    {'idx': 22, 'names': "person"}, 
    {'idx': 23, 'names': "tissue box, tissue box, tissue box, tissue box, box, tissue box, tissue box, box, book, tissue box"}, 
    {'idx': 24, 'names': "storage bin, mat, mat, mat, mat, mat, mat, mat, mat, mat"}, 
    {'idx': 25, 'names': "speaker, speaker"}, 
    {'idx': 26, 'names': "tissue box, cup"}
]
```
and generates the following results:
```
[
    {"idx": 1, "name": "trash bin", "category": "Asset"},
    {"idx": 2, "name": "trash bin", "category": "Asset"},
    {"idx": 3, "name": "sofa chair", "category": "Asset"},
    {"idx": 4, "name": "chair", "category": "Asset"},
    {"idx": 6, "name": "closet door", "category": "Standalone"},
    {"idx": 7, "name": "tv", "category": "Ordinary"},
    {"idx": 8, "name": "coffee table", "category": "Asset"},
    {"idx": 9, "name": "folded chair", "category": "Asset"},
    {"idx": 10, "name": "picture", "category": "Standalone"},
    {"idx": 11, "name": "speaker", "category": "Ordinary"},
    {"idx": 12, "name": "stuffed animal", "category": "Ordinary"},
    {"idx": 13, "name": "trash bin", "category": "Asset"},
    {"idx": 14, "name": "refrigerator", "category": "Asset"},
    {"idx": 15, "name": "potted plant", "category": "Ordinary"},
    {"idx": 16, "name": "couch", "category": "Asset"},
    {"idx": 17, "name": "power outlet", "category": "Standalone"},
    {"idx": 18, "name": "book", "category": "Ordinary"},
    {"idx": 19, "name": "tissue box", "category": "Ordinary"},
    {"idx": 20, "name": "paper bag", "category": "Ordinary"},
    {"idx": 21, "name": "cup", "category": "Ordinary"},
    {"idx": 22, "name": "person", "category": "Ordinary"},
    {"idx": 23, "name": "tissue box", "category": "Ordinary"},
    {"idx": 24, "name": "mat", "category": "Standalone"},
    {"idx": 25, "name": "speaker", "category": "Ordinary"},
    {"idx": 26, "name": "tissue box", "category": "Ordinary"}
]
```