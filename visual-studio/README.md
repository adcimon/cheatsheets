# Visual Studio

<p align="center"><img align="center" width="20%" height="20%" src="assets/visualstudio.svg"></p>

[Visual Studio](https://en.wikipedia.org/wiki/Microsoft_Visual_Studio) is an [integrated development environment (IDE)](https://en.wikipedia.org/wiki/Integrated_development_environment) from Microsoft.

### Inconsistent line endings

* Go to `Edit → Find and Replace → Quick Replace`.
* Check `Use Regular Expressions`.
* Replace `(?<!\r)\n` for `\r\n`

### Hide vertical dotted indentation

* Go to `Tools → Options → Text Editor`.
* Uncheck `Show structure guide lines`.

### Run Debug as Administrator

Go to `app.manifest` → `<requestedPrivileges>` and add the execution level requirement:
```
<requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
```
* When trying to debug, the editor will warn about the admin right and restart itself with admin rights.
* The executable will be marked as requiring admin rights, therefore when deploying is not necessary to configure admin rights in the file properties.
