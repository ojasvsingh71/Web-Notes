

[](https://app.100xdevs.com/courses/3/169/184#79a48ed86ff34614837c87f817d307f3 "Step 1 - Add routing to the react app")**Step 1 - Add routing to the react app**

Import `react-router-dom` into your project and add the following routes -

1.  `/signup` - The signup page

2.  `/signin` - The signin page

3.  `/dashboard` - Balances and see other users on the platform.

4.  `/send` - Send money to other users

### 

Solution

```
function App() {
  return (
    <>
       <BrowserRouter>
        <Routes>
          <Route path="/signup" element={<Signup />} />
          <Route path="/signin" element={<Signin />} />
          <Route path="/dashboard" element={<Dashboard />} />
          <Route path="/send" element={<SendMoney />} />
        </Routes>
      </BrowserRouter>
    </>
  )
}
```

## 

[](https://app.100xdevs.com/courses/3/169/184#2bdcb0df2655451294a4ad36962cdd0d "Step 2 - Create and hook up Signup page")**Step 2 - Create and hook up Signup page**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F7976173f-e759-44d1-87bd-3f943f866080%2FUntitled.png?table=block&id=fa22a2b5-cbe4-4506-977e-dfd8dcb37951&cache=v2)

If the user signup is successful, take the user to `/dashboard`

If not, show them an error message

## 

[](https://app.100xdevs.com/courses/3/169/184#4c82ed94d08e4cc1a52a312888c42d2d "Step 3 - Create the signin page")**Step 3 - Create the signin page**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fa06837f8-ce06-4544-9b6d-fa17561db02c%2FUntitled.png?table=block&id=b4232541-ef8f-47e4-bd96-fac1a73d595f&cache=v2)

If the signin in successful, take the user to `/dashboard`

## 

[](https://app.100xdevs.com/courses/3/169/184#3af3878e7f394c0fb14cb24680633fa2 "Step 4 - Dashboard page")**Step 4 - Dashboard page**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fb4e91be0-0329-4cd7-9f27-758c47307959%2FUntitled.png?table=block&id=e640ac20-1037-4304-a47f-171f41035d2d&cache=v2)

Show the user their balance, and a list of users that exist in the database

Clicking on `Send money` should open a modal that lets the user send money

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fbc3d31e8-ebcc-4874-acbb-130363942506%2FUntitled.png?table=block&id=de36195b-98f6-4523-9482-2705cb1100df&cache=v2)

## 

[](https://app.100xdevs.com/courses/3/169/184#598725226bee4bdd8a931f7150d709c0 "Step 5 - Auth Components")**Step 5 - Auth Components**

Full Signup component

You can break down the app into a bunch of components. The code only contains the styles of the component, not any onclick functionality.

### 

[](https://app.100xdevs.com/courses/3/169/184#467821a77d26412b8cc9854c9425468f "1. Heading component")**1. Heading component**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F274f517f-75d7-4d3e-9722-e783cb4687cf%2FUntitled.png?table=block&id=778ecbfd-7a08-40fc-a252-f74e61028301&cache=v2)

### 

Code

```
export function Heading({label}) {
    return <div className="font-bold text-4xl pt-6">
      {label}
    </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#9bacfc597c1a4ebe8d86a8ac3b4b5c83 "2. Sub Heading component")****2. Sub Heading component****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F03ea2557-03b4-4a84-96dc-d746931c3d47%2FUntitled.png?table=block&id=7413ed14-4d93-4b81-b8b8-298e84e066b6&cache=v2)

### 

Code

```
export function SubHeading({label}) {
  return <div className="text-slate-500 text-md pt-1 px-4 pb-4">
    {label}
  </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#2ee285310b2e4428a78b412c2d3dc882 "3. InputBox component")****3. InputBox component****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F96539848-848f-416b-8837-6424b4c4ae1d%2FUntitled.png?table=block&id=20cf0d95-e320-46d0-8829-f4794f4e5481&cache=v2)

### 

Code

```
export function InputBox({label, placeholder}) {
    return <div>
      <div className="text-sm font-medium text-left py-2">
        {label}
      </div>
      <input placeholder={placeholder} className="w-full px-2 py-1 border rounded border-slate-200" />
    </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#8019885790a549f196d345e021242371 "4. Button Component")****4. Button Component****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fee5ed771-e131-41b7-b444-85c5cf023a6b%2FUntitled.png?table=block&id=892ae29d-870a-44d7-a489-e17924cd492c&cache=v2)

### 

Code

```
export function Button({label, onClick}) {
    return <button onClick={onClick} type="button" class=" w-full text-white bg-gray-800 hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2">{label}</button>
}
```

This section was blindly copied from [https://flowbite.com/docs/components/buttons/](https://flowbite.com/docs/components/buttons/)

### 

[](https://app.100xdevs.com/courses/3/169/184#4cf4c51591614f89a8dc95b5c935dbc3 "5. BottomWarning")**5. BottomWarning**

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F7eda0e9f-6d5f-41b8-9f0a-335ff9922259%2FUntitled.png?table=block&id=3aee8030-9658-466c-bd66-0dd4b8befa6a&cache=v2)

### 

Code

```
import { Link } from "react-router-dom"

export function BottomWarning({label, buttonText, to}) {
    return <div className="py-2 text-sm flex justify-center">
      <div>
        {label}
      </div>
      <Link className="pointer underline pl-1 cursor-pointer" to={to}>
        {buttonText}
      </Link>
    </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#b882fcea06ea4987bbb3901d0792ce34 "Full Signup component")****Full Signup component****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F05d592c4-eedc-4bcf-9c19-1783170a31cd%2FUntitled.png?table=block&id=bffded62-800b-4c97-94e5-2f11da007f82&cache=v2)

### 

Code

```
import { BottomWarning } from "../components/BottomWarning"
import { Button } from "../components/Button"
import { Heading } from "../components/Heading"
import { InputBox } from "../components/InputBox"
import { SubHeading } from "../components/SubHeading"

export const Signup = () => {
    return <div className="bg-slate-300 h-screen flex justify-center">
    <div className="flex flex-col justify-center">
      <div className="rounded-lg bg-white w-80 text-center p-2 h-max px-4">
        <Heading label={"Sign up"} />
        <SubHeading label={"Enter your infromation to create an account"} />
        <InputBox placeholder="John" label={"First Name"} />
        <InputBox placeholder="Doe" label={"Last Name"} />
        <InputBox placeholder="harkirat@gmail.com" label={"Email"} />
        <InputBox placeholder="123456" label={"Password"} />
        <div className="pt-4">
          <Button label={"Sign up"} />
        </div>
        <BottomWarning label={"Already have an account?"} buttonText={"Sign in"} to={"/signin"} />
      </div>
    </div>
  </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#6a890253e5794badaaa4ccbd74d3c1c5 "Full Signin component")****Full Signin component****

### 

Code

```
import { BottomWarning } from "../components/BottomWarning"
import { Button } from "../components/Button"
import { Heading } from "../components/Heading"
import { InputBox } from "../components/InputBox"
import { SubHeading } from "../components/SubHeading"

export const Signin = () => {

    return <div className="bg-slate-300 h-screen flex justify-center">
    <div className="flex flex-col justify-center">
      <div className="rounded-lg bg-white w-80 text-center p-2 h-max px-4">
        <Heading label={"Sign in"} />
        <SubHeading label={"Enter your credentials to access your account"} />
        <InputBox placeholder="harkirat@gmail.com" label={"Email"} />
        <InputBox placeholder="123456" label={"Password"} />
        <div className="pt-4">
          <Button label={"Sign in"} />
        </div>
        <BottomWarning label={"Don't have an account?"} buttonText={"Sign up"} to={"/signup"} />
      </div>
    </div>
  </div>
}
```

## 

[](https://app.100xdevs.com/courses/3/169/184#51363b37116a4255ad995a79e706a9eb "Step 6 - Signin-ed Comonents")**Step 6 - Signin-ed Comonents**

### 

[](https://app.100xdevs.com/courses/3/169/184#1e0a7901c5c3410997e330acc0ba0fcd "1. Appbar")****1. Appbar****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fe2eceb08-3b62-4a55-9d1d-83a27dda5943%2FUntitled.png?table=block&id=15c9a249-e88d-4d31-8dd6-b1fc0cc111b5&cache=v2)

### 

Code

```
export const Appbar = () => {
    return <div className="shadow h-14 flex justify-between">
        <div className="flex flex-col justify-center h-full ml-4">
            PayTM App
        </div>
        <div className="flex">
            <div className="flex flex-col justify-center h-full mr-4">
                Hello
            </div>
            <div className="rounded-full h-12 w-12 bg-slate-200 flex justify-center mt-1 mr-2">
                <div className="flex flex-col justify-center h-full text-xl">
                    U
                </div>
            </div>
        </div>
    </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#5ee4ab08f2f84e39ae3cc7900320a74a "2. Balance")****2. Balance****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fd770f99e-3297-4ef1-bbd7-67a08ead5421%2FUntitled.png?table=block&id=0ed11a45-22ba-4880-a104-71201393d291&cache=v2)

### 

Code

```
export const Balance = ({ value }) => {
    return <div className="flex">
        <div className="font-bold text-lg">
            Your balance
        </div>
        <div className="font-semibold ml-4 text-lg">
            Rs {value}
        </div>
    </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#2d4e317c2e9941d3bbee11d738e7dfca "3. Users component")****3. Users component****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F5ceb71d0-7c15-4592-aba9-75bb0c3d07db%2FUntitled.png?table=block&id=88bbaa41-4af0-451a-8b34-78e212f620f3&cache=v2)

### 

Code

```
import { useState } from "react"
import { Button } from "./Button"

export const Users = () => {
    // Replace with backend call
    const [users, setUsers] = useState([{
        firstName: "Harkirat",
        lastName: "Singh",
        _id: 1
    }]);

    return <>
        <div className="font-bold mt-6 text-lg">
            Users
        </div>
        <div className="my-2">
            <input type="text" placeholder="Search users..." className="w-full px-2 py-1 border rounded border-slate-200"></input>
        </div>
        <div>
            {users.map(user => <User user={user} />)}
        </div>
    </>
}

function User({user}) {
    return <div className="flex justify-between">
        <div className="flex">
            <div className="rounded-full h-12 w-12 bg-slate-200 flex justify-center mt-1 mr-2">
                <div className="flex flex-col justify-center h-full text-xl">
                    {user.firstName[0]}
                </div>
            </div>
            <div className="flex flex-col justify-center h-ful">
                <div>
                    {user.firstName} {user.lastName}
                </div>
            </div>
        </div>

        <div className="flex flex-col justify-center h-ful">
            <Button label={"Send Money"} />
        </div>
    </div>
}
```

### 

[](https://app.100xdevs.com/courses/3/169/184#bd8dd6e5fb394eefa85326f43d7bb071 "4. SendMoney Component")****4. SendMoney Component****

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Fdf43800b-aad2-49af-b036-3844c76fa935%2FUntitled.png?table=block&id=d23ad217-dcc2-4e2a-ac40-7b95ad432e7f&cache=v2)

### 

Code

```
export const SendMoney = () => {
    return <div class="flex justify-center h-screen bg-gray-100">
        <div className="h-full flex flex-col justify-center">
            <div
                class="border h-min text-card-foreground max-w-md p-4 space-y-8 w-96 bg-white shadow-lg rounded-lg"
            >
                <div class="flex flex-col space-y-1.5 p-6">
                <h2 class="text-3xl font-bold text-center">Send Money</h2>
                </div>
                <div class="p-6">
                <div class="flex items-center space-x-4">
                    <div class="w-12 h-12 rounded-full bg-green-500 flex items-center justify-center">
                    <span class="text-2xl text-white">A</span>
                    </div>
                    <h3 class="text-2xl font-semibold">Friend's Name</h3>
                </div>
                <div class="space-y-4">
                    <div class="space-y-2">
                    <label
                        class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
                        for="amount"
                    >
                        Amount (in Rs)
                    </label>
                    <input
                        type="number"
                        class="flex h-10 w-full rounded-md border border-input bg-background px-3 py-2 text-sm"
                        id="amount"
                        placeholder="Enter amount"
                    />
                    </div>
                    <button class="justify-center rounded-md text-sm font-medium ring-offset-background transition-colors h-10 px-4 py-2 w-full bg-green-500 text-white">
                        Initiate Transfer
                    </button>
                </div>
                </div>
        </div>
      </div>
    </div>
}
```

## 

[](https://app.100xdevs.com/courses/3/169/184#074693c901894d64b7d006b055a4f2d0 "Step 7 - Wiring up the backend calls")**Step 7 - Wiring up the backend calls**

You can use

1.  fetch or

2.  axios

to wire up calls to the backend server.

The final code looks something like this -

[https://github.com/100xdevs-cohort-2/paytm/tree/complete-solution](https://github.com/100xdevs-cohort-2/paytm/tree/complete-solution) (complete-solution branch on the repo)

The important bits here are -

1.  Signup call - [https://github.com/100xdevs-cohort-2/paytm/blob/complete-solution/frontend/src/pages/Signup.jsx#L36](https://github.com/100xdevs-cohort-2/paytm/blob/complete-solution/frontend/src/pages/Signup.jsx#L36)

2.  Call to get all the users given the filter - [https://github.com/100xdevs-cohort-2/paytm/blob/complete-solution/frontend/src/components/Users.jsx#L13](https://github.com/100xdevs-cohort-2/paytm/blob/complete-solution/frontend/src/components/Users.jsx#L13)

3.  Call to transfer money b/w accounts - [https://github.com/100xdevs-cohort-2/paytm/blob/complete-solution/frontend/src/pages/SendMoney.jsx#L45](https://github.com/100xdevs-cohort-2/paytm/blob/complete-solution/frontend/src/pages/SendMoney.jsx#L45)