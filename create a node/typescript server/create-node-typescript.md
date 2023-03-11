# Setting up the project



## Creating the project
```git
mkdir newProject
cd newProject
npm init -y
```

## Installing dependencies
```git  
npm install --save-dev typescript @types/node ts-node ts-node-dev nodemon
```

## Creating the tsconfig.json file
```git
npx tsc --init
```

## Replace this scripts on your new package.json file
```json
"scripts": {
    "dev": "nodemon src/index.ts",
    "start": "ts-node src/index.ts"
  },
```

## Creating the src folder
```git
mkdir src
touch src/index.ts
```

## Add console.log on index.ts
```ts
console.log('Hello World')
```
## Run the project
```git
npm run start - will start the server.
npm run dev - will start the server and restarts it on every change.
```

