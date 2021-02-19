---
layout: post
title:      "Inventory Update in JavaScript"
date:       2021-02-19 19:03:39 +0000
permalink:  inventory_update_in_javascript
---

This was one of my code exercises for the day (from [freeCodeCamp](https://www.freecodecamp.org/)): 

> Compare and update the current inventory stored in a 2D array against a second 2D array of a fresh delivery. Update the current existing inventory item quantities (in arr1). If an item cannot be found, add the new item and quantity into the inventory array. The returned inventory array should be in alphabetical order by item.
> 

```

// Example inventory lists
var curInv = [
    [21, "Bowling Ball"],
    [2, "Dirty Sock"],
    [1, "Hair Pin"],
    [5, "Microphone"]
];

var newInv = [
    [2, "Hair Pin"],
    [3, "Half-Eaten Apple"],
    [67, "Bowling Ball"],
    [7, "Toothpaste"]
];

updateInventory(curInv, newInv);
```

When I saw the inventory lists, I immediately thought "key : value" pairs. If we convert this 2D array into a single JS Object, we could take advantage of the ["in" operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) to check if an item already exists in the current inventory list. Luckily, JS has a method just for this kind of scenario: [`Object.fromEntries()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries)

In order to use the "in" operator to check the items, we need to make the item names the "key" of the new inventory Object. This is possible with a little array manipulation.
```
let inventory = Object.fromEntries(curInv.map(([ key, val ]) => [ val, key ]))
```
This would be our current `inventory` Object:
```
{
Bowling Ball: 88
Dirty Sock: 2
Hair Pin: 3
Half-Eaten Apple: 3
Microphone: 5
Toothpaste: 7
}
```
Next, we want to check if each item in the fresh delivery already exists in our current `inventory` Object. If it does, we want to update the value (count) of that item. If it does not exist, we want to add the item key and value. This is where we can implement that "in" operator:
```
for(let i = 0; i < newInv.length; i++){
        if(newInv[i][1] in inventory){
            inventory[newInv[i][1]] += newInv[i][0]
        }else{
            inventory[newInv[i][1]] = newInv[i][0]
        }
    }
```
Once this iterates through the `newInv` list, we have a complete `inventory` Object with updated counts. However, our solution needs to return an inventory array in alphabetical order by item.
```
updateInventory(curInv, newInv) should return [[88, "Bowling Ball"], [2, "Dirty Sock"], [3, "Hair Pin"], [3, "Half-Eaten Apple"], [5, "Microphone"], [7, "Toothpaste"]]
```
Conveniently, `Object.fromEntries()` has a reverse method, [`Object.entries()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries). We can sort the resulting array and then manipulate it similarly as before.  

My final solution implementation:
```
function updateInventory(arr1, arr2) {
    let inventory = Object.fromEntries(arr1.map(([ key, val ]) => [ val, key ]))
    for(let i = 0; i < arr2.length; i++){
        if(arr2[i][1] in inventory){
            inventory[arr2[i][1]] += arr2[i][0]
        }else{
            inventory[arr2[i][1]] = arr2[i][0]
        }
    }
    return Object.entries(inventory).sort().map(([ key, val ]) => [ val, key ]);
}
```

