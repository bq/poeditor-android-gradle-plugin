# PoEditor Android Gradle Plug-in
[![Release](https://jitpack.io/v/bq/poeditor-android-gradle-plugin.svg)](https://jitpack.io/#bq/poeditor-android-gradle-plugin)

Simple plug-in that eases importing [PoEditor](https://poeditor.com) localized strings to your Android project.

## Purpose
This plug-in super-charges your Android project by providing tasks to download your localized strings from the PoEditor service into you Android project.
It also provides a built-in syntax to handle placeholders to enhance the already awesome Android support from PoEditor.

## Setting Up
In your main `build.gradle`, add [jitpack.io](https://jitpack.io/) repository in the `buildscript` block and include the plug-in as a dependency:

```groovy
buildscript {
    repositories { 
        maven { url 'https://jitpack.io' }
    }
    dependencies {
        classpath 'com.github.bq:poeditor-android-gradle-plugin:1.0.0'
    }
}
```

## How to use
Apply and configure the plug-in in your app's `build.gradle` file:
```groovy
apply plugin: 'com.bq.poeditor'

poEditor {
    apiToken = "your_api_token"
    projectId = 12345
    defaultLang = "en"
    resDirPath = "${project.rootDir}/app/src/main/res"
}
```

The complete attribute list is the following:

Attribute                     | Description
------------------------------|-----------------------------------------
```apiToken```                | PoEditor API Token.
```projectId```               | PoEditor project ID.
```defaultLang```             | The lang to be used to build default ```strings.xml``` (```/values``` folder)
```resDirPath```              | The path to the project's ```/res``` folder.

After the configuration is done, just run the new ```importPoEditorStrings``` task via Android Studio or command line:

```
./gradlew importPoEditorStrings
```

This task will:
* Download all strings files (every available lang) from PoEditor given the api token and project id.
* Process the incoming strings to fix some PoEditor incompatibilities with Android strings system. 
* Create and save strings.xml files to ```/values-<lang>``` (or ```/values``` in case of the default lang). It supports
region specific languages by creating the proper folders (i.e. ```/values-es-rMX```).

## Handling tablet specific strings

You can mark some strings as tablet specific strings by adding ```_tablet```suffix to the string key in PoEditor. 
The plug-in will extract tablet strings to its own XML and save it in ```values-<lang>-sw600dp```.

If you define the following string in PoEditor:
```welcome_message: Hey friend``` and ```welcome_message_tablet: Hey friend how are you doing today, you look great!```

The plug-in will create two `strings.xml` files:

`/values/strings.xml`
```xml
<string name="welcome_message">Hey friend</string>
```

`/values-sw600dp/strings.xml`
```xml
<string name="welcome_message">Hey friend how are you doing today, you look great!</string>
```

## Handle placeholders
You can add placeholders to your strings. We've defined a placeholder markup to use in PoEditor string definition: it uses a double braces syntax, like this one

```
{{value}}
```

The PoEditor string:

```
welcome_message: Hey {{user_name}} how are you
``` 

will become, in `strings.xml`

```xml
<string name="welcome_message">Hey %1%s how are you</string>
```

If you need more than one placeholder in the same string, you can use ordinals too:

PoEditor string:

```
welcome_message: Hey {1{user_name}} how are you, today offer is {2{current_offer}}
``` 

will become, `in strings.xml`

```xml
<string name="welcome_message">Hey %1%s how are you, today offer is %2%s</string>
```

This way you could change the order of the placeholders depending on the language:

PoEditor string with Spanish translation:

```
welcome_message: La oferta del día es {2{current_offer}} para ti, {1{user_name}}
``` 

will become, in `values-es/strings.xml`

```xml
<string name="welcome_message">La oferta del día es %2%s para ti, %1%s</string>
```

## iOS alternative
If you want a similar solution for your iOS projects, check this out: [poeditor-parser-swift](https://github.com/bq/poeditor-parser-swift)

## Authors & Collaborators
* **[Iván Martínez](https://github.com/imartinez)** - *Initial work*
* **[Adrián García](https://github.com/adriangl)** - *Maintainer*

## License
This project is licensed under the Apache Software License, Version 2.0.
```
   Copyright 2016 BQ

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```