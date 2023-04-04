

## 기본 The Basics

Swift는 정수 (integer) =  Int
부동 소수점 (floating-point) =  (Double) 및 Float
부울 (Boolean) 값에 대한 Bool  =  true, false
텍스트 데이터에 대한 String
String을 쪼개면 -> Character이다 
Character 합친것이 String

Swift는 또한 콜렉션 타입 (Collection Types)에서 자세히 다룰 Array, Set, Dictionary 3개의 기본 콜렉션 타입을 제공합니다.


## 변수와 상수
상수와 변수는 사용하기 전에 반드시 선언이 되어야 합니다.
var age: Int = 30 // 변수  값이 변경될수있는값
let name: String = "John" // 상수 변하지않는값

#### 타입 명시하기
쓰려고하는 타입을 명시하는것이 좋다.
var age = 1 
이런식으로 써도 타입 추론이가능해서 좋지만 가독성이 떨어지므로 
var age: Int = 1
상수, 변수 선언후 타입을 명시후 사용하기.

코드에서 저장한 값이 변경되지 않는다면 항상 let 키워드로 상수로 선언해야 합니다. 변수는 오직 값을 저장하고 변경이 필요할 때 선언합니다.

#### 상수, 변수 네이밍
상수와 변수 이름은 유니코드 (Unicode) 문자를 포함하여 대부분의 문자를 포함할 수 있습니다.

let n = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"

(하지만 지금 저희가 사용하는부분에 있어서는 다른문자를 쓰고있지는않습니다.)

#### 상수, 변수 출력하기
print(n)  // 3.14159 프린트 진행
print("\(n)의 값은 파이?") // 3.14159의 값은 파이?
\()를 사용하여 문자열 삽입을 통하여 진행(자세한건 문자열때..)


#### 주석
var: Int = 1  //나이는 1살
// var: Int = 1  
// 을 붙혀 주석처리 를 진행
주석처리된것은 컴파일시에 무시된다.
주로 설명? 을 하기 위해서 나타낸다.
/* 월화수목금토일 오늘은 목요일... */
을 사용하면  /*을 기준으로 안에 있는 것들이 주석으로 정리가 된다. 


#### 정수 타입
각 정수 타입의 min 과 max 프로퍼티를 통해 각 정수 타입의 최소값과 최대값을 가져올 수 있습니다
UInt = 양수만 있다. 
let minValue = UInt8.min  // 0
let maxValue = UInt8.max  // 255
let maxValue = UInt16.max  // 65535
let maxValue = UInt32.max //4294967295
let maxValue = UInt64.max  // 18446744073709551615
min은 어떤수를 하더라도 0 이기에 max만 실험진행
UInt 을 아직까지는 필요로 한적은없었습니다.
그치만 알고 있다면? 필요로 할때 쓰이지 않을까 생각됩니다.

Int는 양,음 다가지고 있죠.
let ValueMin = Int.min  // -9223372036854775808
let ValueMax = Int.max  // 9223372036854775807
Int8.min  // -128
Int8.max  // 128
Int16.min // -32768
Int16.max // 32768
Int32.min // -2147483648
Int32.max // 2147483648
Int64.min // -9223372036854775808
Int64.max // 9223372036854775807

#### 부동 소수점 숫자
Double 은 64-bit 부동 소수점 숫자를 표기
Float 는 32-bit 부동 소수점 숫자를 표기

Double 이 더많은 소수점을 표기한다?
Double 은 최소 15자리의 소수점 정확도를 가지고 있으며
Float 는 더 적은 6자리의 정확도를 가집니다. 
사용할 적절한 부동 소수점 타입은 코드에서 작업해야하는 값의 특성과 범위에 따라 다릅니다. 두 타입 중에는 Double 이 선호됩니다.


#### 숫자 리터럴 (Numeric Literals)

let decimalInteger = 17
let binaryInteger = 0b10001 // 17
let octalInteger = 0o21 // 17 
let hexadecimalInteger = 0x11 // 17 
진수로 계산해서도 나타난다... 그치만 잘 쓰지는 않는거같습니다..

#### 부울(Booleans)
부울 값은 참과 거짓의 값만 가집니다.
Swift는 2개의 부울 상수 값인 true 와 false 를 제공합니다:
let orangesAreOrange = true
let turnipsAreDelicious = false
기본값은 거짓 = false 이다.

let i = 1
if i == 1 {
    // 참
} else {
 // 거짓
}
부울 값은 조건문에서 많이 사용하게 됩니다



#### 타입 별칭
typealias AudioSample = UInt16  //유인트16선언하기 
var maxAmplitudeFound = AudioSample.min
// 기본선언으로 min값을줘서 0으로 진행
maxAmplitudeFound = 1  // 이렇게 변경하여 사용가능
//그치만 굳이 이런 방법을 쓸지는 모르겠네요..


#### 튜플 (Tuples)
튜플 (Tuples) 은 여러값을 단일 복합 값으로 그룹화 합니다. 튜플안에 값은 어떠한 타입도 가능하며 서로 같은 타입일 필요는 없습니다.
let http404Error = (404, "Not Found")
print(http404Error)


추가적으로 2가지의 원소를 가지고 있는 http404Error를
새로운 변수에 0, 1 번째로 할당해서 나눠서 사용할수있다.
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
404 튜플의 첫번째 인덱스값 statusCode = 404
// Prints "The status code is 404"


404 튜플의 두번째 인덱스값 statusMessage = "Not Found"
print("The status message is \(statusMessage)")
// Prints "The status message is Not Found"


print("The status code is \(http404Error.0)")
print("The status code is \(http404Error.1)")
// Prints "The status code is 404"
// Prints "The status message is Not Found"
이런식으로 사용이 가능하다.



let http200Status = (statusCode: 200, description: "OK", test: "tom")
상수를 선언하여 튜플로 정의 후 2가지의 타입을 만들어 진행한다.

print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"

print("The status message is \(http200Status.description)")
// Prints "The status message is OK"

print("The status message is \(http200Status.test)")
// Print "The status message is tom"


## `옵셔널`
값이 없는 경우에 옵셔널 (optionals) 을 사용합니다. 옵셔널은 2가지 가능성이 있습니다: 값이 있고 옵셔널을 풀어서 값에 접근하거나 값이 없을 수도 있습니다.

let possibleNumber = "123"
var convertedNumber = Int(possibleNumber  //스트링값에서 인트값으로
var serverResponseCode: Int? = 404  // ?옵셔너을 줘서 값이 있을수도 있고 없을수도 있다고 정의한다.

serverResponseCode
serverResponseCode = nil  //변수에 nil을 할당하여 값이 없음을 나타낼수있다.


- if 구문과 강제 언래핑
if serverResponseCode != nil {
    print("convertedNumber contains some integer value.")
} else {
    print("else")
}
// 170번 줄에서 nil 로 정의했기때문에 else 진행


옵셔널에 값이 포함되어 있다고 확신하면 옵셔널 이름 끝에 느낌표 (!)를 추가하여 값에 접근할 수 있습니다.
여기서 느낌표란 "이 옵셔널은 확실히 값을 가지고 있습니다. 사용해도 괜찮습니다."라는 의미입니다.
값을 확실하게 알고 있더라도 !는 사용하지 않는것이 좋습니다.
if serverResponseCode != nil {
    print("convertedNumber has an integer value of \(convertedNumber!).")
} else {
    print("else")
}

- 옵셔널 바인딩
옵셔널 바인딩 (optional binding) 은 옵셔널이 값을 포함하고 있는지 확인하고 값이 있는 경우 해당 값을 임시 상수 또는 변수로 사용할 수 있게 해줍니다. 

강제 언래핑 (forced unwrapping) 보다 옵셔널 바인딩을 사용하여 옵셔널 (Optionals) 섹선에 있는 예제의 possibleNumber 를 다시 작성할 수 있습니다:


if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} 
else { print("else") }
//The string "123" has an integer value of 123

"Int(possibleNumber) 에 의해 반환된 옵셔널 Int 에 값이 포함되어 있으면 actualNumber 라는 새로운 상수에 옵셔널에 포함된 값을 설정합니다."
actualNumber(if let안에서만 사용가능), possibleNumber(밖에서 할당되었지만 가능하네?) 똑같은 값이 나타난다.


let myNumber = Int(possibleNumber)
if let myNumber = myNumber {
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
//새로운 변수에 기존 옵셔널을 할당해서 if let 바인딩하여 사용하기


- 암시적으로 언래핑 된 옵셔널
옵셔널을 만들기위해 타입뒤에 물음표 (String?)를 작성하는 대신에 느낌표 (String!) 로 암시적으로 언래핑 된 옵셔널을 작성합니다.

항상 값이 있다고 가정할수있을경우 !를 사용하여 
옵셔널을 암시적으로 언래핑 된 옵셔널 (implicitly unwrapped optionals)로 정의됩니다.

항상 값이 있는 경우라.. readline으로 값을줘서 실행하는경우에는?
!써도 되지않을까 생각되긴하는데 굳이 사용해야할지 의문이 든다.

let possibleString: String? = "An optional string."
let forcedString: String = possibleString!
// requires an exclamation point
타입에 ? 을 주면서 기본값이 있으니 !로 나타난다...



### 에러 처리
프로그램이 실행되는 동안 에러가 발생할 때 처리하기위해 에러 처리를 진행합니다.

func makeASandwich() throws { }
함수 선언후 throws 라는 메소드를 입력하여 에러를 던지게끔진행한다.

do catch 문을 사용하여 에러시에 에러문구가 나타날수있게 진행
do {
    try makeASandwich() // try 이후 조건의 함수 설정
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
// 조건을 건 함수 진행중에
// SandwichError.outOfCleanDishes 에러가 발생하면 
// washDishes() 함수가 호출됩니다. 

} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
// 위와 같이 조건을 건 함수 진행중에
// SandwichError.missingIngredients 에러가 발생시
//  buyGroceries(ingredients) 가 실행된다.
