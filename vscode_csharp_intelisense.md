# Install the "C# for Visual Studio Code" extention.

In my case something didn't work and I had to install from .vsix\
https://github.com/OmniSharp/omnisharp-vscode/releases

# Enable decompilation support.

%USERPROFILE%\\.omnisharp\omnisharp.json

```
{
    "RoslynExtensionsOptions": {
        "enableDecompilationSupport": true
    }
}
```

# Set path to MSBuild

See: https://lifesaver.codes/answer/omnisharp-tries-to-use-msbuild-16-3-from-visual-studio-2019-in-net-core-3-x-projects-1700

${workspaceFolder}\omnisharp.json

```
{
  "MSBuild": {
    "MSBuildOverride": {
      "MSBuildPath": "C:\\Users\\gkocot\\.vscode\\extensions\\ms-dotnettools.csharp-1.24.0\\.omnisharp\\1.38.0\\.msbuild\\Current\\Bin",
      "Name": "OmniSharp MSBuild",
      "PropertyOverrides": {
        "MSBuildExtensionsPath": "C:\\Users\\gkocot\\.vscode\\extensions\\ms-dotnettools.csharp-1.24.0\\.omnisharp\\1.38.0\\.msbuild"
      }
    }
  }
}
```
