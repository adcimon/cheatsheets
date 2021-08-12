# Node.js

<p align="center"><img align="center" src="nodejs.png"></p>

[Node.js](https://nodejs.org/) is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://v8.dev/).

## Index

* [npm](#npm)
* [Nest.js](#nestjs)
* [Packages](#packages)

## npm

[Node Package Manager (npm)](https://www.npmjs.com/) is a package manager for the JavaScript programming language.

Initialize a module directory, creating a `package.json` file.
```
npm init
```

Install a package.
```
npm install <package>
npm install <package>@<version>
```

Uninstall a package.
```
npm uninstall <package>
```

## Nest.js

[Nest.js](https://nestjs.com/) is a framework for building efficient, scalable Node.js web applications.

Install CLI.
```
npm install -g @nestjs/cli
```

Print version.
```
nest --version
```

Create a new project.
```
nest new myproject
```

Build the application.
```
npm run build
```

Run the application.
```
npm run start:dev
npm run start:debug
npm run start:prod
```

## Packages

[Serve Static](https://www.npmjs.com/package/@nestjs/serve-static)
```
npm install @nestjs/serve-static
```

[WebSockets](https://www.npmjs.com/package/@nestjs/websockets)
```
npm install ws
npm install @nestjs/websockets
npm install @nestjs/platform-ws
```

[socket.io](https://www.npmjs.com/package/socket.io)
```
npm install socket.io
npm install @nestjs/websockets
npm install @nestjs/platform-socket.io
```

[TypeORM](https://www.npmjs.com/package/typeorm)
```
npm install typeorm
npm install @nestjs/typeorm
```

[Passport](https://www.npmjs.com/package/passport)
```
npm install passport
npm install passport-local
npm install @nestjs/passport

npm install passport-jwt
npm install @nestjs/jwt
```

[Schedule](https://www.npmjs.com/package/@nestjs/schedule)
```
npm install @nestjs/schedule
npm install @types/cron
```

[ms](https://www.npmjs.com/package/ms)
```
npm install ms
```

[Nodemailer](https://www.npmjs.com/package/nodemailer)
```
npm install nodemailer
npm install @types/nodemailer
```
