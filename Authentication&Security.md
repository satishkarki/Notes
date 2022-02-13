# Authentication and Security

### Level 1 Security

Email and Password to access the page

```javascript
// To register with email and password
//In register page
app.post("/register", function(req,res){
    const newUser=new User({
        email: req.body.username,
        password:req.body.password
    });
    newUser.save(function(err){
        if (err){
            console.log(err);
        } else{
            res.render("secrets");
        }
    });
});
```

```javascript
// To login with the registered email and password
// In Login page
app.post("/login", function(req,res){
    const username=req.body.username;
    const password=req.body.password;
    User.findOne({email:username}, function(err, foundUser){
        if(err){
            console.log(err);
        } else {
            if (foundUser){
                if (foundUser.password===password){
                    res.render("secrets");
                }else{
                    res.render("login")
                };
            }
        }
    });
});
```

### Level 2 Security

Encrypting the password

Right now we have email and password which is stored in plain text in our MongoDB database. Next step is to encrypt the user information.

#### [Mongoose Encryption](https://www.npmjs.com/package/mongoose-encryption)

```bash
npm install mongoose-encryption
```

Simple encryption and authentication for mongoose documents. 

```javascript
const mongoose=require("mongoose");
const encrypt=require("mongoose-encryption");

mongoose.connect('mongodb://localhost:27017/userDB', {useNewUrlParser:true});

const userSchema=new mongoose.Schema({
    email:String,
    password: String
});
// Our encryption key is still vulnerable 
const secret="Thisisoursecret";
userSchema.plugin(encrypt,{secret:secret, encryptedFields:['password']});

const User=new mongoose.model("User", userSchema);
```

In our database

```bash
# password is encrypted
userDB> db.users.find()
[
  {
    _id: ObjectId("614e89997d413194face4f49"),
    email: 'notfake@mail.com',
    _ct: Binary(Buffer.from("613b501f755cb58bedb64e6e1bb4337957663674efc03d520cbebfaeb5681f692c1e8bb57a3a3443d0eac31b987c0e2bbd", "hex"), 0),
    _ac: Binary(Buffer.from("61183c678fa8358c8ad85963435784a8c377d8c4590276f5de66f1971f3dd4335d5b225f6964222c225f6374225d", "hex"), 0),
    __v: 0
  }
]
```

#### Environment Variable

[dotenv](https://www.npmjs.com/package/dotenv)

Dotenv is a zero-dependency module that loads environment variables from a `.env` file into [`process.env`](https://nodejs.org/docs/latest/api/process.html#process_process_env)

```bash
npm install dotenv
```

```javascript
// In app.js at the beginning
require('dotenv').config()
```

```javascript
// In .env file
// Add environment-specific variables on new lines in the form of NAME=VALUE

SECRET=Thisisoursecret
```

```javascript
// In app.js, change this
userSchema.plugin(encrypt,{secret:secret, encryptedFields:['password']});
// to use :process.env
userSchema.plugin(encrypt,{secret:process.env.SECRET, encryptedFields:['password']});
```

#### .gitignore

Next step is to include the sensitive files in the `.gitignore` file. You know the drill.

[.gitignore Templates](https://github.com/github/gitignore)

**Note:** Remember `git log` ? It shows all the previous commits made so make sure to incorporate `.env` and `.gitignore` before the first commit.

### Level 3 Security

Hashing Password

Here I am using `md5` but remember `md5 hashes` are **no longer considered cryptographically secure methods** and should not be used for cryptographic authentication.

[md5 guide](https://www.npmjs.com/package/md5)

```bash
npm install md5
```

```javascript
// In app.js
const md5=require("md5");


const newUser=new User({
  email: req.body.username,
  password:md5(req.body.password)
```

```bash
# In database
userDB> db.users.find()
[
  {
    _id: ObjectId("614e9ce39f97c6f4a5607fad"),
    email: 'notfake@mail.com',
    password: '827ccb0eea8a706c4c34a16891f84e7b',
    __v: 0
  }
]
```

### Level 4 Security

- Salting & Salt Rounds
- [bcrypt](https://www.npmjs.com/package/bcrypt) :A library to help you hash passwords
- Be careful about the version compatibility

```bash
npm install bcrypt
```

```javascript
// In app.js
const bcrypt=require("bcrypt");
const saltRounds=10

app.post("/register", function(req,res){
bcrypt.hash(req.body.password, saltRounds, function(err,hash){
        const newUser=new User({
            email: req.body.username,
            password:req.body.password
        });
        newUser.save(function(err){
            if (err){
                console.log(err);
            } else{
                res.render("secrets");
            }
        });
    });
});

app.post("/login", function(req,res){
app.post("/login", function(req,res){
    const username=req.body.username;
    const password=req.body.password;

    User.findOne({email:username}, function(err, foundUser){
        if(err){
            console.log(err);
        } else {
            if (foundUser){
                bcrypt.compare(password, foundUser.password, function(err, resresult){
                    if(result===true){
                        res.render("secrets");
                    }else{
                        res.render("login")
                    }
                });
             }
        }
    });
});
```

```bash
// In database
[
  {
    _id: ObjectId("614f63d03cabf56391b87557"),
    username: '1@mail.com',
    salt: '50ff484e8db7a6cd6849c082bef8206efb921f8c41ed10391e65250c436be166',
    hash: '7879f8cac67631cafb857fb8d43fa653cdf7dd711a53e41b958e73a20a3dbc1c3a80d3ca96f4cc72b71c489068cc021c55fcdb3bac08e4389c1f5f06affc02883696ed7a80176108136cfb490609ebb9e79b4340bef1326caac481e4a6bc1b736d3a4dee738ca3b5e6d0355e416644894d9a0a562cb5990b4f8d28d1a5f00a0020fe458fc804fc59ca70aadb0367aab0b7031e5605331a9d5225224219181e3149118be0422308e104053a04d56d25dc3962841bdf4ab4819d07070cb738dc0ea1d3a33cb949b000f8e9af991f4297dfa836a444680c03c1170a96d9c1b2491a4b9852412de68e7bc3fe007b17dd477eb0148324ed5a94bf84e239b8881630d312312b34f7c6fc3e6217c1eea505171ea453c3d4b71496ac73aeff0085f65b4f8c680faefa2cbf26099c88d0d9120ea07980586776f6fb0e4f643624d4aeb96e7ecd9678bc5177ee212800368af64f02b42dcc09d2a3fd2ee6f53ee0407c7595f369974aecbd6af6e38f07b5ce525b3ee11379b5e2b3134d501d3f5db471988f7471449799bbdd15e5a667dcc3cfdd11ba0764e2594d39dc3b8fc7a9c035d789c3d9bb04d08ec256c1bdd77c1aa414f78b20016a3a40d55588122e02dff86513ea1430c816876be2b2f1b450537fbef787d7f100e1a1f85e4aa8f9eab87653ca6849bf2b3c7fab645e669ec9175ff4c3be280c597c63000410a911a42c6d0e78',
    __v: 0
  }
]

```



### Level 5 Security

Cookies and Sessions

[Passportjs](http://www.passportjs.org/)

```bash
# packages
npm install passport
npm install passport-local
npm install passport-local-mongoose
# Not express-sessions
npm install express-session

```

```javascript
//In App.js

const session=require("express-session");
const passport=require("passport");
const passportLocalMongoose=require("passport-local-mongoose");

app.use(session({
    secret:"Our Little Secret",
    resave:false,
    saveUninitialized:false
}));

app.use(passport.initialize());
app.use(passport.session());

userSchema.plugin(passportLocalMongoose);

passport.use(User.createStrategy());
passport.serializeUser(User.serializeUser());
passport.deserializeUser(User.deserializeUser());

app.get("/secrets", function(req,res){
    if (req.isAuthenticated()){
        res.render("secrets");
    } else {
        res.redirect("/login");
    }
});

app,post("/register", function(req,res){
    User.register({username:req.body.username},req.body.password, function(err,user){
        if(err){
            console.log(err);
            res.redirect("/register");
        } else{
            passport.authenticate("local")(req,res,function(){
                res.redirect("/secrets");
            });
        }
    });
});

app.post("/login", function(req,res){
    const user =new User({
        username:req.body.username,
        password:req.body.password
    });
    req.login(user, function(err){
        if(err){
            console.log(err);
        } else{
            passport.authenticate("local")(req,res,function(){
                res.redirect("/secrets");
            });
        }
    });
});
```



### Level 6 Security

OAuth 2.0 & how to implement  Sign in with Google

Open Authorization

-  Granular Level of Access

- Read/Read+Write Access

- Revoke Access

  

Step 1: Set up your app in third party developer console

Step 2: Redirect to Authenticate 

Step 3: User logs in with 3rd party application

Step 4: User Grants Permission

Step 5: Receives AuthCode from Access Token



















