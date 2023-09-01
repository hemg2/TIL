Cocoapod 사전설치 필수

프로젝트 경로에서 pod init
생성된 Podfile에 target ‘프로젝트명’ do 밑에 아래 내용 추가
pod ‘SwiftLint’

pod install 실행
Target > build phase > + > new run script phase
Run Script에 아래 내용 추가
${PODS_ROOT}/SwiftLint/swiftlint

Run Script 내부 요소 중에 Based on dependency analysis 해제 (빌드시 알림 없애기 위해)
xcodproj 파일 대신 xcworkspace 파일로 실행



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
