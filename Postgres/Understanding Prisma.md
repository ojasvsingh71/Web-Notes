



# ORMs

Object-Relational Mapping (ORM) is a crucial concept in modern software development, particularly when dealing with databases in object-oriented programming languages. Prisma is an ORM that exemplifies the use of this technique. Here's an elaboration on ORMs, with a focus on how Prisma fits into this context:

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2Ffb396a8a-5a2f-47e3-8c4c-eb5857b70643%2FUntitled.png?table=block&id=307a6d65-ba9b-4f43-9e30-5ae642df39ae&cache=v2)

#### 

[](https://app.100xdevs.com/courses/3/190/227#20f487d097524db7a6df35254a16d6eb "What are ORMs?")**What are ORMs?**

#### 

[](https://app.100xdevs.com/courses/3/190/227#399a8a5342bc4193a5cc150d3433efbb "Official Definition")**Official Definition**

-   **ORM**: Object-Relational Mapping is a programming technique for converting data between incompatible systems using object-oriented programming languages. It creates a "virtual object database" that developers can interact with using their programming language instead of direct database queries.

-   **Abstraction**: ORMs abstract the complexities of the database, allowing developers to work with database records as if they were objects in their code. This includes handling CRUD operations (Create, Read, Update, Delete) and managing database connections and transactions.

#### 

[](https://app.100xdevs.com/courses/3/190/227#f6820cb6127941f09eb2dfd658c47f37 "Simplified Definition")**Simplified Definition**

-   **Ease of Use**: ORMs simplify database interactions by letting developers use the syntax and paradigms of their programming language rather than writing SQL queries. This can make code more readable and maintainable.

#### 

[](https://app.100xdevs.com/courses/3/190/227#c79d2d1d581443fe9533f4ce8baca364 "Prisma as an ORM")**Prisma as an ORM**

Prisma is a next-generation ORM that takes the concept of ORMs further by providing additional tools and features that enhance the developer experience:

-   **Schema Definition**: Prisma uses a declarative Prisma schema to define the application's data model. This schema is used to generate a Prisma Client that provides type-safe database access.

-   **Migrations**: Prisma Migrate allows developers to define and perform database schema migrations in a controlled and versioned manner.

-   **Type Safety**: Prisma ensures type safety by generating a client that is tailored to the schema, reducing the risk of runtime errors due to mismatched data types.

-   **Query Building**: Prisma Client provides a fluent API for building queries, which can be more intuitive than writing raw SQL, especially for complex queries.

-   **Performance**: Prisma is designed to be performant and efficient, with a focus on minimizing the overhead typically associated with ORMs.

> ORMs, including Prisma, offer a high-level abstraction over database interactions, making it easier for developers to work with data in the context of their applications.

## 

[](https://app.100xdevs.com/courses/3/190/227#211e07f916754d6990e22e0df6a64755 "Why ORMs?")Why ORMs?

Object-Relational Mapping (ORM) frameworks provide a bridge between the object-oriented world of application development and the relational world of databases. They offer several advantages that make them an attractive choice for developers. Let's delve into these benefits with explanations and code snippets to illustrate their impact.

#### 

[](https://app.100xdevs.com/courses/3/190/227#3a4b6b99bfc34367b7b07ba7fc914384 "1. Simpler Syntax")1. Simpler Syntax

ORMs allow developers to work with high-level programming constructs instead of writing SQL queries directly. This means you can manipulate database entries using objects and methods in your programming language.

**Without ORM: SQL Query**

```
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
```

**With ORM: Object Manipulation (Example in JavaScript using Prisma)**

```
await prisma.users.create({
  data: {
    name: 'John Doe',
    email: 'john@example.com',
  },
});
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#cf12889a91494be483b5ad64d7c9e999 "2. Database Abstraction")2. Database Abstraction

ORMs provide a unified API to interact with different databases, making it easier to switch databases if needed without rewriting your data access layer.

**Prisma Example**: The same Prisma client code works across different databases. Switching from PostgreSQL to MySQL, for instance, primarily requires changes in the configuration, not in the code that interacts with the database.

**Prisma Schema for PostgreSQL**

```
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

**Prisma Schema for MySQL**

```
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#e30b1aec00984502bfc8c868f8723501 "3. Type Safety/Auto-completion")3. Type Safety/Auto-completion

Modern ORMs, especially those used in statically typed languages or with TypeScript support, offer type safety and auto-completion, reducing runtime errors and improving developer productivity.

**TypeScript Example with Prisma**: When you query the database, the Prisma client provides auto-completion for table names and columns, and the returned data is automatically typed.

```
// TypeScript understands the structure of the expected result,
// providing auto-completion and type checking
const user = await prisma.user.findUnique({
  where: {
    email: 'john@example.com',
  },
});
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#cfb65cc09d114fc9bbc07819fb9033a7 "4. Automatic Migrations")4. Automatic Migrations

ORMs can automate the process of generating and applying database schema migrations, making it easier to evolve your database schema as your application grows.

**Prisma Migration Example**: Prisma Migrate generates SQL migration files for your schema changes, which can be applied to update the database schema.

**Generate Migration**

```
npx prisma migrate dev --name add_phone_number
```

This command might generate a SQL file similar to:

```
-- Migration SQL generated by Prisma Migrate
ALTER TABLE "users"
ADD COLUMN "phone_number" VARCHAR(15);
```

**Apply Migration** Applying migrations is handled by Prisma Migrate when you run the above command, keeping your database schema in sync with your Prisma schema.

## 

[](https://app.100xdevs.com/courses/3/190/227#febfbbb34fe74a70aeaba719b8f6cc1a "Prisma")Prisma

Prisma is a next-generation ORM (Object-Relational Mapping) tool for Node.js and TypeScript applications. It simplifies database workflows by providing a robust set of features that enhance developer productivity and code quality. Let's delve into the core components that make Prisma a powerful tool for modern application development.

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F1b691f2a-30cb-466f-b685-147394d18c0b%2FUntitled.png?table=block&id=8b3d9f7b-5301-4b05-bf97-21d8a72be691&cache=v2)

#### 

[](https://app.100xdevs.com/courses/3/190/227#8a7d8b20a3624f72803f09e75da9871f "1. Data Model")1. Data Model

Prisma uses a Prisma Schema file to define the data model of your application. This schema acts as a single source of truth for your database structure, including tables, columns, relationships, and more. The Prisma Schema Language (PSL) is intuitive yet powerful, allowing you to define your database schema in a clear and concise manner.

**Example Prisma Schema**:

```
// schema.prisma

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  posts     Post[]
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

This schema defines two models, `User` and `Post`, representing tables in the database. It specifies fields for each table, their types, and the relationship between users and posts.

#### 

[](https://app.100xdevs.com/courses/3/190/227#f4134482052f4d40ad6905e62279820f "2. Automated Migrations")2. Automated Migrations

Prisma Migrate is a feature that automatically generates and runs database migrations based on changes to your Prisma schema. This means that when you modify your data model, Prisma Migrate can automatically update your database schema to match, without the need for manual SQL migration scripts.

**Generating and Applying Migrations**:

```
npx prisma migrate dev --name init
```

This command generates SQL migration files for the current state of your Prisma schema and applies them to your database, creating or altering tables and relationships as defined.

#### 

[](https://app.100xdevs.com/courses/3/190/227#987437d0377d44f3a89204dcf782a4ad "3. Type Safety")3. Type Safety

Prisma Client is a type-safe database client generated based on your Prisma schema. This means that every database query you write is checked against the schema, significantly reducing the risk of runtime errors due to data type mismatches. The client provides full auto-completion and type checking in supported editors, making it easier to write and refactor code confidently.

**Example Usage of Prisma Client**:

```
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function main() {
  const newUser = await prisma.user.create({
    data: {
      name: 'Alice',
      email: 'alice@example.com',
    },
  });
  console.log(newUser);
}

main();
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#55c77139d8154d848117aed289cf2cd8 "4. Auto-Completion")4. Auto-Completion

Prisma's integration with code editors (such as VSCode) provides auto-completion for model fields, operations, and even potential query results. This feature not only speeds up development but also helps prevent errors by ensuring that your queries align with the defined schema.

**Auto-Completion Example**: When writing queries with Prisma Client, your editor can suggest model fields, available methods, and more, based on the Prisma schema.

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F1f2e3480-8047-485c-be64-a9a8c88cb3e7%2FUntitled.png?table=block&id=4b40849f-8093-4ed9-be1f-0d4b0859dc07&cache=v2)

## 

[](https://app.100xdevs.com/courses/3/190/227#8333503d6ffb43ae96954d84566129c3 "Installing Prisma")Installing Prisma

Creating a simple TODO app with Prisma in a Node.js environment involves several steps, from initializing your Node.js project to setting up Prisma. Here's a detailed guide to get you started:

#### 

[](https://app.100xdevs.com/courses/3/190/227#0a99a76018d24e738e1b1ec04bf0a72e "Step 1: Initialize an Empty Node.js Project")Step 1: Initialize an Empty Node.js Project

First, create a new directory for your project and navigate into it. Then, initialize a new Node.js project:

```
mkdir todo-app
cd todo-app
npm init -y
```

This command creates a `package.json` file with default values.

#### 

[](https://app.100xdevs.com/courses/3/190/227#54a5c804f17d4b13b55c5c9cfe069790 "Step 2: Add Dependencies")Step 2: Add Dependencies

Install Prisma, TypeScript, ts-node (for running TypeScript files directly), and @types/node (for Node.js type definitions) as development dependencies:

```
npm install prisma typescript ts-node @types/node --save-dev
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#13c57232643c40eea2f3e07b20470f0d "Step 3: Initialize TypeScript")Step 3: Initialize TypeScript

Set up TypeScript in your project:

```
npx tsc --init
```

This command creates a `tsconfig.json` file, which configures TypeScript options.

#### 

[](https://app.100xdevs.com/courses/3/190/227#5bf56b968fc14ab9b1fbc59443f7b607 "Step 4: Configure TypeScript")Step 4: Configure TypeScript

Edit the `tsconfig.json` file to specify the root directory and the output directory for the compiled JavaScript files:

-   Change `"rootDir"` to `"./src"`. This tells TypeScript to look for `.ts` files in the `src` directory.

-   Change `"outDir"` to `"./dist"`. Compiled `.js` files will be output to the `dist` directory.

Your `tsconfig.json` should include these changes like so:

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "rootDir": "./src",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#d958c2c04b98426d8261acfc5db0c356 "Step 5: Initialize a Fresh Prisma Project")Step 5: Initialize a Fresh Prisma Project

Initialize Prisma in your project:

```
npx prisma init
```

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fdd624914-6876-4b58-9694-424f7aa5e22a%2F87101674-4129-4d54-8a81-a8154aeaeab2%2FUntitled.png?table=block&id=58b57206-5c95-4a50-8e53-5d3f8979f879&cache=v2)

This command performs several actions:

-   Creates a `prisma` directory with a `schema.prisma` file inside. This is where you define your database schema.

-   Creates a `.env` file in the root of your project. This is where you set environment variables, such as your database connection string.

#### 

[](https://app.100xdevs.com/courses/3/190/227#753dca976a73467bb5b7e0ea30193061 "Next Steps")Next Steps

After initializing Prisma, you can proceed to define your database schema in the `schema.prisma` file. For a TODO app, you might define a `Todo` model like this:

```
// prisma/schema.prisma

datasource db {
  provider = "postgresql" // Or another database provider like "mysql", "sqlite", etc.
  url      = env("DATABASE_URL")
}

model Todo {
  id        Int      @id @default(autoincrement())
  title     String
  completed Boolean  @default(false)
}
```

Remember to replace `"postgresql"` with your database provider and set your database connection string in the `.env` file:

```
DATABASE_URL="postgresql://user:password@localhost:5432/mydb?schema=public"
```

Finally, to create the `Todo` table in your database, run Prisma Migrate:

```
npx prisma migrate dev --name init
```

This command generates and applies a migration based on your schema changes.

> You can start adding functionality to your TODO app, such as creating, reading, updating, and deleting TODO items using Prisma Client in your application code.

## 

[](https://app.100xdevs.com/courses/3/190/227#e2d32fefffa24e9e8888f79cfbea7b66 "Selecting Your Database")Selecting Your Database

Prisma supports a variety of databases, including relational databases like MySQL and PostgreSQL, as well as the document-oriented database MongoDB (in Preview). Selecting and configuring your database with Prisma involves updating the `schema.prisma` file and setting the database connection URL in your environment variables. Here's how you can do it:

#### 

[](https://app.100xdevs.com/courses/3/190/227#7e5c23af58c040529da0dd24852c197e "Step 1: Update schema.prisma for Your Database")Step 1: Update `schema.prisma` for Your Database

The `schema.prisma` file contains a `datasource` block where you specify your database connection. You need to update the `provider` field according to the database you want to use.

#### 

[](https://app.100xdevs.com/courses/3/190/227#33462b91c78c42e781b8e66464da7d95 "For PostgreSQL")For PostgreSQL

```
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#b6c2b3f206a447088b3fdadc5351d49f "For MySQL")For MySQL

```
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#75c043105db545199e83068059f001e1 "For MongoDB (Preview)")For MongoDB (Preview)

```
datasource db {
  provider = "mongodb"
  url      = env("DATABASE_URL")
}
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#2db38ee08b84426e9619f59f50a3e1fa "Step 2: Set Your Database Connection URL")Step 2: Set Your Database Connection URL

The `url` field in the `datasource` block references an environment variable `DATABASE_URL` where you should set your database connection string. This is done in the `.env` file in the root of your project.

#### 

[](https://app.100xdevs.com/courses/3/190/227#e46a5cb8b4884115a0c1b2e7243fca7c "Example .env Content for PostgreSQL")Example `.env` Content for PostgreSQL

```
DATABASE_URL="postgresql://username:password@localhost:5432/mydatabase"
```

Replace `username`, `password`, `localhost`, `5432`, and `mydatabase` with your actual database credentials and details.

#### 

[](https://app.100xdevs.com/courses/3/190/227#08ef02d18b9c406aa10df8eb7446d251 "Example .env Content for MySQL")Example `.env` Content for MySQL

```
DATABASE_URL="mysql://username:password@localhost:3306/mydatabase"
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#f65189a22f454a85ba4cb6f0ece15f40 "Example .env Content for MongoDB")Example `.env` Content for MongoDB

```
DATABASE_URL="mongodb+srv://username:password@cluster0.example.mongodb.net/mydatabase"
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#7d4dcf41e9dd425982024337293ca361 "Step 3: Install the Prisma VSCode Extension")Step 3: Install the Prisma VSCode Extension

To enhance your development experience with Prisma, it's highly recommended to install the Prisma VSCode extension. This extension provides features like syntax highlighting, formatting, auto-completion, and a visual overview of your Prisma schema.

You can install the Prisma extension directly from the Visual Studio Code Marketplace:

1.  Open VSCode.

2.  Go to the Extensions view by clicking on the square icon on the sidebar or pressing `Ctrl+Shift+X`

3.  Search for "Prisma".

4.  Find the Prisma extension by Prisma and click "Install".

> Remember, when using MongoDB with Prisma, it's currently in Preview, so it's a good idea to keep an eye on the official Prisma documentation for any updates or changes.

## 

[](https://app.100xdevs.com/courses/3/190/227#a86d9847588345afbe35364f2370687a "Defining Models")Defining Models

Defining your data model in Prisma involves specifying the structure of your database tables and their relationships directly in the `schema.prisma` file. This schema acts as a blueprint for your database, allowing Prisma to generate the necessary code to interact with your data in a type-safe manner. Let's walk through the process of defining a data model for a simple application with Users and Todos tables, and then generating the corresponding migrations to update your database schema.

#### 

[](https://app.100xdevs.com/courses/3/190/227#73186081e44d4a72a4b485093fa4f7e6 "Step 1: Define Your Data Model in schema.prisma")Step 1: Define Your Data Model in `schema.prisma`

To add a Users and a Todos table to your application, you'll define two models in your `schema.prisma` file: `User` and `Todo`. At this stage, we won't worry about defining relationships between these tables.

```
// schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql" // Or your database provider of choice
  url      = env("DATABASE_URL")
}

model User {
  id        Int     @id @default(autoincrement())
  username  String  @unique
  password  String
  firstName String
  lastName  String
}

model Todo {
  id          Int     @id @default(autoincrement())
  title       String
  description String
  done        Boolean @default(false)
  userId      Int     // This will later be used to establish a relationship
}
```

In this schema:

-   Each `model` keyword defines a table in your database.

-   The fields within each model represent columns in the table.

-   Attributes like `@id`, `@default(autoincrement())`, and `@unique` specify column constraints and behaviors.

#### 

[](https://app.100xdevs.com/courses/3/190/227#1e6084229ecb47da8228176053d9f3b4 "Step 2: Generate Migrations")Step 2: Generate Migrations

After defining your data model, the next step is to generate migrations to create these tables in your database. Prisma Migrate translates changes in your Prisma schema into SQL migration files, which are then applied to your database to update its schema.

Run the following command to generate and apply migrations:

```
npx prisma migrate dev --name initialize_schema
```

This command does a few things:

-   It generates SQL migration files that represent the schema changes (in this case, creating the `User` and `Todo` tables).

-   It applies these migrations to your database, creating the tables.

-   It generates or updates the Prisma Client, which you use to interact with your database in your application code.

#### 

[](https://app.100xdevs.com/courses/3/190/227#c161de3f9752456cbf0e0dc27377af49 "Step 3: Inspect the Migrations Folder")Step 3: Inspect the Migrations Folder

After running the migrations, you can find them in the `prisma/migrations` folder in your project directory. Each migration is stored in a separate folder, named with a timestamp and the name you provided (`initialize_schema` in this case). Inside, you'll find:

-   A `migration.sql` file containing the SQL commands that were run against your database.

-   A `README.md` file with information about the migration.

Inspecting these files can give you insights into the exact changes made to your database schema.

> By defining your data model in the `schema.prisma` file and using Prisma Migrate, you've successfully created a Users and a Todos table in your database without manually writing any SQL.

This process not only simplifies database schema management but also ensures that your application's data model is version-controlled and easily reproducible across different environments.

## 

[](https://app.100xdevs.com/courses/3/190/227#e12b75529f53489e9ada7034025447f1 "Exploring Your Databases")Exploring Your Databases

Exploring your database with `psql` after Prisma has created tables for you is a straightforward process. `psql` is a command-line interface for interacting with PostgreSQL that allows you to execute queries, view table structures, and manage your database. Here's how you can use `psql` to explore the tables created by Prisma:

#### 

[](https://app.100xdevs.com/courses/3/190/227#4cec95e29550490cb6fc0cc56b20252f "Step 1: Connect to Your Database")Step 1: Connect to Your Database

Open your terminal and use the `psql` command to connect to your PostgreSQL database. Replace `localhost`, `postgres`, and `postgres` with your database's host, database name, and user, respectively, if they are different.

```
psql -h localhost -d postgres -U postgres
```

You might be prompted to enter the password for the PostgreSQL user.

#### 

[](https://app.100xdevs.com/courses/3/190/227#e0aa2ed6616542e0b1d9905fdf980182 "Step 2: List Tables")Step 2: List Tables

Once connected, you can list all the tables in your database using the `\\dt` command.

```
\\dt
```

This command will display a list of tables, including those created by Prisma. You should see the `User` and `Todo` tables listed if you followed the previous steps to define your data model and run migrations.

#### 

[](https://app.100xdevs.com/courses/3/190/227#239a082ef2a34c47b9bb5160f61df680 "Step 3: Describe Table Structure")Step 3: Describe Table Structure

To get detailed information about the structure of a specific table, use the `\\d` command followed by the table name. For example, to describe the `User` table:

```
\\d "User"
```

This will show you the columns, their data types, and any constraints or indexes associated with the table.

#### 

[](https://app.100xdevs.com/courses/3/190/227#647c53197bbe4b9d92cbce7fdd1da518 "Step 4: Query Data")Step 4: Query Data

You can also execute SQL queries directly to retrieve data from your tables. For instance, to select all records from the `User` table:

```
SELECT * FROM "User";
```

#### 

[](https://app.100xdevs.com/courses/3/190/227#e3c92bb45f0f418cad2a9030d8c42309 "Step 5: Exit psql")Step 5: Exit `psql`

When you're done exploring, you can exit `psql` by typing `\\q` and pressing Enter.

```
\\q
```

> Using `psql` to explore your database gives you a direct view of the underlying structure and data. It's a powerful tool for database administration and can be particularly useful for verifying the results of ORM operations, such as those performed by Prisma. Whether you're developing, debugging, or simply curious about the state of your database, `psql` provides the necessary commands to interact with and inspect your PostgreSQL database effectively.

## 

[](https://app.100xdevs.com/courses/3/190/227#42f0bce3d7614eab9e7c26601c53fdc2 "Prisma Client")Prisma Client

#### 

[](https://app.100xdevs.com/courses/3/190/227#f59a2855c56b4438bf4bcd347398f21a "What is a Prisma Client?")What is a Prisma Client?

The Prisma Client is an auto-generated and type-safe query builder that's tailored to your data model. It provides a fluent API that lets you compose queries in a way that is both intuitive and close to natural language. The client abstracts away the SQL layer, offering methods that correspond to various database operations, such as creating, reading, updating, and deleting records.

#### 

[](https://app.100xdevs.com/courses/3/190/227#daa21fd45e3145c0b03ab347d90580ca "How Does the Prisma Client Work?")How Does the Prisma Client Work?

When you use Prisma Client in your application, you write code like this:

```
const newUser = await prisma.user.create({
  data: {
    email: "harkirat@gmail.com",
  },
});
```

Under the hood, Prisma Client converts this operation into an SQL query similar to:

```
INSERT INTO users (email) VALUES ('harkirat@gmail.com');
```

This conversion is handled automatically, so you don't need to write SQL queries manually.

#### 

[](https://app.100xdevs.com/courses/3/190/227#5b2d5dfcfac4499bb90f09ea204b81cb "How to Generate the Prisma Client?")How to Generate the Prisma Client?

After defining your data model in the `schema.prisma` file, you can generate the Prisma Client by running the following command in your terminal:

```
npx prisma generate
```

This command reads your Prisma schema and generates the client code accordingly. The generated client includes all the necessary functions to interact with your database based on the models you've defined.

#### 

[](https://app.100xdevs.com/courses/3/190/227#8f7a2d43f4b34277969e5e2891f8c110 "Using the Generated Prisma Client")Using the Generated Prisma Client

Once generated, you can import and use the Prisma Client in your Node.js application to perform database operations. Here's an example of how you might use the client in an async function:

```
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function main() {
  const newUser = await prisma.user.create({
    data: {
      email: "harkirat@gmail.com",
    },
  });
  console.log(newUser);
}

main()
  .catch(e => {
    throw e;
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
```

In this example, we're using the `create` method on the `user` model to insert a new user into the database. The Prisma Client provides similar methods for other CRUD operations and supports complex queries, including filtering, sorting, and joining data across tables.

## 

[](https://app.100xdevs.com/courses/3/190/227#900dd80efe164c0596950894903b48a5 "Creating Your First Application")Creating Your First Application

### 

[](https://app.100xdevs.com/courses/3/190/227#4957845cfcde46818be9504673eaaa75 "1] Insert")1] Insert

Creating a function to insert data into the `**Users**` table using Prisma in a TypeScript application

The provided solution defines an asynchronous function `insertUser` that takes four parameters: `username`, `password`, `firstName`, and `lastName`. This function uses the Prisma Client to insert a new user into the `Users` table with the provided details.

```
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

async function insertUser(username: string, password: string, firstName: string, lastName: string) {
  const res = await prisma.user.create({
    data: {
        username,
        password,
        firstName,
        lastName
    }
  });
  console.log(res);
}

insertUser("admin1", "123456", "harkirat", "singh");
```

Here's a breakdown of the key parts of this function:

-   **Prisma Client Initialization**: `const prisma = new PrismaClient();` creates a new instance of the Prisma Client. This instance is used to perform operations on your database.

-   **The** `**insertUser**` **Function**: This is an asynchronous function, indicated by the `async` keyword. It's designed to insert a new user into the database.

-   **Inserting Data**: `prisma.user.create()` is a method provided by the Prisma Client to create (or insert) a new record in the `user` table. The method takes an object with a `data` property, which itself is an object containing the fields to be inserted into the table.

-   **Awaiting the Promise**: The `await` keyword is used to wait for the promise returned by `prisma.user.create()` to resolve. This is necessary because database operations are asynchronous.

-   **Logging the Result**: The result of the insert operation (the newly created user record) is stored in the `res` variable and then logged to the console.

-   **Executing the Function**: Finally, `insertUser("admin1", "123456", "harkirat", "singh");` calls the function with sample data. In a real application, you would likely call this function in response to user input, such as a form submission.

### 

[](https://app.100xdevs.com/courses/3/190/227#fd3108fb8c61406ab5ab864bf597c7f9 "2] Update")2] **Update**

Updating data in the `**Users**` table using Prisma in a TypeScript application involves specifying the criteria for selecting the user to update and providing the new data for the selected fields.

The solution defines an asynchronous function `updateUser` that takes a `username` and an object containing the new `firstName` and `lastName` values. This function uses the Prisma Client to update the specified user in the database.

```
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

interface UpdateParams {
    firstName: string;
    lastName: string;
}

async function updateUser(username: string, {
    firstName,
    lastName
}: UpdateParams) {
  const res = await prisma.user.update({
    where: { username },
    data: {
      firstName,
      lastName
    }
  });
  console.log(res);
}

updateUser("admin1", {
    firstName: "new name",
    lastName: "singh"
});
```

Here's a breakdown of the key components:

-   **Prisma Client Initialization**: `const prisma = new PrismaClient();` creates a new instance of the Prisma Client, which is used to interact with your database.

-   **The** `**UpdateParams**` **Interface**: This TypeScript interface defines the shape of the object expected by the `updateUser` function for the update operation. It specifies that both `firstName` and `lastName` should be strings.

-   **The** `**updateUser**` **Function**: This asynchronous function is designed to update a user's `firstName` and `lastName` in the database. It takes a `username` to identify the user to update and an `UpdateParams` object containing the new values.

-   **Updating Data**: `prisma.user.update()` is a method provided by the Prisma Client to update a record in the `user` table. It requires two main arguments:

-   `where`: An object specifying the criteria to find the record to update. In this case, it's the `username` of the user.
-   `data`: An object containing the fields to update and their new values.

-   **Awaiting the Promise**: The `await` keyword pauses execution until the promise returned by `prisma.user.update()` is resolved, ensuring the update operation completes before proceeding.

-   **Logging the Result**: The result of the update operation (the updated user record) is stored in the `res` variable and then logged to the console.

-   **Executing the Function**: The function is called with a sample `username` and new values for `firstName` and `lastName`. In a real application, these values would likely come from user input.

### 

[](https://app.100xdevs.com/courses/3/190/227#7c2c1d22b9a147d1bdf546a75adadc24 "3] Get a User’s Detail")3] Get a User’s Detail

Fetching a user's details from the database based on their username can be done efficiently using Prisma Client.

The solution defines an asynchronous function `getUser` that takes a `username` as an argument. This function uses the Prisma Client to find the first user that matches the given `username`.

```
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

async function getUser(username: string) {
  const user = await prisma.user.findFirst({
    where: {
        username: username
    }
  });
  console.log(user);
}

getUser("admin1");
```

Here's a breakdown of the key components:

-   **Prisma Client Initialization**: `const prisma = new PrismaClient();` creates a new instance of the Prisma Client, which is used to interact with your database.

-   **The** `**getUser**` **Function**: This asynchronous function is designed to fetch a user's details from the database. It takes a `username` to identify the user.

-   **Fetching Data**: `prisma.user.findFirst()` is a method provided by the Prisma Client to retrieve the first record that matches the given criteria from the `user` table. It requires an object with a `where` clause:

-   `where`: An object specifying the criteria to find the record. In this case, it's looking for a user with a matching `username`.

-   **Awaiting the Promise**: The `await` keyword is used to wait for the promise returned by `prisma.user.findFirst()` to resolve. This is necessary because database operations are asynchronous.

-   **Logging the Result**: The result of the fetch operation (the user record) is stored in the `user` variable and then logged to the console.

-   **Executing the Function**: The function is called with a sample `username` of "admin1". In a real application, this value would likely come from user input, such as a login form or a search query.