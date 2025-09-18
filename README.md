# Lecture 16 - RESTful API (Part 1)

### Create an Express + TypeScript project

Create a project directory and go inside.

```bash
mkdir lecture16
cd lecture16
```

Initialize project using `pnpm`. This creates `package.json` and `pnpm-lock.yaml` files inside your project directory.

```bash
pnpm init
```

Install `Express` as runtime dependency.

```bash
pnpm add express
```
Install necessary development dependencies

```bash
pnpm add -D typescript @types/node @types/express tsx nodemon
```

Open the project with your code editor

```bash
code .
```

Create `tsconfig.ts` to specify Typescript compiler (`tsc`)

```bash
npx tsc --init
```

Open and edit the `tsconfig.ts` file

```json
{
  ...
  "compilerOptions": {
  "target": "esnext",
  "module": "nodenext",
  "strict": true,
  "outDir": "./dist",
  "rootDir": "./src"
  },
  "include": ["src/**/*"]
}
```

Open the `package.json` file and modify the **"type"** and **"scripts"** sections

```json
{
  ...
  "type": "module",
  "scripts": {
  "dev": "npx nodemon --exec tsx src/index.ts",
  "build": "npx tsc",
  "serve": "node dist/index.js",
  },
  ...
}
```
## Simple Express App

```typescript
import express, { Request, Response } from 'express';

const app = express();
const port = 3000;

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

- [src/libs/studentValidator.ts](https://github.com/cpe207-staff/lecture16-2568-done/blob/main/src/schemas/studentSchema.ts)
- [src/libs/courseValidator.ts](https://github.com/cpe207-staff/lecture16-2568-done/blob/main/src/schemas/courseSchema.ts)