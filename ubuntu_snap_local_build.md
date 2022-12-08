### HOWTO build the oggw snap locally on Ubuntu 20.04
- See the changes in 'snap-local-on-Ubuntu_20.04' branch, compare ${projectFolder}/snap/snapcraft.yaml
  to the previous version in ${projectFolder}/snap/oggw/snap/snapcraft.yaml;
- Source paths in the snapcraft.yaml had to be modified from ../../<path> to ./<path>
  (other option would be to try using snapcraft --destructive-mode option);
- I don't know what snapcraft version our build system is using, maybe some really old or custiomized one.
  I tried snapcraft version 4.8 and 6.0.2 but the build always failed complaining about the 
  'node-engine' and 'node-package-manager' properties.
  I couldn't find any documentation of the 'node-engine' property of the 'nodejs' plugin.
  At the end I changed 'nodejs' plugin to 'npm' plugin, what also implied changing from core18 to core20
  (building on Ubuntu 20.04 instead of Ubuntu 18.04);
- There is still a problem building nlohmann-json and json-schema-validator prerequisites of the mercuryinterface,
  I have commented out mercuryinterface for now (shouldn't be that hard to set correct library paths, but I was In hurry);
- There is a problem with accessing artifactory.leneldev.com, maybe on Jenkins they have a build node that already has a correct content in the ~/.npmrc ??? The 1st time you run snapcraft --debu it fails and you have to paste the following content to the ~/.npmrc
```
registry=https://artifactory.leneldev.com/artifactory/api/npm/npm-virtual
_auth=Z3J6ZWdvcnoua29jb3RAbGVuZWxkZXYuY29tOkFLQ3A1ZlRhQnJNM1I2eUdXZEY2NkdMNjltdkJ5Nmp6bmhpc0p5Y1phN2lxTVE4NjNtOTM3TVBRS1cxRzFYSnNXR0g2cGo4Vjc=
always-auth=true
email=
strict-ssl=true
unsafe-perm=true
```
- Additionally there are problemns with npm running on root accoun so you have to add the 'unsafe-perm=true' in the ~/.npmrc;
- Looks like on core20 the build precess produces more of, as they described it, 'no-easy-install-files', which has to be removed:
```
- -lib/node_modules/npm/node_modules/node-gyp/gyp/pylib/gyp/__pycache__/__init__.cpython-38.pyc
- -lib/node_modules/npm/node_modules/node-gyp/gyp/pylib/gyp/__pycache__/common.cpython-38.pyc
- -lib/node_modules/npm/node_modules/node-gyp/gyp/pylib/gyp/__pycache__/input.cpython-38.pyc
- -lib/node_modules/npm/node_modules/node-gyp/gyp/pylib/gyp/__pycache__/simple_copy.cpython-38.pyc
- -lib/node_modules/npm/node_modules/node-gyp/gyp/pylib/gyp/__pycache__/xcode_emulation.cpython-38.pyc
- -lib/node_modules/npm/node_modules/node-gyp/gyp/pylib/gyp/generator/__pycache__/__init__.cpython-38.pyc
- -lib/node_modules/npm/node_modules/node-gyp/gyp/pylib/gyp/generator/__pycache__/make.cpython-38.pyc
```
#### Usefull links
ENOTCACHED
https://forum.snapcraft.io/t/npm-err-code-enotcached-npm-install-problem-with-nodejs-plugin/14440
.npmrc
https://forum.snapcraft.io/t/how-can-i-use-npmrc-when-building-node-app/24131
EXAMPLE Node.js snapcraft
https://github.com/ppd/gopass-ui-snap/blob/master/snap/snapcraft.yaml
