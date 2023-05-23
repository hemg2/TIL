## 다중 액션함수 하나로 줄이기

```swift
@IBAction func strawBerryStepper(_ sender: UIStepper) {
        strawBerryLabel.text = "\(Int(sender.value))"
    }
@IBAction func bananaStepper(_ sender: UIStepper) {
        bananaLabel.text = Int(sender.value).description
    }
.......
```
이렇게 스테퍼 하나의 액션당 그에 맞는 과일 레이블이 변경되게 진행했었는데 이점 을 줄이기 위해

```swift
@IBAction func changeStockOnLabel(by sender: UIStepper) {
        let stepperAndLabel: [UIStepper: UILabel] = [
            strawBerryStepper: strawBerryStockLabel,
            bananaStepper: bananaStockLabel,
            pineappleStepper: pineappleStockLabel,
            kiwiStepper: kiwiStockLabel,
            mangoStepper: mangoStockLabel
        ]
        
        if let label = stepperAndLabel[sender] {
            label.text = Int(sender.value).description
        }
    }
```

스텝퍼와 레이블 을 하나로 묶어서 입력하면 그게 맞게 변경할 수있게 진행했다.(딕셔너리로 진행했는데 튜플로도 가능할것 같다 그럼 아랫부분이 포문으로 접근하면 될거같은?..)
스텝퍼엔레이블 의 키값에 접근하여 레이블값을 변경 진행 그것의 값을 공유하는형식..



```swift
func showFruitStock() {
        stock = fruitStore.fruitStock()
        
        guard let strawBerryStock = stock[.strawBerry] else { return }
        guard let bananaStock = stock[.banana] else { return }
        guard let pineappleStock = stock[.pineApple] else { return }
        guard let kiwiStock = stock[.kiwi] else { return }
        guard let mangoStock = stock[.mango] else { return }
        
        strawBerryStepper.value = Double(strawBerryStock)
        bananaStepper.value = Double(bananaStock)
        pineappleStepper.value = Double(pineappleStock)
        kiwiStepper.value = Double(kiwiStock)
        mangoStepper.value = Double(mangoStock)
        
        strawBerryLabel.text = stock[.strawBerry]?.description
        bananaLabel.text = stock[.banana]?.description
        pineappleLabel.text = stock[.pineApple]?.description
        kiwiLabel.text = stock[.kiwi]?.description
        mangoLabel.text = stock[.mango]?.description
    }
```


```swift
func showFruitStock() {
        stock = fruitStore.fruitStock()
        
        let fruitStock: [Fruit : UILabel] = [
            .strawBerry: strawBerryLabel,
            .banana: bananaLabel,
            .pineApple: pineappleLabel,
            .kiwi: kiwiLabel,
            .mango: mangoLabel
        ]
        
        for (fruit, label) in fruitStock {
            guard let stock = stock[fruit] else { return }
            label.text = String(stock)
        }
    }
```

- 과일 재고에 접근한다-> 과일이 딕셔너리로 되어있기에 바인딩을하여 사용할수있게 진행
- 이후 스테퍼값에 바인딩값을 연결 진행 -> 과일기본재고값을 연결
-위와 같이 레이블에도 -> 과일기본재고값을 연결
이렇게 하나하나 진행했던 과정을 과일과 레이블을 딕셔너리로 만들어 한번에 진행 할 수있게 진행했다.

코드를 줄일수있는 방법은 정말... 생각을 깊이 하게 된다면.. 조금더 접근하여 줄일수있는것같다..
이러한 과정이 정말 계속해서 해야 머리에 익혀서 트이는것 같다..
우선은 가장 기본적인 방법으로 진행하며 점점 그것을 업데이트 하는걸 반복해서 익혀야 할거 같다.
