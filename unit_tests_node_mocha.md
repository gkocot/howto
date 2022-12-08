# Run specific tests locally

```
cd ${projectFolder}\src
.\node_modules\.bin\mocha --grep 'updateDeviceByHardwareIdWithGatewayFallback'
```
or
```
npm run test -- --grep "when data access layer returns null"
```

# Run\debug mocha unit tests in VSCode

- Install 'Mocha Test Explorer' VSCode extention;
- Open .vscode\launch.json, inside the configuration section prss Ctl+Space and select '{} Node.js: Mocha Tests' option to generate a configuration;
- Correct the paths to the test folder ${workspaceFolder}/src/test and to the mocha executable ${workspaceFolder}/src/node_modules/mocha/bin/\_mocha;
- Set "cwd": "${workspaceFolder}/src";
- Edit .vscode\settings.json

```
{
    "mochaExplorer.files": "src/test/**/*.js",
    "mochaExplorer.cwd": "src",
    // might need this one too (with your appropriate debug config name)
    "mochaExplorer.debuggerConfig": "Mocha Tests"
}
```
