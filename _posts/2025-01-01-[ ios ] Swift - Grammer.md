---
layout: archive
title:  "[ios] Swift Grammer"
---

## if문


```
if (isDarkMode == true) {
    print("다크모드 입니다.")
} else {
    print("다크모드 아닙니다.")
}
```


3항연산자

```swift
var title : String = isDarkMode == true ? "다크모드 입니다" : "다크모드가 아닙니다."

var title2 : String = isDarkMode ? "다크모드 입니다" : "다크모드가 아닙니다."

var title3 : String = !isDarkMode ? "다크모드가 아닙니다." : "다크모드 입니다"
```