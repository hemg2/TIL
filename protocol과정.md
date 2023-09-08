- 프로토콜 생성후 구현 진행
```swift
protocol DateFormattable {
    func formattedDate(from date: Date) -> String
}

extension DateFormattable {
    func formattedDate(from date: Date) -> String {
        let formatter = DateFormatter()
        formatter.dateStyle = .long
        formatter.timeStyle = .short
        formatter.locale = Locale(identifier: "ko_kr")
        formatter.dateFormat = "yyyy/MM/dd"
        return formatter.string(from: date)
    }
}
```

 - 뷰컨 또는 셀에서 사용 예시
 
```swift
class TableViewCell: UITableViewCell, DateFormattable {
    func setModel(_ sample: Sample) {
        dateLabel.text = formattedDate(from: sample.createdAt)
    }
}
// ViewController.swift
class ViewController: UIViewController, DateFormattable {
    func updateDateLabel(with date: Date) {
        dateLabel.text = formattedDate(from: date)
    }
}
```
