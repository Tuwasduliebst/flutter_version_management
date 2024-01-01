# flutter_version_management : fvm vs fenv

## The summary of the need for Flutter versioning is as follows:

- Managing multiple projects that require different Flutter SDK versions simultaneously necessitates setting up more than one Flutter SDK.
- Frequent updates in SDK versions require testing new releases and occasionally rolling back to older versions.
- Inconsistencies in Flutter SDK versions among different developers working on the same project can lead to varied execution results despite using the same code.

## Changing the Flutter SDK version typically involves the following process. 
```
// Changing the flutter version
flutter upgrade
flutter downgrade

// If the above command is not supported in your flutter version.
cd {flutter_sdk_path}
git checkout {flutter_version}
flutter doctor
```
- The Flutter SDK is maintained in a GitHub repository, and switching between channels (master/stable/beta) is slow.
- Each time you change the Flutter SDK version, reinstallation and deletion are necessary.
- Installing the SDK versions used and setting them for each project can be more efficient in terms of development environment setup.

Specifying the Flutter SDK version for each project developed in Flutter can alleviate these inconveniences and enable tracking of the Flutter SDK version for each project.

To address these inconveniences, the available tools are primarily fvm and fenv. Both tools fundamentally allow multiple Flutter SDK versions to be downloaded and create symbolic links within each Flutter project to use the desired Flutter SDK version. 

##Environments
The environment variables are as follows
```
- fvm - '$HOME/.pub-cache/bin/fvm'
- fenv - '$HOME/.fenv/bin/fenv'
```  
The flutter SDK installation path is configured as a hidden folder for fenv.
```
- fvm - '$HOME/fvm/versions/{version_name}'
- fenv - '$HOME/.fenv/versions/{version_name}'
```  
After setting up the flutter SDK in the Flutter project, a symbolic link is created, and a file is created in the project path that defines which flutter SDK version the current project uses.

## Commands
The commands for using each tool are listed below. There are no noticeable differences in the commands for using the tools.

|  Command	|  fvm	|  fenv 	|
|---	|---	|---	|
| Get available flutter sdk versions  	| fvm list  	| fenv install -l  	|
| Install flutter SDK  	| fvm install {flutter_version} 	| fenv install {flutter_version}  	|
| Set flutter SDK to current project  	| fvm use {flutter_version}  	| fenv local {flutter_version}  	|
| Run flutter  	| fvm flutter {command}  	| flutter {command}  	|

However, when using Flutter commands, fvm borrows the proxy command format and flutter uses the flutter command format.

## Setup SDK Path in IDE
For fvm, you need to change the SDK settings for both Android Studio and VSCode, but for fenv, you don't need to change the SDK Path setting if you are using VSCode. This is because the default flutter SDK Path is defined as `.flutter` inside VSCode. You can declare it as settings.json > `dart.flutterSdkPath: null` and it will work fine.

## Conclusion
FVM is currently used in many projects and has the advantage of being stable. However, I think fenv is better in terms of development experience, and it works well with VSCode.

## References

[FVM Official Site](https://fvm.app/docs/getting_started/overview/)<br>
[FENV Official Site](https://github.com/fenv-org/fenv/blob/main/README.md)<br>
[FVM으로 Flutter 버전관리 하기](https://velog.io/@kjha2142/Flutter-FVM%EC%9C%BC%EB%A1%9C-Flutter-%EB%B2%84%EC%A0%84%EA%B4%80%EB%A6%AC-%ED%95%98%EA%B8%B0)<br>
[FVM + Sidekick 으로 Flutter 버전관리 하기](https://brunch.co.kr/@devbobby/5)














