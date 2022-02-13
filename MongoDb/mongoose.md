# Mongoose

Elegant [MongoDB](https://www.mongodb.com/) object modeling for [Node.js](https://nodejs.org/en/)

### Installing mongoose package

```bash
npm install mongoose
```

```java
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/fruitsDB', {useNewUrlParser:true});

const fruitSchema=new mongoose.Schema({
  name:String,
  rating: Number,
  review:String
});

const Fruit=mongoose.model("Fruit",fruitSchema);

const fruit =new Fruit({
  name:"Apple",
  rating:7,
  review:"Better than Banana."
});
fruit.save();
```



### References

https://mongoosejs.com/