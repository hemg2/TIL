# SwuftUI
### SwiftUI의 프로퍼티 래퍼
- @State, @Published 사용 이유:
  - SwiftUI는 데이터의 변화를 감지하고 View를 자동으로 업데이트하기 위해 프로퍼티 래퍼를 사용합니다.
  - @State: View 내부에서 관리되는 데이터에 사용. View의 상태 변경 시 View가 자동으로 업데이트됩니다.
  - @Published: Observable 객체 내부의 데이터에 사용. 데이터 변경 시 관찰자에게 알림을 보냅니다.
