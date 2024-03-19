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

what is the average numbers of tages per users?
how many users have enum as one of their tags ?
what are the names and age of users who are inactive and have velit as a tag?
how many users a phone number starting with "+1(940) " ?
who has registered the most recently ?
