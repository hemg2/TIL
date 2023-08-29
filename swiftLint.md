새로 파일 생성 -> user Interface -> Empty 
혹은 other -> Empty로 파일을 생성한다. 
이름은 무조건 `.swiftlint.yml` 로 만들어야 한다. 파일명이 .으로 시작하므로 숨김파일로 처리된다.


프로젝트 파일 적용시

- disabled_rules: 
Default Rules 중에 비활성화하고 싶은 규칙을 추가한다. 규칙 이름은 SwiftLintFramework Reference 에서 확인할 수 있다.

```swift
disabled_rules:
- trailing_whitespace 후행 공백
- line_length 선 길이

 # SwiftLint 검사에서 제외할 파일 경로
excluded:
- Pods   
- Diary/AppDelegate.swift 
- Diary/SceneDelegate.swift 
```
[swiftLint rule](https://realm.github.io/SwiftLint/rule-directory.html)
