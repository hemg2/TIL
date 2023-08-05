```swift
enum BankManagerNameSpace {
	static let startBankingService: String = "은행 업무 시작"
	static let openBank: String = "1: 은행 개점"
	static let closeBank: String = "2: 종료"
	static let userInput: String = "입력:"
}
SwiftCopy
   private func printMenu() {
        print(BankManagerNameSpace.openBank,
              BankManagerNameSpace.closeBank,
              BankManagerNameSpace.userInput,
              separator: "\n",
              terminator: " ")
    }
```
