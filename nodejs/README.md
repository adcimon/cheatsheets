# Node.js

<p align="center"><img align="center" width="50%" height="50%" src="assets/nodejs.svg"></p>

[Node.js](https://nodejs.org/) is a JavaScript runtime built on [V8](https://v8.dev/) JavaScript engine.

## Index

* [Install](#install)
* [Packages](#packages)
  * [npm](#npm)
  * [Electron](#electron)
  * [NestJS](#nestjs)
  * [Tailwind CSS](#tailwind-css)
  * [TypeScript](#typescript)

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

### npm

[Node Package Manager (npm)](https://www.npmjs.com/) is the package manager of Node.
* `CommonJS` is the original module system (`require`, `module.exports` and `.cjs` files).
* `ECMAScript` module system became a standard and support was added for it (`import`, `export` and `.mjs` files).
* JavaScript `.js` files are treated as whatever the module system for the project is, defined in `package.json`, CommonJS by default or ECMAScript (`"type": "module"`).

Update npm.
```
npm install --global npm@latest
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
* By default saves the package to `dependencies`.
* `--save-dev` saves the package to `devDependencies`.

Move a package from `dev` to `prod` or viceversa.
```
npm install <package> --save-dev
npm install <package> --save-prod
```

Uninstall a package.
```
npm uninstall <package>
```

Install a global package.
```
npm install --global <package>
npm install --global <package>@<version>
```

Uninstall a global package.
* Run `npm list --global`.
* Go to `C:\Users\<user>\AppData\Roaming\npm`.
* Delete the package files.
* Go to `node_modules` and delete the package.

List global packages.
```
npm list --global
```

List packages.
```
npm list --depth=0
```

Check outdated packages.
```
npm outdated
```

Update packages.
```
npm update
npm update --save
npm update <package>
npm update <package> --save
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
| [Axios](https://github.com/axios/axios) | npm install axios |
| [Bowser](https://github.com/bowser-js/bowser) | npm install bowser |
| [dnd](https://github.com/hello-pangea/dnd) | npm install @hello-pangea/dnd |
| [dnd-kit](https://github.com/clauderic/dnd-kit) | npm install @dnd-kit/core |
| [dotenv](https://github.com/motdotla/dotenv) | npm install dotenv |
| [Electron](https://github.com/electron/electron) | npm install --save-dev electron |
| [Electron Builder](https://github.com/electron-userland/electron-builder) | npm install --save-dev electron-builder |
| [esbuild](https://github.com/evanw/esbuild) | npm install --save-exact --save-dev esbuild |
| [fs-extra](https://github.com/jprichardson/node-fs-extra) | npm install fs-extra |
| [ics](https://github.com/adamgibbons/ics) | npm install ics |
| [i18next](https://github.com/i18next/i18next) | npm install i18next react-i18next |
| [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) | npm install jsonwebtoken |
| [lexical](https://github.com/facebook/lexical) | npm install lexical @lexical/react |
| [libphonenumber-js](https://gitlab.com/catamphetamine/libphonenumber-js) | npm install libphonenumber-js |
| [ms](https://github.com/vercel/ms) | npm install ms |
| [Material UI](https://github.com/mui/material-ui) | npm install @mui/material @emotion/react @emotion/styled |
| [Material UI Icons](https://github.com/mui/material-ui) | npm install @mui/icons-material |
| [Moment](https://github.com/moment/moment/) | npm install moment |
| [Multer](https://github.com/expressjs/multer) | npm install multer<br>npm install --save-dev @types/multer |
| [NestJS](https://github.com/nestjs/nest) | npm install --global @nestjs/cli |
| [NestJS Schedule](https://github.com/nestjs/schedule) | npm install @nestjs/schedule<br>npm install --save-dev @types/cron |
| [NestJS Serve Static](https://github.com/nestjs/serve-static) | npm install @nestjs/serve-static |
| [Nodemailer](https://github.com/nodemailer/nodemailer) | npm install nodemailer<br>npm install --save-dev @types/nodemailer |
| [OpenID Connect Provider](https://github.com/panva/node-oidc-provider) | npm install oidc-provider<br>npm install --save-dev @types/oidc-provider |
| [Passport](https://github.com/jaredhanson/passport) | npm install passport<br>npm install @nestjs/passport |
| [Passport Local](https://github.com/jaredhanson/passport-local) | npm install passport-local |
| [Passport JWT](https://github.com/mikenicholson/passport-jwt) | npm install passport-jwt<br>npm install @nestjs/jwt |
| [qrcode](https://github.com/soldair/node-qrcode) | npm install qrcode<br>npm install --save-dev @types/qrcode |
| [React](https://github.com/facebook/react) | npm install react<br>npm install --save-dev @types/react<br>npm install --save-dev @types/react-dom |
| [React Hot Toast](https://github.com/timolins/react-hot-toast) | npm install react-hot-toast |
| [React Transition Group](https://github.com/reactjs/react-transition-group) | npm install react-transition-group<br>npm install --save-dev @types/react-transition-group |
| [Recoil](https://github.com/facebookexperimental/Recoil) | npm install recoil |
| [serve](https://github.com/vercel/serve) | npm install --global serve |
| [SQLite](https://github.com/mapbox/node-sqlite3) | npm install sqlite3 |
| [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss) | npm install --save-dev tailwindcss |
| [Three](https://github.com/mrdoob/three.js) | npm install three<br>npm install --save-dev @types/three |
| [TypeORM](https://github.com/typeorm/typeorm) | npm install typeorm<br>npm install @nestjs/typeorm |
| [Typescript](https://github.com/Microsoft/TypeScript) | npm install typescript<br>npm install --save-dev typescript |
| [uuid](https://github.com/uuidjs/uuid) | npm install uuid |
| [Vite](https://github.com/vitejs/vite) | npm install vite<br>npm install @vitejs/plugin-react |
| [ws](https://github.com/websockets/ws) | npm install ws<br>npm install @nestjs/websockets<br>npm install @nestjs/platform-ws |
| [Socket.io](https://github.com/socketio/socket.io) | npm install socket.io<br>npm install @nestjs/websockets<br>npm install @nestjs/platform-socket.io |
| [yup](https://github.com/jquense/yup) | npm install yup |

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

### NestJS

[NestJS](https://nestjs.com/) is a framework for building efficient, scalable web applications.

NestJS is built around the design pattern [Dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) and has a built-in container that resolves relationships between providers using a constructor based dependency injection.
* Providers (classes with `@Injectable()`) are added to the `exports` array of the producer module.
* Modules (classes with `@Module()`) are added to the `imports` array of a consumer module.
* Dynamic modules (classes that use `register` or `forRoot`) should always export the module instead of its services (the module has a configuration necessary for the services to work).

Install CLI.
```
npm install --global @nestjs/cli
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

### Tailwind CSS

[Tailwind CSS](https://tailwindcss.com/) is a utility-first CSS framework for rapidly building custom user interfaces.

Install.
```
npm install --save-dev tailwindcss
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

### TypeScript

[TypeScript](https://www.typescriptlang.org/) is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale.

Install.
```
npm install typescript
npm install --save-dev typescript
npm install --global typescript
```

Check version.
```
tsc --version
```

Generate `tsconfig.json`.
```
tsc --init
```

Install base [tsconfig.json](https://github.com/tsconfig/bases) files.
```
npm install --save-dev @tsconfig/recommended
```
