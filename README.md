<p align="center"><img src="media/logo_named_right.png" alt="" width="50%"></p>

# SimpleDialogFragments

[![API 14+](https://img.shields.io/badge/API-14+-green.svg)](https://developer.android.com/about/dashboards/index.html#Platform)
[![Maven Central](https://img.shields.io/maven-central/v/io.github.eltos/simpledialogfragments.svg)](https://search.maven.org/artifact/io.github.eltos/simpledialogfragments)
[![JitPack](https://jitpack.io/v/eltos/SimpleDialogFragments.svg)](https://jitpack.io/#eltos/SimpleDialogFragments)
[![Code Climate Rating](https://codeclimate.com/github/eltos/SimpleDialogFragments/badges/gpa.svg)](https://codeclimate.com/github/eltos/SimpleDialogFragments)
[![Github CI](https://github.com/eltos/SimpleDialogFragments/actions/workflows/build.yml/badge.svg)](https://github.com/eltos/SimpleDialogFragments/actions/workflows/build.yml)
[![License](https://img.shields.io/github/license/eltos/simpledialogfragments.svg)](https://github.com/eltos/SimpleDialogFragments#license)






<img width="40%" align="right" src="https://github.com/eltos/SimpleDialogFragments/raw/main/media/screenshot.png"/>

SimpleDialogFragments Library is a collection of easy to use and extendable DialogFragment's for Android.
It is fully compatible with rotation changes and can be implemented with only a few lines of code.

A new approach of result handling ensures data integrity over rotation changes, that many other libraries lack.



|[JavaDoc API](https://eltos.github.io/SimpleDialogFragments)|[Wiki](https://github.com/eltos/SimpleDialogFragments/wiki)|[Releases](https://github.com/eltos/SimpleDialogFragments/releases)|[Screenshots](https://github.com/eltos/SimpleDialogFragments/wiki/Showcase)|[Demo APK](https://github.com/eltos/SimpleDialogFragments/releases/download/v3.4/testApp.apk)|
|-|-|-|-|-|



### Features

* Common dialogs that can be used with few lines of code
  * Alert dialogs
  * Input and checkbox dialogs with suggestions and validations
  * Filterable single- / multi-choice dialogs
  * Color pickers (palettes and/or HSV)
  * Extensive forms
  * Date and time pickers
  * Pin code dialog
  * Progress dialogs
* Easy result handling even after rotation changes
* Persistence on rotation changes
* Material design
* Customizable and extendable dialogs


## Usage

Check the [release page](https://github.com/eltos/SimpleDialogFragments/releases) for the latest and older versions:

In your module level ``build.gradle`` when using [mavenCentral](https://search.maven.org/artifact/io.github.eltos/simpledialogfragments):
```groovy
dependencies {
    implementation 'io.github.eltos:simpledialogfragments:3.4'
}
```
or if using [JitPack](https://jitpack.io/#eltos/SimpleDialogFragments):
```groovy
dependencies {
    implementation 'com.github.eltos:simpledialogfragments:v3.4'
}
```


### Examples

You can find more examples in the [testApp](testApp/src/main/java/eltos/simpledialogfragments/MainActivity.java) and the [Wiki](https://github.com/eltos/SimpleDialogFragments/wiki).

**Alert dialog**
```java
SimpleDialog.build()
            .title(R.string.hello)
            .msg(R.string.hello_world)
            .show(this);
```
**Choice dialog**
```java
int[] data = new int[]{R.string.choice_A, R.string.choice_B, R.string.choice_C};

SimpleListDialog.build()
                .title(R.string.select_one)
                .choiceMode(ListView.CHOICE_MODE_SINGLE_DIRECT)
                .items(getBaseContext(), data)
                .show(this, LIST_DIALOG);
```
**Color picker**
```java
SimpleColorDialog.build()
                 .title(R.string.pick_a_color)
                 .colorPreset(Color.RED)
                 .allowCustom(true)
                 .show(this, COLOR_DIALOG);
```

**Form dialog**
```java
SimpleFormDialog.build()
                .title(R.string.register)
                .msg(R.string.please_fill_in_form)
                .fields(
                        Input.name(USERNAME).required().hint(R.string.username).validatePatternAlphanumeric(),
                        Input.password(PASSWORD).required().max(20).validatePatternStrongPassword(),
                        Input.email(EMAIL).required(),
                        Input.plain(COUNTRY).hint(R.string.country)
                             .inputType(InputType.TYPE_CLASS_TEXT | InputType.TYPE_TEXT_FLAG_CAP_SENTENCES)
                             .suggest(R.array.countries_locale).forceSuggestion(),
                        Check.box(null).label(R.string.terms_accept).required()
                )
                .show(this, REGISTRATION_DIALOG);
```

**Progress bar dialog**
```java
MyTask task = new MyTask();
task.execute();

SimpleProgressDialog.bar()
        .title(R.string.working)
        .task(task, cancelable, autoDismiss)
        .neg(R.string.continue_in_background)
        .show(this);
```

### Receive Results
Supply a tag when showing the dialog and let the hosting Activity or Fragment implement the `SimpleDialog.OnDialogResultListener`.  
For details, please refere to the [wiki](https://github.com/eltos/SimpleDialogFragments/wiki/SimpleDialog#receiving-results).
```java
@Override
public boolean onResult(@NonNull String dialogTag, int which, @NonNull Bundle extras) {
    if (PASSWORD_DIALOG.equals(dialogTag) && which == BUTTON_POSITIVE){
        String pw = extras.getString(SimpleInputDialogFragment.TEXT);
        // ...
        return true;
    }
    if (LIST_DIALOG.equals(dialogTag) && which == BUTTON_POSITIVE){
        ArrayList<Integer> pos = extras.getIntegerArrayList(SimpleListDialog.SELECTED_POSITIONS);
        // ...
        return true;
    }
    if (REGISTRATION_DIALOG.equals(dialogTag) && which == BUTTON_POSITIVE){
        String username = extras.getString(USERNAME);
        String password = extras.getString(PASSWORD);
        // ...
        return true;
    }
    // ...
    return false;
}

```

## Extensions
Known extensions and projects using this library:
- [File/Folder picker](https://github.com/isabsent/FilePicker) (see [#30](https://github.com/eltos/SimpleDialogFragments/issues/30))

## License

Copyright 2017-2021 Philipp Niedermayer ([github.com/eltos](https://github.com/eltos))

Licensed under the [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)  


You may only use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software in compliance with the License. For more information visit http://www.apache.org/licenses/LICENSE-2.0  
The above copyright notice alongside a copy of the Apache License shall be included in all copies or substantial portions of the Software not only in source code but also in a license listing accessible by the user.  

 
 
I would appreciate being notified when you release an application that uses this library. Thanks!
