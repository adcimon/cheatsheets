# Node.js

<p align="center"><img align="center" width="50%" height="50%" src="assets/nodejs.svg"></p>

[Node.js](https://nodejs.org/) is a JavaScript runtime built on [V8](https://v8.dev/) JavaScript engine.

## Index

* [Install](#install)
* [Packages](#packages)
* [Nest.js](#nestjs)
* [Tailwind CSS](#tailwind-css)

# Install

Ubuntu
```
curl -fsSL https://deb.nodesource.com/setup_current.x -o setup_node.sh
chmod +x setup_node.sh
./setup_node.sh
apt-get install -y nodejs
```

Versions
```
https://deb.nodesource.com/setup_current.x
https://deb.nodesource.com/setup_14.x
https://deb.nodesource.com/setup_13.x
https://deb.nodesource.com/setup_12.x
https://deb.nodesource.com/setup_11.x
https://deb.nodesource.com/setup_10.x
```

## Packages

[Node Package Manager (npm)](https://www.npmjs.com/) is a package manager for the JavaScript programming language.

Update npm.
```
npm install -g npm@latest
```

Initialize a module directory, creating a `package.json` file.
```
npm init
```

Run an application.
```
npm run
npm run <script>
npm run --prefix <path/to/package.json> <script>
```

Install a package.
```
npm install -help
npm install <package>
npm install <package>@<version>
```

Uninstall a package.
```
npm uninstall <package>
```

List of packages.
| Packages | Install |
|---|---|
| [dotenv](https://github.com/motdotla/dotenv) | npm install dotenv |
| [fs-extra](https://github.com/jprichardson/node-fs-extra) | npm install fs-extra |
| [ms](https://github.com/vercel/ms) | npm install ms |
| [Multer](https://github.com/expressjs/multer) | npm install multer<br>npm install @types/multer |
| [Nest.js](https://github.com/nestjs/nest) | npm install -g @nestjs/cli |
| [Nest.js Schedule](https://github.com/nestjs/schedule) | npm install @nestjs/schedule<br>npm install @types/cron |
| [Nest.js Serve Static](https://github.com/nestjs/serve-static) | npm install @nestjs/serve-static |
| [Nodemailer](https://github.com/nodemailer/nodemailer) | npm install nodemailer<br>npm install @types/nodemailer |
| [Passport](https://github.com/jaredhanson/passport) | npm install passport<br>npm install @nestjs/passport |
| [Passport Local](https://github.com/jaredhanson/passport-local) | npm install passport-local |
| [Passport JWT](https://github.com/mikenicholson/passport-jwt) | npm install passport-jwt<br>npm install @nestjs/jwt |
| [serve](https://github.com/vercel/serve) | npm install -g serve |
| [SQLite](https://github.com/mapbox/node-sqlite3) | npm install sqlite3 |
| [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss) | npm install -d tailwindcss |
| [TypeORM](https://github.com/typeorm/typeorm) | npm install typeorm<br>npm install @nestjs/typeorm |
| [uuid](https://github.com/uuidjs/uuid) | npm install uuid |
| [ws](https://github.com/websockets/ws) | npm install ws<br>npm install @nestjs/websockets<br>npm install @nestjs/platform-ws |
| [Socket.io](https://github.com/socketio/socket.io) | npm install socket.io<br>npm install @nestjs/websockets<br>npm install @nestjs/platform-socket.io |
| [yup](https://github.com/jquense/yup) | npm install yup |

## Nest.js

[Nest.js](https://nestjs.com/) is a framework for building efficient, scalable Node.js web applications.

Nest is built around the design pattern [Dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) and has a built-in container that resolves relationships between providers using a constructor based dependency injection.
* Providers (classes with `@Injectable()`) are added to the `exports` array of the producer module.
* Modules (classes with `@Module()`) are added to the `imports` array of a consumer module.
* Dynamic modules (classes that use `register` or `forRoot`) should always export the module instead of its services (the module has a configuration necessary for the services to work).

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

## Tailwind CSS

[Tailwind CSS](https://tailwindcss.com/) is a utility-first CSS framework for rapidly building custom user interfaces.

Install.
```
npm install -D tailwindcss
```

Create default configuration file [tailwind.config.js](https://github.com/tailwindlabs/tailwindcss/blob/master/stubs/defaultConfig.stub.js).
```
npx tailwindcss init --full
```

Build CSS.
```
npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch
```

Build CSS with all the classes.
```
module.exports = {
  content: ["./src/**/*.{html,js}"],
  safelist: [
    {
      pattern: /(.*?)/,
    },
  ],
  ...
```
