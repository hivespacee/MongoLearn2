# Assignment-2
- Easy-1
```js
db.products.aggregate([
  {
    $match: {
      category: "Electronics"
    }
  }
]) 
```
 Output :
 ```js
  {
  _id: ObjectId('68383a36c2450def960df7ae'),
  name: 'Laptop Pro',
  category: 'Electronics',
  price: 1200,
  quantity: 10,
  tags: [
    'computer',
    'portable',
    'work'
  ],
  date_added: 2023-01-15T10:00:00.000Z,
  supplier: {
    name: 'TechGlobe',
    location: 'USA'
  }
}
{
  _id: ObjectId('68383a36c2450def960df7af'),
  name: 'Wireless Mouse',
  category: 'Electronics',
  price: 25,
  quantity: 100,
  tags: [
    'peripheral',
    'computer',
    'wireless'
  ],
  date_added: 2023-02-01T11:30:00.000Z,
  supplier: {
    name: 'GadgetPro',
    location: 'China'
  }
}
{
  _id: ObjectId('68383a36c2450def960df7b0'),
  name: 'Mechanical Keyboard',
  category: 'Electronics',
  price: 75,
  quantity: 50,
  tags: [
    'peripheral',
    'computer',
    'mechanical'
  ],
  date_added: 2023-01-20T14:00:00.000Z,
  supplier: {
    name: 'TechGlobe',
    location: 'USA'
  }
}
{
  _id: ObjectId('68383a36c2450def960df7b4'),
  name: 'Smartwatch',
  category: 'Electronics',
  price: 199,
  quantity: 25,
  tags: [
    'wearable',
    'gadget',
    'portable'
  ],
  date_added: 2023-04-01T12:00:00.000Z,
  supplier: {
    name: 'GadgetPro',
    location: 'China'
  }
}
{
  _id: ObjectId('68383a36c2450def960df7b7'),
  name: 'Bluetooth Speaker',
  category: 'Electronics',
  price: 80,
  quantity: 60,
  tags: [
    'audio',
    'portable',
    'wireless'
  ],
  date_added: 2023-02-25T17:00:00.000Z,
  supplier: {
    name: 'SoundWave',
    location: 'USA'
  }
}    

```

- Easy-2
``` js
db.products.aggregate([
  {
    $group: {
      _id: "$category",
      count: { $sum: 1 }
    }
  }
])
   ```



Output:

``` js
{
  _id: 'Apparel',
  count: 2
}

{
  _id: 'Home Goods',
  count: 1
}

{
  _id: 'Accessories',
  count: 1
}
{
  _id: 'Sports',
  count: 1
}
{
  _id: 'Electronics',
  count: 5
}


```

- Easy-3
``` js
 db.products.aggregate([
  {
    $project: {
      _id: 0,
      name: 1,
      price: 1
    }
  },
  {
    $sort: {
      price: -1
    }
  }
])
  ```

Output:

```js
{
  name: 'Laptop Pro',
  price: 1200
}

{
  name: 'Espresso Machine',
  price: 250
}

{
  name: 'Smartwatch',
  price: 199
}
{
  name: 'Bluetooth Speaker',
  price: 80
}
{
  name: 'Mechanical Keyboard',
  price: 75
}
{
  name: 'Denim Jeans',
  price: 60
}
{
  name: 'Leather Wallet',
  price: 45
}
{
  name: 'Yoga Mat',
  price: 30
}
{
  name: 'Wireless Mouse',
  price: 25
}
{
  name: 'Cotton T-Shirt',
  price: 20
}

```


- Medium -1:
``` js
 db.products.aggregate([
  {
    $group: {
      _id: "$supplier.name",
      totalQuantity: { $sum: "$quantity" }
    }
  }
])

```

Output:

``` js
{
  _id: 'GadgetPro',
  totalQuantity: 125
}
{
  _id: 'HomeBest',
  totalQuantity: 30
}
{
  _id: 'FashionHub',
  totalQuantity: 280
}
{
  _id: 'StyleCraft',
  totalQuantity: 120
}
{
  _id: 'ActiveLife',
  totalQuantity: 90
}
{
  _id: 'TechGlobe',
  totalQuantity: 60
}
{
  _id: 'SoundWave',
  totalQuantity: 60
}

```
- Medium-2
``` js
 db.products.aggregate([
  { $unwind: "$tags" },
  {
    $group: {
      _id: "$tags",
      averagePrice: { $avg: "$price" }
    }
  },
  { $sort: { averagePrice: -1 } }
])
  ```
Output:
```js
{
  _id: 'work',
  averagePrice: 1200
}
{
  _id: 'portable',
  averagePrice: 493
}
{
  _id: 'computer',
  averagePrice: 433.3333333333333
}
{
  _id: 'appliance',
  averagePrice: 250
}
{
  _id: 'coffee',
  averagePrice: 250
}
{
  _id: 'kitchen',
  averagePrice: 250
}
{
  _id: 'wearable',
  averagePrice: 199
}
{
  _id: 'gadget',
  averagePrice: 199
}
{
  _id: 'audio',
  averagePrice: 80
}
{
  _id: 'mechanical',
  averagePrice: 75
}
{
  _id: 'denim',
  averagePrice: 60
}
{
  _id: 'wireless',
  averagePrice: 52.5
}
{
  _id: 'peripheral',
  averagePrice: 50
}
{
  _id: 'leather',
  averagePrice: 45
}
{
  _id: 'fashion',
  averagePrice: 45
}
{
  _id: 'clothing',
  averagePrice: 40
}
{
  _id: 'exercise',
  averagePrice: 30
}
{
  _id: 'fitness',
  averagePrice: 30
}
{
  _id: 'cotton',
  averagePrice: 20
}
{
  _id: 'cotton',
  averagePrice: 20
}
```

- Medium-3
 ``` js
 db.products.aggregate([
    {$match:{date_added:{$gte:new ISODate("2023-02-01T00:00:00Z"),$lt: new ISODate("2023-03-01T00:00:00Z")}}},
    {$project:{_id:0,name:1,category:1,date_added:{$dateToString:{format:"%Y-%m-%d",date: "$date_added"}}}}
    ])
 ```


Output:
```js  
{
  name: 'Wireless Mouse',
  category: 'Electronics',
  date_added: '2023-02-01'
}

{
  name: 'Espresso Machine',
  category: 'Home Goods',
  date_added: '2023-02-15'
}
{
  name: 'Bluetooth Speaker',
  category: 'Electronics',
  date_added: '2023-02-25'
}
```
