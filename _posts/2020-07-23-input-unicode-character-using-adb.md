---
title: "Input Unicode Character by Adb"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Android
  - Adb
---

> Source https://stackoverflow.com/questions/14224549/adb-shell-input-unicode-character

`adb shell input` doesn't support unicode character, there is an open project to handle this [ADBKeyBoard](https://github.com/senzhk/ADBKeyBoard)

## Enable/Disable it

Switch to ADBKeyBoard from adb
```
adb shell ime set com.android.adbkeyboard/.AdbIME   
```

Check your available virtual keyboards:
```
adb shell ime list -a  
```

Switch back to original virtual keyboard: (in my case)
```
adb shell ime set com.google.android.apps.automotive.inputmethod/.InputMethodService  
```

## Input

### 1. Sending text input
```
adb shell am broadcast -a ADB_INPUT_TEXT --es msg '你好嗎? Hello?'
```
If it's not working, you can try to input as base64
```
adb shell am broadcast -a ADB_INPUT_B64 --es msg `echo -n '你好嗎? Hello?' | base64`
```

### 2. Sending keyevent code  (67 = KEYCODE_DEL)
```
adb shell am broadcast -a ADB_INPUT_CODE --ei code 67
```

### 3. Sending editor action (2 = IME_ACTION_GO)
```
adb shell am broadcast -a ADB_EDITOR_CODE --ei code 2
```

### 4. Sending unicode characters
To send 😸 Cat
```
adb shell am broadcast -a ADB_INPUT_CHARS --eia chars '128568,32,67,97,116'
```

### 5. Send meta keys
To send Ctrl+Space
```
adb shell am broadcast -a ADB_INPUT_MCODE --eia mcode '4096,62'
```

### 6. CLEAR all text (starting from v2.0)
```
adb shell am broadcast -a ADB_CLEAR_TEXT
```

