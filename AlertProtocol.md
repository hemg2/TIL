```swift
protocol AlertDisplayable {
    func showAlert(title: String?, message: String?, actions: [UIAlertAction], preferredStyle: UIAlertController.Style)
}

extension AlertDisplayable where Self: UIViewController {
    func showAlert(title: String?,
                   message: String?,
                   actions: [UIAlertAction],
                   preferredStyle: UIAlertController.Style) {
        let alertController = UIAlertController(title: title, message: message, preferredStyle: preferredStyle)
        actions.forEach { alertController.addAction($0) }
        
        present(alertController, animated: true)
    }
}

```

```swift
let alertController = UIAlertController(title: nil, message: nil, preferredStyle: .actionSheet)
```
스타일만변경하면 알럿에서 시트로변경이 가능하다! 좋습니다.
