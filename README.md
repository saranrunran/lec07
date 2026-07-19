# Lecture 16 - RESTful API (Part 1)

### Get an API Testing tool

Please download `Insomnia` app an install in your PC. This a tool for testing your API.

- [Go to Insomnia website](https://insomnia.rest/)

---

### Content

- How to create `Express + Typescript` project
- Express app structure
  - Route handlers
  - `express.json()` middleware
- How to create `/students` endpoint
  - CRUD operation (`GET`, `POST`, `PUT`, `DELETE` methods)
  - Extract request's `query parameters` using `request.query.{param_name}
  - Extract request's `body` (JSON payload) using `request.body`

---

### Create an Express + TypeScript project

Create a project directory and go inside.

```bash
mkdir <project_dir>
cd <project_dir>
```

Initialize project using `pnpm`. This creates `package.json` and `pnpm-lock.yaml` files inside your project directory.

```bash
pnpm init
```

Install `Express` and other runtime dependency.

```bash
pnpm i express cors helmet morgan debug
```
Install TypeScript and othe necessary development dependencies

```bash
pnpm i –D typescript @tsconfig/node-lts @tsconfig/node-ts tsx tsc-alias
pnpm i -D @types/node @types/express @types/cors @types/morgan @types/debug cross-env nodemon
pnpm approve-builds
```

Open the project with your code editor

```bash
code .
```

### Create and Edit files

Edit `package.json` in the `scripts` section:

```json
"scripts": {
    "dev": "nodemon",
    "build": "tsc && tsc-alias",
    "start": "node ./dist/src/index.js"
 }
```

Create a `tsconfig.json` file as followed: **(update: 19/07/2026)**

```json
{
  "extends": [
    "@tsconfig/node-lts/tsconfig.json",
    "@tsconfig/node-ts/tsconfig.json"
  ],
  "compilerOptions": {
    "types": ["node"],
    "rootDir": ".",
    "outDir": "./dist",
    "paths": {
      "@src/*": ["./src/*"]
    }
  },
  "include": ["./src/**/*"],
  "exclude": ["node_modules"]
}
```
**Note:** 
- We use based configuration for Node.js project from the `@tsconfig/node-lts` and `@tsconfig/nodel-ts` packages.
- We only overwrites what we need for this project.

Create a `.gitignore` file as followed:

```
.env
.env.test
dist
logs
node_modules/
```

Create a `nodemon.json` file as followed:

```json
{
  "watch": ["src",".env"],
  "ext": "js,ts,json",
  "ignore": ["src/logs/*", "src/**/*.{spec,test}.ts"],
  "exec": "tsx src/index.ts"
}
```
This configurations tells `nodemon` to monitor `*.js`, `*.ts`, `*.json` inside the `src` directory. If any of those files are changed, `nodemon` will restart the app automatically.

## Simple Express App (update)

```typescript
import express, { type Request, type Response } from 'express';

const app = express();
const port = 3000;

// An Express middleware that parses request's payload
// make the data available in 'req.body' object
app.use(express.json()); 

app.get('/', (req: Request, res: Response) => {
 res.send('Hello from Express with TypeScript!');
});

app.listen(port, () => {
 console.log(`🚀 Server running on http://localhost:${port}`);
});
```

---

### Running scripts

Run app in development mode (from `src` directory)

```bash
pnpm run dev
```

Build app from `src` and output to `dist` directory

```bash
pnpm run build
```

Run app in production mode (from `dist` directory)

```bash
pnpm run serve
```

---

## Vercel Deployment

When deploy an `Express` project on Vercel, make sure that you configure **Framework Settings** corresponding to your project setup.

Modify the `index.ts` by add the following line of code at the bottom of the file

```typescript
...

export default app

```

#### Framework Settings

1. Framework Preset : `Express`
2. Build Command : `npx tsc`
3. Output Directory : `dist`
4. Install Command : `pnpm install`

This should be enough for our Express project setup

---

## Codes templates

### Interfaces (for data object)
 
 - [src/libs/types.ts](https://github.com/cpe207-staff/lecture16-2568-done/blob/main/src/libs/types.ts)

### Database (variables)

 - [src/db/db.ts](https://github.com/cpe207-staff/lecture16-2568-done/blob/main/src/db/db.ts)

### Zod validators (for HTTP request validation)

Install `zod` as a dependency

```bash
pnpm add zod
```

- [src/libs/studentValidator.ts](https://github.com/cpe207-staff/lecture16-2568-done/blob/main/src/schemas/studentSchema.ts)
- [src/libs/courseValidator.ts](https://github.com/cpe207-staff/lecture16-2568-done/blob/main/src/schemas/courseSchema.ts)