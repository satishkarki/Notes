# Newsletter

FrameWork Used: [Bootstrap](https://getbootstrap.com/docs/5.1/examples/sign-in/), [MailChimp](https://mailchimp.com/developer/)

MailChimp API key: 2c007072ed8434291e24baf0628b495c-us5

List ID : c20dd7b602

```javascript
const express=require("express");
const bodyParser=require("body-parser");
const request=require("request");

const app=express();

app.use(express.static("public"));
app.use(bodyParser.urlencoded({extended:true}));

app.get("/",function(req,res){
    res.sendFile(__dirname+ "/signup.html");
});

app.post("/",function(req,res){
    const firstName=req.body.fname;
    const lastName=req.body.lname;
    const email=req.body.email;
    // console.log(firstName,lastName,email);
    var data={
        members:[{
            email_address:email,
            status:"subscribed",
            merge_field:{
                FNAME:firstName,
                LNAME:lastName
            }
        }]
    };
    const jsonData=JSON.stringify(data);
    const url="https://us5.api.mailchimp.com/3.0/lists/c20dd7b602"
    const option={
        method:"POST",
        auth:"satish1:2c007072ed8434291e24baf0628b495c-us5"
    }
    const request=https.request(url,option,function(response){
        response.on("data",function(data){
            console.log(JSON.parse(data));
        })
    })
    request.write(jsonData);
    request.end();
});

app.listen(3000, function(){
    console.log("Server is running on port 3000");
});
```



