
```swift
// Element Interface
protocol Element {
    var 동물이름: String { get }
    var 동물나이: Int { get }
    func accept(visitor: 방문자)
}

class Dog: Element {
    let 동물이름: String
    let 동물나이: Int
    
    init(name: String, age: Int) {
        self.동물이름 = name
        self.동물나이 = age
    }
    
    func accept(visitor: 방문자) {
        visitor.visit(dog: self)
    }
    
    func 물어() {
        print("악!악!악!")
    }
}

class Cat: Element {
    var 동물나이: Int
    let 동물이름: String
    
    init(name: String, age: Int) {
        self.동물이름 = name
        self.동물나이 = age
    }
    
    func accept(visitor: 방문자) {
        visitor.visit(cat: self)
    }
}
```

```swift
// Visitor Interface
protocol 방문자프로토콜 {
    func visit(dog: Dog)
    func visit(cat: Cat)
}

class 방문자: 방문자프로토콜 {
    let 방문자이름: String // 방문자는 accept로 가서 알고리즘을실행시킨다.
    
    init(name: String) {
        self.방문자이름 = name
    }
    
    func visit(dog: Dog) {
        print("\(방문자이름) 왔다 \(dog.동물이름) \(dog.동물나이)")
    }
    
    func visit(cat: Cat) {
        print("\(방문자이름), \(cat.동물이름), \(cat.동물나이)")
    }
}

```

```swift
let dog = Dog(name: "초코", age: 3)
let cat = Cat(name: "냥냥펀치", age: 5)

let vet = 방문자(name: "Hemg")

dog.accept(visitor: vet)
cat.accept(visitor: vet)
```
```swift
Hemg 왔다 초코 3
```

서로 합성관계이다 서로를 참조도 하고있다.

### 언제 사용하면 좋을까요?
- Visitor Pattern 은 적용해야 할 대상 객체(Elements)가 추가되는 경우가 적고, 적용할 로직(Visitor)이 추가될 가능성이 많은 상황일 때 사용을 고려해볼 수 있습니다
