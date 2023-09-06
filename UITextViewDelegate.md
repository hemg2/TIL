```swift
func textViewShouldBeginEditing(UITextView) -> Bool
Asks the delegate whether to begin editing in the specified text view.
편집 세션을 시작해야 하는 경우 true입니다. 그렇지 않으면 편집을 허용하지 않으려면 false입니다.
flase를 주게 되면 편집을막는다.
```

```swift
func textViewDidBeginEditing(UITextView)
텍스트 편집시에 전달 기능
```

```swift
func textViewShouldEndEditing(UITextView) -> Bool
편집중지 메서드 
편집을 중지해야 하는 경우 true입니다. 그렇지 않으면 편집 세션을 계속해야 하는 경우 false입니다
```

```swift
func textViewDidEndEditing(UITextView)
편집이 종료된 텍스트 보기입니다.
프로젝트 사용시
 func textViewDidEndEditing(_ textView: UITextView) {
       saveContext()
    }
키보드가 멈추게되면  종료 시점으로 되면서 저장되게 진행
```


```swift
func textViewDidChange(UITextView)
사용자가 지정된 텍스트 뷰에서 텍스트 또는 특성을 변경할 때 대리자에게 알립니다.
```
