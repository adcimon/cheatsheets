# Node.js

<p align="center"><img align="center" width="50%" height="50%" src="assets/nodejs.svg"></p>

[Node.js](https://nodejs.org/) is a JavaScript runtime built on [V8](https://v8.dev/) JavaScript engine.

## Index

* [Install](#install)
* [Packages](#packages)
  * [TypeScript](#typescript)
  * [Tailwind CSS](#tailwind-css)
  * [Nest.js](#nestjs)
  * [Electron](#electron)

# Install

A list of available versions can be found in the [releases](https://nodejs.org/en/blog/release/) section of the blog.

Ubuntu.
```
curl -fsSL https://deb.nodesource.com/setup_current.x -o setup_node.sh
chmod +x setup_node.sh
./setup_node.sh
apt-get install -y nodejs
```

Versions.
```
https://deb.nodesource.com/setup_current.x
https://deb.nodesource.com/setup_14.x
https://deb.nodesource.com/setup_13.x
https://deb.nodesource.com/setup_12.x
https://deb.nodesource.com/setup_11.x
https://deb.nodesource.com/setup_10.x
```

## Packages

[Node Package Manager (npm)](https://www.npmjs.com/) is the package manager of Node.

Update npm.
```
npm install -g npm@latest
```

Initialize a module directory.
```
npm init
```

Run an application.
```
npm run
npm run <script>
npm run --prefix <path/to/package.json> <script>
```

Install all packages.
```
npm install
```

Install a package.
```
npm install <package>
npm install <package>@<version>
npm install git+https://<host>/<user>/<package>.git
npm install git+ssh://git@<host>/<user>/<package>.git
```

Uninstall a package.
```
npm uninstall <package>
```

Install a global package.
```
npm install -g <package>
npm install -g <package>@<version>
```

Uninstall a global package.
* Run `npm list -g`.
* Go to `C:\Users\<User>\AppData\Roaming\npm`.
* Delete the package files.
* Go to `node_modules` and delete the package.

List the global packages.
```
npm list -g
```

Check outdated packages.
```
npm outdated
```

Update packages.
```
npm update
```

Recreate `package-lock.json`.
```
npm install --package-lock-only
```

Symlink a package folder, handy to work and test a package iteratively without having to continually rebuild.
```
npm link <package>
npm unlink <package>
```

Create a `tarball` from a package.
```
npm pack
```

Login to a registry.
```
npm login --registry=<url> --scope=<user>
npm login --registry=https://npm.pkg.github.com --scope=@adcimon
```

Publish a package.
```
npm publish
npm publish <folder>
```

List of packages.
| Package | Install |
|---|---|
| [dotenv](https://github.com/motdotla/dotenv) | npm install dotenv |
| [Electron](https://github.com/electron/electron) | npm install --save-dev electron |
| [Electron Builder](https://github.com/electron-userland/electron-builder) | npm install --save-dev electron-builder |
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
| [React](https://github.com/facebook/react) | npm install react<br>npm install @types/react |
| [React Transition Group](https://github.com/reactjs/react-transition-group) | npm install react-transition-group<br>npm install @types/react-transition-group |
| [Recoil](https://github.com/facebookexperimental/Recoil) | npm install recoil |
| [serve](https://github.com/vercel/serve) | npm install -g serve |
| [SQLite](https://github.com/mapbox/node-sqlite3) | npm install sqlite3 |
| [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss) | npm install -d tailwindcss |
| [TypeORM](https://github.com/typeorm/typeorm) | npm install typeorm<br>npm install @nestjs/typeorm |
| [Typescript](https://github.com/Microsoft/TypeScript) | npm install typescript<br>npm install --save-dev typescript<br>npm install -g typescript |
| [uuid](https://github.com/uuidjs/uuid) | npm install uuid |
| [ws](https://github.com/websockets/ws) | npm install ws<br>npm install @nestjs/websockets<br>npm install @nestjs/platform-ws |
| [Socket.io](https://github.com/socketio/socket.io) | npm install socket.io<br>npm install @nestjs/websockets<br>npm install @nestjs/platform-socket.io |
| [yup](https://github.com/jquense/yup) | npm install yup |

### TypeScript

[TypeScript](https://www.typescriptlang.org/) is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale.

Install.
```
npm install typescript
npm install --save-dev typescript
npm install -g typescript
```

Check version.
```
tsc -v
```

Generate `tsconfig.json`.
```
tsc --init
```

Install base [tsconfig.json](https://github.com/tsconfig/bases) files.
```
npm install --save-dev @tsconfig/recommended
```

### Tailwind CSS

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

### Nest.js

[Nest.js](https://nestjs.com/) is a framework for building efficient, scalable web applications.

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

Run unit tests.
```
npm run test:watch
```

Run integration tests.
```
npm run test:e2e
```

### Electron

[Electron](https://www.electronjs.org/) is a free and open-source software framework developed and maintained by GitHub designed to create desktop applications using web technologies which are rendered using a flavor of the [Chromium](https://www.chromium.org/) browser engine, and a backend using the [Node.js](https://nodejs.org/) runtime environment.

Install.
```
mkdir my-app
cd my-app
npm init
npm install --save-dev electron
```

Build with [Electron Builder](https://www.electron.build/).
```
electron-builder --win [nsis|nsis-web|portable]
```

Startup project.
```
https://github.com/electron-react-boilerplate/electron-react-boilerplate
```
