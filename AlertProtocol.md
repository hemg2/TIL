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
