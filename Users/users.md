## 1. how many users are active ?

```javascript
[
  {
    $match: {
      isActive: true,
    },
  },
  {
    $count: "active User",
  },
];
```

## 2. what is the average age of the all users ?

```javascript
[
  {
    $group: {
      _id: null,
      average_age: {
        $avg: "$age",
      },
    },
  },
  {
    $project: {
      _id: 0,
    },
  },
];
```

## 3. list the top 5 most common favorite fruits among users ?

```
[
  {
    $group: {
      _id: "$favoriteFruit",
      user:{
        $sum:1
      }

    }
  },
  {
    $sort: {
      user: -1
    }
  },
  {
    $limit:5
  }
]
```

## 4. find the total number of male and female ?

```
[
  {
    $group: {
      _id: "$gender",
      total: {
        $sum:1
      }
    }
  }
]
```

## 5. which county has the hightest number of registered users ?

```
[
  {
    $group: {
      _id: "$company.location.country",
      count: {
        $sum: 1,
      },
    },
  },
  {
    $sort: {
      count: -1,
    },
  },
  {
    $limit: 1,
  },
]
```

## 6 . list all unique eye colors present in the collection

```
[
  {
    $group: {
      _id: "$eyeColor",
      user: {
        $sum: 1,
      },
    },
  },
]
```

## 7. what is the average numbers of tages per users?

```
[
  {
    $unwind: "$tags",
  },
  {
    $group: {
      _id: "$_id",
      perUserTags: {
        $sum: 1,
      },
    },
  },
  {
    $group: {
      _id: null,
      averageTagPerUser: {
        $avg: "$perUserTags",
      },
    },
  },
  {
    $project: {
      _id: 0,
    },
  },
]

or,

[
  {
    $addFields: {
      tagsNumber: {
        $size: {
          $ifNull: ["$tags", []],
        },
      },
    },
  },
  {
    $group: {
      _id: null,
      averageTagsUser: {
        $avg: "$tagsNumber",
      },
    },
  },
  {
    $project: {
      _id: 0,
    },
  },
]
```

## 8. how many users have enum as one of their tags ?

```
[
  {
    $match: {
      tags: "enim",
    },
  },
  {
    $count: "total",
  },
]
```

## 9. what are the names and age of users who are inactive and have velit as a tag?

```
[
  {
    $match: {
      isActive: false,
      tags: "velit",
    },
  },
  {
    $project: {
      name: 1,
      age: 1,
    },
  },
]
```

## 10. how many users a phone number starting with "+1(940) " ?

```
[
  {
    $match: {
      "company.phone": { $regex: /^\+1 \(940\)/ },
    },
  },
  {
    $count: "users",
  },
]
```

## 11. find out five user who has registered the most recently ?

```
[
  {
    $sort: {
      registered: -1,
    },
  },
  {
    $limit: 5,
  },
]

```

## 12. categories users by their favorite fruits ?

```
[
  {
    $group: {
      _id: "$favoriteFruit",
      users: {
        $push: "$$ROOT"
      }
    }
  }
]
```

## 13. How many users have 'ad' as second tag in their list of tags ?

```
[
  {
    $match: {
      "tags.1": "ad",
    },
  },
  {
    $count: "user",
  },
]
```

## 14. find users who have both "enim" and "id" as their tags ?

```
[
  {
    $match: {
      tags: {
        $all: ["enim", "id"],
      },
    },
  },
]
```

## 15. list all company located in USA

```
[
  {
    $match: {
      "company.location.country": "USA",
    },
  },
]

```
