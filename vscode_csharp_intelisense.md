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

# VSCode + OmniSharp on Ubuntu 18.04
OmniSharp couldn't find symbols althoug in the OmniShgarp log there were no errors.  
I had to set in settings.json
```
"omnisharp.useModernNet": false
```
 and [install Mono](https://www.mono-project.com/download/stable/#download-lin):
```
sudo apt install gnupg ca-certificates
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
sudo apt install mono-devel
```
