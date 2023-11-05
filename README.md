# Light Mailer

You can use this automated version of Nodemailer to send emails easily. All you have to do is create a REST API and make a request to it using a frontend with the necessary data which you want to send in the email.

## Why Light Mailer

- Easy to use.
- No any advanced configurations. (Configured everything in nodemailer for you.)
- Best for small projects.



## Installation

You can install this package using npm:

```
npm install light-mailer
```

## Usage

### Quick Tutorial

First import necessary modules into your project:

```
const lightMailer = require('light-mailer');
const express = require("express");
const fs = require("fs");
```

Next, create an email template and read its content like this:

```
const template = fs.readFileSync("./template.html", "utf8");
```

The email template must include placeholders with the exact names of the keys of the JavaScript object which you receive in the request body. (Please declare the placeholders like this: `{{}}` ) In this case, the email template will look like this:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <p>Name - {{name}}</p>
    <p>Name - {{message}}</p>
</body>
</html>
```

Then create a REST API using Express.js and add the API endpoint "/send-mail" as follows:

```
const app = express();
const PORT = 4000 || process.env.PORT;

app.use(express.json());

app.post("/send-mail", (req, res) => {
    // ...
});

app.listen(PORT, (req, res) => {
    console.log("Server is running on port", PORT);
});
```

After that, you can get the data that you want to send as an email from the request body. Next, create a new instance of lightMailer with the necessary arguments. Then call the sendMail function with the data that you want to send as an email and the email template. Finally, write the response as follows:

```
app.post("/send-mail", (req, res) => {
    const data = req.body;

    const mail = new lightMailer(
        "your-gmail@gmail.com",
        "your-gmail-password",
        "sender's-gmail@gmail.com",
        "receiver's-gmail@gmail.com"
    );

    mail.sendMail(data, template);

    res.status(200).json({
        status: "success",
        data: {
            message: "Email sent successfully!",
        },
    });
});
```

> Please make sure that your email address doesn't have two-factor authentication activated.

You can check if the API works using Postman. Just make a POST request to the following link: `127.0.0.1:4000/send-mail/` and add the JSON object below to the request body.
```
{
    "name": "Example",
    "message": "Hello World!"
}
```

Afterward, check the recipient's email address that you provided when creating the lightMailer instance.
<br><br>
This is the end of the quick tutorial.

## Functions & Parameters

> These functions include the lightMailer function, which was created in the quick tutorial. Note that you can use any name for that!

| Function | Parameters |
|----------|----------|
| lightMailer | Email, Password, Sender's email, Receiver's email |
| sendMail | data, template |



## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
