# Calculator

> The resource comes from [microsoft/testbase: Samples and Tools for Test Base for M365. (github.com)](https://github.com/microsoft/testbase)

The app is a calculator with two types: with UI and without UI. It is simply a sample/test app to try out the functionality of Test Base.

## Prerequisites
Make sure you install the softwares below to build.
- [.NET SDK](https://dotnet.microsoft.com/download)

- [Node.js](https://nodejs.org/en/)

  > my version is 14.19.3

- [WiX Toolset](https://github.com/wixtoolset/wix3/releases)
  After installation, add path of wix toolset (e.g, _C:\Program Files (x86)\WiX Toolset v3.14\bin_) to system variables

- Install [Nuget](https://www.nuget.org/downloads)

  > modify content of `%appdata%/NuGet/NuGet.config` as follows:
  >
  > ```xml
  > <?xml version="1.0" encoding="utf-8"?>
  > <configuration>
  >     <packageSources>
  >         <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
  >     </packageSources>
  > </configuration>
  > ```

## Build
Run _build.ps1_ in PowerShell to build, then find the msi under **windows_installer** folder.
After intalling the msi, you will find the calculator under _C:\Program Files (x86)\Calculator_.

## Usage
Calculator is a simple calculator with UI.

CalculatorCLI is a simple command line calculator.
```
    CalculatorCLI.exe 2+2
    CalculatorCLI.exe 88/11
    CalculatorCLI.exe 8*2
```

## modification

### change package.json

change `vue-cli-service electron:build` to `vue-cli-service electron:build --publish never` in `package.json`

```json
{
  "name": "Calculator",
  "version": "0.1.0",
  "private": true,
  "description": "Calaulator app for uitest",
  "author": "youri",
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint",
    "electron:build": "vue-cli-service electron:build --publish never",
    "electron:serve": "vue-cli-service electron:serve",
    "postinstall": "electron-builder install-app-deps",
    "postuninstall": "electron-builder install-app-deps",
    "pack": "npm run electron:build && node ./build_installer.js"
  },
  "main": "background.js",
  "dependencies": {
    "core-js": "^3.8.3",
    "electron-squirrel-startup": "^1.0.0",
    "electron-wix-msi": "^4.0.0",
    "path": "^0.12.7",
    "vue": "^3.2.13",
    "vue-router": "4"
  },
  "devDependencies": {
    "@babel/core": "^7.12.16",
    "@babel/eslint-parser": "^7.12.16",
    "@vue/cli-plugin-babel": "~5.0.0",
    "@vue/cli-plugin-eslint": "~5.0.0",
    "@vue/cli-service": "~5.0.0",
    "electron": "^15.5.5",
    "electron-devtools-installer": "^3.1.0",
    "eslint": "^7.32.0",
    "eslint-plugin-vue": "^8.0.3",
    "vue-cli-plugin-electron-builder": "~2.1.1"
  },
  "eslintConfig": {
    "root": true,
    "env": {
      "node": true
    },
    "extends": [
      "plugin:vue/vue3-essential",
      "eslint:recommended"
    ],
    "parserOptions": {
      "parser": "@babel/eslint-parser"
    },
    "rules": {}
  },
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not dead",
    "not ie 11"
  ]
}

```

### add functional test

Add `testbasepackage`. The resource comes from [testbase/Samples/Package/Functional/Calculator-Appium-Java-Sample at main · microsoft/testbase (github.com)](https://github.com/microsoft/testbase/tree/main/Samples/Package/Functional/Calculator-Appium-Java-Sample) and is restructured to the ideal structure.
