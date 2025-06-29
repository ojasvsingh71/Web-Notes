

[](https://app.100xdevs.com/courses/3/169/182#5037d75fb0234d1c860598ec0217cb69 "Step 1 - What are we building, Clone the starter repo")**Step 1 - What are we building, Clone the starter repo**

We’re building a PayTM like application that let’s users send money to each other given an initial dummy balance

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F49a375a4-ed74-4b8c-b0fd-983eabec0e44%2FUntitled.png?table=block&id=fc67110c-b0b5-457e-88e6-03d33bd71326&cache=v2)

#### 

[](https://app.100xdevs.com/courses/3/169/182#dcd1a2a882964b7fbfc631ed7ea83aef "Things to do")**Things to do**

Clone the 8.2 repository from [https://github.com/100xdevs-cohort-2/paytm](https://github.com/100xdevs-cohort-2/paytm)

```
git clone https://github.com/100xdevs-cohort-2/paytm
```

💡

Please keep a MongoDB URL handy before you proceed. This will be your primary database for this assignment 1. Create a free one here - [https://www.mongodb.com/](https://www.mongodb.com/) 2. There is a Dockerfile in the codebase, you can run mongo locally using it.

#### 

[](https://app.100xdevs.com/courses/3/169/182#d889cb3d614748b4bc2ebf556a7396f8 "Explore the repository")**Explore the repository**

The repo is a basic **express + react + tailwind boilerplate**

#### 

[](https://app.100xdevs.com/courses/3/169/182#3cfcddd4c9e64036bc7a350e93f17717 "Backend")**Backend**

1.  Express - HTTP Server

2.  mongoose - ODM to connect to MongoDB

3.  zod - Input validation

```
// index.js
const express = require("express");
const app = express();
```

#### 

[](https://app.100xdevs.com/courses/3/169/182#24d6daa611fd441f86169de6828295cc "Frontend")**Frontend**

1.  React - Frontend framework

2.  Tailwind - Styling framework

```
// App.jsx
function App() {

  return (
    <div>
        Hello world
    </div>
  )
}

export default App
```

## 

[](https://app.100xdevs.com/courses/3/169/182#ecfdbcf7e350419ab07d3faa3276d72c "Step 2 - User Mongoose schemas")**Step 2 - User Mongoose schemas**

We need to support 3 routes for user authentication

1.  Allow user to sign up.

2.  Allow user to sign in.

3.  Allow user to update their information (firstName, lastName, password).

To start off, create the mongo schema for the users table

1.  Create a new file (db.js) in the root folder

2.  Import mongoose and connect to a database of your choice

3.  Create the mongoose schema for the users table

4.  Export the mongoose model from the file (call it User)

### 

Solution

Simple solution

```

// backend/db.js
const mongoose = require('mongoose');

// Create a Schema for Users
const userSchema = new mongoose.Schema({
    username: String,
    password: String,
    firstName: String,
    lastName: String
});

// Create a model from the schema
const User = mongoose.model('User', userSchema);

module.exports = {
	User
};
```

Elegant Solution

```

// backend/db.js
const mongoose = require('mongoose');

// Create a Schema for Users
const userSchema = new mongoose.Schema({
    username: {
        type: String,
        required: true,
        unique: true,
        trim: true,
        lowercase: true,
        minLength: 3,
        maxLength: 30
    },
    password: {
        type: String,
        required: true,
        minLength: 6
    },
    firstName: {
        type: String,
        required: true,
        trim: true,
        maxLength: 50
    },
    lastName: {
        type: String,
        required: true,
        trim: true,
        maxLength: 50
    }
});

// Create a model from the schema
const User = mongoose.model('User', userSchema);

module.exports = {
	User
};
```

## 

[](https://app.100xdevs.com/courses/3/169/182#b96d4384b49e4275934a715352f1ab74 "Step 3 - Create routing file structure")**Step 3 - Create routing file structure**

In the index.js file, route all the requests to `/api/v1` to a apiRouter defined in `backend/routes/index.js`

### 

[](https://app.100xdevs.com/courses/3/169/182#05ba11a26f2f412789d165894c65c14b "Step 1")**Step 1**

Create a new file `backend/routes/index.js` that exports a new express router.

( How to create a router - [https://www.geeksforgeeks.org/express-js-express-router-function/](https://www.geeksforgeeks.org/express-js-express-router-function/) )

### 

Solution

```
// backend/api/index.js
const express = require('express');

const router = express.Router();

module.exports = router;
```

### 

[](https://app.100xdevs.com/courses/3/169/182#142fd086036a40e5945db8118fc25ce9 "Step 2")**Step 2**

Import the router in index.js and route all requests from `/api/v1` to it

### 

Solution

```
// backend/index.js
const express = require("express");
const rootRouter = require("./routes/index");

const app = express();

app.use("/api/v1", rootRouter);
```

## 

[](https://app.100xdevs.com/courses/3/169/182#39549b5b87724b0c81b4c4d91e1ed996 "Step 4 - Route user requests")**Step 4 - Route user requests**

### 

[](https://app.100xdevs.com/courses/3/169/182#68efa0350b3746d2b34792a561bf24c8 "1. Create a new user router")**1. Create a new user router**

Define a new router in `backend/routes/user.js` and import it in the index router.

Route all requests that go to `/api/v1/user` to the user router.

### 

Solution

```
// backend/routes/user.js
const express = require('express');

const router = express.Router();

module.exports = router;
```

### 

[](https://app.100xdevs.com/courses/3/169/182#01f8b26b6a1841aca2e770ffa85f10f3 "2. Create a new user router")**2. Create a new user router**

Import the userRouter in `backend/routes/index.js` so all requests to `/api/v1/user` get routed to the userRouter.

### 

Solution

```
// backend/routes/index.js
const express = require('express');
const userRouter = require("./user");

const router = express.Router();

router.use("/user", userRouter)

module.exports = router;
```

## 

[](https://app.100xdevs.com/courses/3/169/182#378215fdc12f461bada30906a599e818 "Step 5 - Add cors, body parser and jsonwebtoken")**Step 5 - Add cors, body parser and jsonwebtoken**

### 

[](https://app.100xdevs.com/courses/3/169/182#6d72b2ac7ca64729a0aac57c1213899a "1. Add cors")**1. Add cors**

Since our frontend and backend will be hosted on separate routes, add the `cors` middleware to `backend/index.js`

### 

Hint

Look at [https://www.npmjs.com/package/cors](https://www.npmjs.com/package/cors)

### 

Solution

```
// backend/index.js
const express = require('express');
const cors = require("cors");

app.use(cors());

const app = express();


module.exports = router;
```

### 

[](https://app.100xdevs.com/courses/3/169/182#65b23956bff54167a6c75754c3e9c6a0 "2. Add body-parser")**2. Add body-parser**

Since we have to support the JSON body in post requests, add the express body parser middleware to `backend/index.js` You can use the `body-parser` npm library, or use express.json

### 

Hint

[https://medium.com/@mmajdanski/express-body-parser-and-why-may-not-need-it-335803cd048c](https://medium.com/@mmajdanski/express-body-parser-and-why-may-not-need-it-335803cd048c)

### 

Solution

```
// backend/index.js
const express = require('express');
const cors = require("cors");
const rootRouter = require("./routes/index");

const app = express();

app.use(cors());
app.use(express.json());

app.use("/api/v1", rootRouter);
```

### 

[](https://app.100xdevs.com/courses/3/169/182#c6f359944e9e404e8eaa503a45e05d2e "3. Add jsonwebtoken")**3. Add jsonwebtoken**

We will be adding authentication soon to our application, so install jsonwebtoken library. It’ll be useful in the next slide

```
npm install jsonwebtoken
```

### 

[](https://app.100xdevs.com/courses/3/169/182#b553fbdf328c435abad65c6dd79d22fd "4. Export JWT_SECRET")**4. Export JWT_SECRET**

Export a JWT_SECRET from a new file `backend/config.js`

### 

Solution

```
//backend/config.js
module.exports = {
	JWT_SECRET: "your-jwt-secret"
}
```

### 

[](https://app.100xdevs.com/courses/3/169/182#01b50e13a9ba4d5798b833c0d37e64d5 "5. Listen on port 3000")**5. Listen on port** `**3000**`

Make the express app listen on PORT 3000 of your machine

### 

Solution

```
// backend/index.js
... Existing code

app.listen(3000);
```

## 

[](https://app.100xdevs.com/courses/3/169/182#22d4b59c84284b2e958b4cb4513f412a "Step 6 - Add backend auth routes")**Step 6 - Add backend auth routes**

In the user router (`backend/routes/user`), add 3 new routes.

#### 

[](https://app.100xdevs.com/courses/3/169/182#5152fe7e42b74418ba27e773c66680b6 "1. Signup")**1. Signup**

This route needs to get user information, do input validation using zod and store the information in the database provided

1.  Inputs are correct (validated via zod)

2.  Database doesn’t already contain another user

If all goes well, we need to return the user a jwt which has their user id encoded as follows -

```
{
	userId: "userId of newly added user"
}
```

💡

Note - We are not hashing passwords before putting them in the database. This is standard practise that should be done, you can find more details here - [https://mojoauth.com/blog/hashing-passwords-in-nodejs/](https://mojoauth.com/blog/hashing-passwords-in-nodejs/)

**Method: POST** Route: /api/v1/user/signup **Body:**

```
{
	username: "name@gmail.com",
	firstName: "name",
	lastName: "name",
	password: "123456"
}
```

Response:

Status code - 200

```
{
	message: "User created successfully",
	token: "jwt"
}
```

Status code - 411

```
{
	message: "Email already taken / Incorrect inputs"
}
```

### 

Solution

```
const zod = require("zod");
const { User } = require("../db");
const jwt = require("jsonwebtoken");
const { JWT_SECRET } = require("../config");

const signupBody = zod.object({
    username: zod.string().email(),
	firstName: zod.string(),
	lastName: zod.string(),
	password: zod.string()
})

router.post("/signup", async (req, res) => {
    const { success } = signupBody.safeParse(req.body)
    if (!success) {
        return res.status(411).json({
            message: "Email already taken / Incorrect inputs"
        })
    }

    const existingUser = await User.findOne({
        username: req.body.username
    })

    if (existingUser) {
        return res.status(411).json({
            message: "Email already taken/Incorrect inputs"
        })
    }

    const user = await User.create({
        username: req.body.username,
        password: req.body.password,
        firstName: req.body.firstName,
        lastName: req.body.lastName,
    })
    const userId = user._id;

    const token = jwt.sign({
        userId
    }, JWT_SECRET);

    res.json({
        message: "User created successfully",
        token: token
    })
})
```

### 

[](https://app.100xdevs.com/courses/3/169/182#e4b1f1b24f1e4eaba784b605f9c2f63f "2. Route to sign in")**2. Route to sign in**

Let’s an existing user sign in to get back a token.

Method: POST Route: /api/v1/user/signin **Body:**

```

{
	username: "name@gmail.com",
	password: "123456"
}
```

Response:

Status code - 200

```

{
	token: "jwt"
}
```

Status code - 411

```

{
	message: "Error while logging in"
}
```

### 

Solution

```
const signinBody = zod.object({
    username: zod.string().email(),
	password: zod.string()
})

router.post("/signin", async (req, res) => {
    const { success } = signinBody.safeParse(req.body)
    if (!success) {
        return res.status(411).json({
            message: "Incorrect inputs"
        })
    }

    const user = await User.findOne({
        username: req.body.username,
        password: req.body.password
    });

    if (user) {
        const token = jwt.sign({
            userId: user._id
        }, JWT_SECRET);

        res.json({
            token: token
        })
        return;
    }


    res.status(411).json({
        message: "Error while logging in"
    })
})
```

By the end, `routes/user.js` should look like follows

### 

Solution

```
// backend/routes/user.js
const express = require('express');

const router = express.Router();
const zod = require("zod");
const { User } = require("../db");
const jwt = require("jsonwebtoken");
const { JWT_SECRET } = require("../config");

const signupBody = zod.object({
    username: zod.string().email(),
	firstName: zod.string(),
	lastName: zod.string(),
	password: zod.string()
})

router.post("/signup", async (req, res) => {
    const { success } = signupBody.safeParse(req.body)
    if (!success) {
        return res.status(411).json({
            message: "Email already taken / Incorrect inputs"
        })
    }

    const existingUser = await User.findOne({
        username: req.body.username
    })

    if (existingUser) {
        return res.status(411).json({
            message: "Email already taken/Incorrect inputs"
        })
    }

    const user = await User.create({
        username: req.body.username,
        password: req.body.password,
        firstName: req.body.firstName,
        lastName: req.body.lastName,
    })
    const userId = user._id;

    const token = jwt.sign({
        userId
    }, JWT_SECRET);

    res.json({
        message: "User created successfully",
        token: token
    })
})

const signinBody = zod.object({
    username: zod.string().email(),
	password: zod.string()
})

router.post("/signin", async (req, res) => {
    const { success } = signinBody.safeParse(req.body)
    if (!success) {
        return res.status(411).json({
            message: "Email already taken / Incorrect inputs"
        })
    }

    const user = await User.findOne({
        username: req.body.username,
        password: req.body.password
    });

    if (user) {
        const token = jwt.sign({
            userId: user._id
        }, JWT_SECRET);

        res.json({
            token: token
        })
        return;
    }


    res.status(411).json({
        message: "Error while logging in"
    })
})

module.exports = router;
```

## 

[](https://app.100xdevs.com/courses/3/169/182#bf78e516ec2f41b3a948ef90d729c04d "Step 7 - Middleware")**Step 7 - Middleware**

Now that we have a user account, we need to `gate` routes which authenticated users can hit.

For this, we need to introduce an auth middleware

Create a `middleware.js` file that exports an `authMiddleware` function

1.  Checks the headers for an Authorization header `Bearer <token>`

2.  Verifies that the token is valid

3.  Puts the `userId` in the request object if the token checks out.

4.  If not, return a 403 status back to the user

```
Header -
Authorization: Bearer <actual token>
```

### 

Solution

```
const { JWT_SECRET } = require("./config");
const jwt = require("jsonwebtoken");

const authMiddleware = (req, res, next) => {
    const authHeader = req.headers.authorization;

    if (!authHeader || !authHeader.startsWith('Bearer ')) {
        return res.status(403).json({});
    }

    const token = authHeader.split(' ')[1];

    try {
        const decoded = jwt.verify(token, JWT_SECRET);

        req.userId = decoded.userId;

        next();
    } catch (err) {
        return res.status(403).json({});
    }
};

module.exports = {
    authMiddleware
}
```

## 

[](https://app.100xdevs.com/courses/3/169/182#6193f4385abf4aefba68b4946b404f41 "Step 8 - User routes")**Step 8 - User routes**

### 

[](https://app.100xdevs.com/courses/3/169/182#231337cf45804accb8382d116b8af0c5 "1. Route to update user information")**1. Route to update user information**

User should be allowed to `optionally` send either or all of

1.  password

2.  firstName

3.  lastName

Whatever they send, we need to update it in the database for the user. Use the `middleware` we defined in the last section to authenticate the user

Method: PUT Route: /api/v1/user **Body:**

```
{
	password: "new_password",
	firstName: "updated_first_name",
	lastName: "updated_first_name",
}
```

Response:

Status code - 200

```
{
	message: "Updated successfully"
}
```

Status code - 411 (Password is too small…)

```
{
	message: "Error while updating information"
}
```

### 

Solution

```
const  { authMiddleware } = require("../middleware");

// other auth routes

const updateBody = zod.object({
	password: zod.string().optional(),
    firstName: zod.string().optional(),
    lastName: zod.string().optional(),
})

router.put("/", authMiddleware, async (req, res) => {
    const { success } = updateBody.safeParse(req.body)
    if (!success) {
        res.status(411).json({
            message: "Error while updating information"
        })
    }

    await User.updateOne(req.body, {
        _id: req.userId
    })

    res.json({
        message: "Updated successfully"
    })
})
```

### 

[](https://app.100xdevs.com/courses/3/169/182#a736e0a7551d46e8a997d8a65e2b4202 "2. Route to get users from the backend, filterable via firstName/lastName")**2. Route to get users from the backend, filterable via firstName/lastName**

This is needed so users can search for their friends and send them money

Method: GET Route: /api/v1/user/bulk Query Parameter: `?filter=harkirat`

Response:

Status code - 200

```

{
	users: [{
		firstName: "",
		lastName: "",
		_id: "id of the user"
	}]
}
```

### 

Hints

[https://stackoverflow.com/questions/7382207/mongooses-find-method-with-or-condition-does-not-work-properly](https://stackoverflow.com/questions/7382207/mongooses-find-method-with-or-condition-does-not-work-properly)

[https://stackoverflow.com/questions/3305561/how-to-query-mongodb-with-like](https://stackoverflow.com/questions/3305561/how-to-query-mongodb-with-like)

### 

Solution

```
router.get("/bulk", async (req, res) => {
    const filter = req.query.filter || "";

    const users = await User.find({
        $or: [{
            firstName: {
                "$regex": filter
            }
        }, {
            lastName: {
                "$regex": filter
            }
        }]
    })

    res.json({
        user: users.map(user => ({
            username: user.username,
            firstName: user.firstName,
            lastName: user.lastName,
            _id: user._id
        }))
    })
})
```

## 

[](https://app.100xdevs.com/courses/3/169/182#0ccbbfa7d9bf4b589e4c208428b2a3f9 "Step 9 - Create Bank related Schema")**Step 9 - Create Bank related Schema**

Update the `db.js` file to add one new schemas and export the respective models

#### 

[](https://app.100xdevs.com/courses/3/169/182#a301222035e04696be78b9f5014288bd "Accounts table")**Accounts table**

The `Accounts` table will store the INR balances of a user.

The schema should look something like this -

```

{
	userId: ObjectId (or string),
	balance: float/number
}
```

```

In the real world, you shouldn’t store `floats` for balances in the database.
You usually store an integer which represents the INR value with
decimal places (for eg, if someone has 33.33 rs in their account,
you store 3333 in the database).


There is a certain precision that you need to support (which for india is
2/4 decimal places) and this allows you to get rid of precision
errors by storing integers in your DB
```

You should reference the users table in the schema (Hint - [https://medium.com/@mendes.develop/joining-tables-in-mongodb-with-mongoose-489d72c84b60](https://medium.com/@mendes.develop/joining-tables-in-mongodb-with-mongoose-489d72c84b60))

### 

Solution

```
const accountSchema = new mongoose.Schema({
    userId: {
        type: mongoose.Schema.Types.ObjectId, // Reference to User model
        ref: 'User',
        required: true
    },
    balance: {
        type: Number,
        required: true
    }
});

const Account = mongoose.model('Account', accountSchema);

module.exports = {
	Account
}
```

### 

By the end of it, `db.js` should look lie this

```
// backend/db.js
const mongoose = require('mongoose');

mongoose.connect("mongodb://localhost:27017/paytm")

// Create a Schema for Users
const userSchema = new mongoose.Schema({
    username: {
        type: String,
        required: true,
        unique: true,
        trim: true,
        lowercase: true,
        minLength: 3,
        maxLength: 30
    },
    password: {
        type: String,
        required: true,
        minLength: 6
    },
    firstName: {
        type: String,
        required: true,
        trim: true,
        maxLength: 50
    },
    lastName: {
        type: String,
        required: true,
        trim: true,
        maxLength: 50
    }
});

const accountSchema = new mongoose.Schema({
    userId: {
        type: mongoose.Schema.Types.ObjectId, // Reference to User model
        ref: 'User',
        required: true
    },
    balance: {
        type: Number,
        required: true
    }
});

const Account = mongoose.model('Account', accountSchema);
const User = mongoose.model('User', userSchema);

module.exports = {
	User,
  Account,
};
```

## 

[](https://app.100xdevs.com/courses/3/169/182#27ff7faf0934409badbc521fb81a0451 "Step 10 - Transactions in databases")**Step 10 - Transactions in databases**

A lot of times, you want multiple databases transactions to be `atomic`

Either all of them should update, or none should

This is super important in the case of a `bank`

Can you guess what’s wrong with the following code -

```

const mongoose = require('mongoose');
const Account = require('./path-to-your-account-model');

const transferFunds = async (fromAccountId, toAccountId, amount) => {
    // Decrement the balance of the fromAccount
	  await Account.findByIdAndUpdate(fromAccountId, { $inc: { balance: -amount } });

    // Increment the balance of the toAccount
    await Account.findByIdAndUpdate(toAccountId, { $inc: { balance: amount } });
}

// Example usage
transferFunds('fromAccountID', 'toAccountID', 100);
```

### 

Solution

1.  What if the database crashes right after the first request (only the balance is decreased for one user, and not for the second user)

2.  What if the Node.js crashes after the first update? It would lead to a `database inconsistency`. Amount would get debited from the first user, and not credited into the other users account. If a failure ever happens, the first txn should rollback. This is what is called a `transaction` in a database. We need to implement a `transaction` on the next set of endpoints that allow users to transfer INR

## 

[](https://app.100xdevs.com/courses/3/169/182#e180715a5d074deb86b45bbfa4c9aa86 "Step 11 - Initialize balances on signup")**Step 11 - Initialize balances on signup**

Update the `signup` endpoint to give the user a random balance between 1 and 10000.

This is so we don’t have to integrate with banks and give them random balances to start with.

### 

Solution

```
router.post("/signup", async (req, res) => {
    const { success } = signupBody.safeParse(req.body)
    if (!success) {
        return res.status(411).json({
            message: "Email already taken / Incorrect inputs"
        })
    }

    const existingUser = await User.findOne({
        username: req.body.username
    })

    if (existingUser) {
        return res.status(411).json({
            message: "Email already taken/Incorrect inputs"
        })
    }

    const user = await User.create({
        username: req.body.username,
        password: req.body.password,
        firstName: req.body.firstName,
        lastName: req.body.lastName,
    })
    const userId = user._id;

		/// ----- Create new account ------

    await Account.create({
        userId,
        balance: 1 + Math.random() * 10000
    })

		/// -----  ------

    const token = jwt.sign({
        userId
    }, JWT_SECRET);

    res.json({
        message: "User created successfully",
        token: token
    })
})
```

## 

[](https://app.100xdevs.com/courses/3/169/182#1038cbeeb7bf4b81999bdd930e5fba72 "Step 12 - Create a new router for accounts")**Step 12 - Create a new router for accounts**

#### 

[](https://app.100xdevs.com/courses/3/169/182#b917ce4b8ba04184a53d4239734739f6 "1. Create a new router")**1. Create a new router**

All user balances should go to a different express router (that handles all requests on `/api/v1/account` ).

Create a new router in `routes/account.js` and add export it

### 

Solution

```
// backend/routes/account.js
const express = require('express');

const router = express.Router();

module.exports = router;
```

#### 

[](https://app.100xdevs.com/courses/3/169/182#6be6d78692da49339ea5f2b09414ed15 "2. Route requests to it")**2. Route requests to it**

Send all requests from `/api/v1/account/*` in `routes/index.js` to the router created in step 1.

### 

Solution

```
// backend/user/index.js
const express = require('express');
const userRouter = require("./user");
const accountRouter = require("./account");

const router = express.Router();

router.use("/user", userRouter);
router.use("/account", accountRouter);

module.exports = router;
```

## 

[](https://app.100xdevs.com/courses/3/169/182#ab044b6e022146a5b1faee9570d55ced "Step 13 - Balance and transfer Endpoints")**Step 13 - Balance and transfer Endpoints**

Here, you’ll be writing a bunch of APIs for the core user balances. There are 2 endpoints that we need to implement

### 

[](https://app.100xdevs.com/courses/3/169/182#392607dbd92f4f40b5a62f5767f433bc "1. An endpoint for user to get their balance.")**1. An endpoint for user to get their balance.**

Method: GET Route: /api/v1/account/balance

Response:

Status code - 200

```
{
	balance: 100
}
```

### 

Solution

```
router.get("/balance", authMiddleware, async (req, res) => {
    const account = await Account.findOne({
        userId: req.userId
    });

    res.json({
        balance: account.balance
    })
});
```

### 

[](https://app.100xdevs.com/courses/3/169/182#6a5547787bfc4dcc8e8367aa2417e42d "2. An endpoint for user to transfer money to another account")**2. An endpoint for user to transfer money to another account**

Method: POST Route: /api/v1/account/transfer Body

```
{
	to: string,
	amount: number
}
```

Response:

Status code - 200

```
{
	message: "Transfer successful"
}
```

Status code - 400

```
{
	message: "Insufficient balance"
}
```

Status code - 400

```
{
	message: "Invalid account"
}
```

### 

Bad Solution (doesn’t use transactions)

```
router.post("/transfer", authMiddleware, async (req, res) => {
    const { amount, to } = req.body;

    const account = await Account.findOne({
        userId: req.userId
    });

    if (account.balance < amount) {
        return res.status(400).json({
            message: "Insufficient balance"
        })
    }

    const toAccount = await Account.findOne({
        userId: to
    });

    if (!toAccount) {
        return res.status(400).json({
            message: "Invalid account"
        })
    }

    await Account.updateOne({
        userId: req.userId
    }, {
        $inc: {
            balance: -amount
        }
    })

    await Account.updateOne({
        userId: to
    }, {
        $inc: {
            balance: amount
        }
    })

    res.json({
        message: "Transfer successful"
    })
});
```

### 

Good solution (uses txns in db

```
router.post("/transfer", authMiddleware, async (req, res) => {
    const session = await mongoose.startSession();

    session.startTransaction();
    const { amount, to } = req.body;

    // Fetch the accounts within the transaction
    const account = await Account.findOne({ userId: req.userId }).session(session);

    if (!account || account.balance < amount) {
        await session.abortTransaction();
        return res.status(400).json({
            message: "Insufficient balance"
        });
    }

    const toAccount = await Account.findOne({ userId: to }).session(session);

    if (!toAccount) {
        await session.abortTransaction();
        return res.status(400).json({
            message: "Invalid account"
        });
    }

    // Perform the transfer
    await Account.updateOne({ userId: req.userId }, { $inc: { balance: -amount } }).session(session);
    await Account.updateOne({ userId: to }, { $inc: { balance: amount } }).session(session);

    // Commit the transaction
    await session.commitTransaction();
    res.json({
        message: "Transfer successful"
    });
});
```

### 

Problems you might run into

Problems you might run into If you run into the problem mentioned above, feel free to proceed with the bad solution

[https://stackoverflow.com/questions/51461952/mongodb-v4-0-transaction-mongoerror-transaction-numbers-are-only-allowed-on-a](https://stackoverflow.com/questions/51461952/mongodb-v4-0-transaction-mongoerror-transaction-numbers-are-only-allowed-on-a)

### 

[](https://app.100xdevs.com/courses/3/169/182#a597750139b54195be9229a3ac728c2f "Final Solution")****Final Solution****

### 

Finally, the account.js file should look like this

### 

[](https://app.100xdevs.com/courses/3/169/182#43ba58cd153b4ad9a75a21e8cb7bf41d "Experiment to ensure transactions are working as expected")**Experiment to ensure transactions are working as expected**

Try running this code locally. It calls transfer twice on the same account ~almost concurrently

### 

Code

```
// backend/routes/account.js
const express = require('express');
const { authMiddleware } = require('../middleware');
const { Account } = require('../db');
const { default: mongoose } = require('mongoose');

const router = express.Router();

router.get("/balance", authMiddleware, async (req, res) => {
    const account = await Account.findOne({
        userId: req.userId
    });

    res.json({
        balance: account.balance
    })
});

async function transfer(req) {
    const session = await mongoose.startSession();

    session.startTransaction();
    const { amount, to } = req.body;

    // Fetch the accounts within the transaction
    const account = await Account.findOne({ userId: req.userId }).session(session);

    if (!account || account.balance < amount) {
        await session.abortTransaction();
        console.log("Insufficient balance")
        return;
    }

    const toAccount = await Account.findOne({ userId: to }).session(session);

    if (!toAccount) {
        await session.abortTransaction();
        console.log("Invalid account")
        return;
    }

    // Perform the transfer
    await Account.updateOne({ userId: req.userId }, { $inc: { balance: -amount } }).session(session);
    await Account.updateOne({ userId: to }, { $inc: { balance: amount } }).session(session);

    // Commit the transaction
    await session.commitTransaction();
    console.log("done")
}

transfer({
    userId: "65ac44e10ab2ec750ca666a5",
    body: {
        to: "65ac44e40ab2ec750ca666aa",
        amount: 100
    }
})

transfer({
    userId: "65ac44e10ab2ec750ca666a5",
    body: {
        to: "65ac44e40ab2ec750ca666aa",
        amount: 100
    }
})
module.exports = router;
```

### 

Error

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F1c68c51d-0068-4adb-90a9-759d6df8156b%2FUntitled.png?table=block&id=d32313cc-8416-46c1-ad26-aa77f8166323&cache=v2)

## 

[](https://app.100xdevs.com/courses/3/169/182#2aba93bb29dc4b3eb0819f6b5834f877 "Step 14 - Checkpoint your solution")**Step 14 - Checkpoint your solution**

A completely working backend can be found here - [https://github.com/100xdevs-cohort-2/paytm/tree/backend-solution](https://github.com/100xdevs-cohort-2/paytm/tree/backend-solution)

Try to send a few calls via postman to ensure you are able to sign up/sign in/get balance

#### 

[](https://app.100xdevs.com/courses/3/169/182#e4705dd8980e41a0a67d7d8224032b38 "Get balance")**Get balance**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fd046fdcd-b004-483b-a11d-01421a78509d%2FUntitled.png?table=block&id=82287634-53b0-498a-9eca-8e3dc0e74875&cache=v2)

#### 

[](https://app.100xdevs.com/courses/3/169/182#b1a6c927d291407b95fa72d4f75af167 "Make transfer")**Make transfer**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F7cbb08d6-4e6f-436a-a323-85f05ad17547%2FUntitled.png?table=block&id=f8b61f1e-d8ed-4300-b0b9-b682036334fa&cache=v2)

#### 

[](https://app.100xdevs.com/courses/3/169/182#0e515f83b16f4d85a9931008ad6633e6 "Get balance again (notice it went down)")**Get balance again (notice it went down)**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fea699dcf-8c16-4527-b60c-69fe18636a51%2FUntitled.png?table=block&id=09bf4eeb-f3a5-4971-8caf-ed71388ecf95&cache=v2)

#### 

[](https://app.100xdevs.com/courses/3/169/182#ea7597ec523c4514ac875eba7439359c "Mongo should look something like this ")**Mongo should look something like this**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Ffaaa857d-72e5-41aa-8ae4-6cb9d63f07ed%2FUntitled.png?table=block&id=be3a1e8e-c4f8-4692-a969-b1e22b36d28b&cache=v2)

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fc4d73497-fb91-4641-8f7d-4dc80f9cc963%2FUntitled.png?table=block&id=91734648-fa45-4aa5-b798-44ee4b1c58ed&cache=v2)