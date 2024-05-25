

확실한 이유를 찾을수는 없었다.
하지만 엔드포인트들을 확인하는 작업중에서 s가 빠지면서 가는 경우가 존재하게 되었다. 이런 점에서 info에서 추가하여 해결 할수있었다.



```swift
  <key>NSAppTransportSecurity</key>
   <dict>
      <key>NSAllowsArbitraryLoads</key>
      <true/>
   </dict>
```
