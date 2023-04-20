## 문자열 과문자(Tom)
# 4.10 문자열
# 스터디 Strings & Characters

- 텍스트를 저장하고 다룹니다
- 문자열 리터럴은 쌍따옴표 (")로 둘러싸인 문자의 연속입니다.
var a: String = "asdas"
var aa: Character = "s"

var b: [String] = ["abcdefg"]
var bb: [Character] = ["a", "b", "c", "d", "e", "f", "g"]

var d = String(bb) ->Character 에서는 String으로 가능
//"abcdefg"
var dd = Character(b) -> String 에서는 불가능 
//에러 
Character 합쳐진것이 String이다.
Character 값은 반드시 하나의 문자만 포함해야 하므로 Character 변수에 추가로 String 또는 Character 를 추가할 수 없습니다.


### 여러줄 문자열 리터럴
여러줄의 문자열이 필요하면 3개의 쌍따옴표로 둘러싸인 일련의 문자들을 여러줄 문자열 리터럴로 사용하면 됩니다.

var c = """
월요일
화요일
수요일
목요일
금토일
"""

### 특수 문자
- "\u{} {}안에 숫자를 넣어 유니코드를 나타낼수있습니다."
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
let a1 = "\u{3422}" // "㐢" 


#""" 으로 시작과 끝을 정할수있다. 중간 부분 """ 있어도 해당되지않음.
let threeMoreDoubleQuotationMarks = #"""
Here are three more double quotes: """
"""#



- 문자열도 기존 문자열에 문자를 추가 할수있다.
- 대신 변수 선언에서만 가능 상수에서는 불가능하다.
var variableString = "Horse"
variableString += " and carriage"

var constantString = "Highlander"  //let -> var 변경
constantString += " and another Highlander"

let str1 = "안녕"
let str2 = "하세요"
var str = str1 + str2   //안녕하세요
let character1 = "!"   
str.append(character1)   // 안녕하세요! 1글자라도 append가능하다.


let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5"
 - \() string값안에 다른타입을 넣는 경우 사용하게 된다.
 - multiplier를 더블값으로 바꾸어 * 2.5 를 진행한다.
 - 기존 3이면 *2.5 가 안되기에 Double타입으로 변경이후 진행

## 순서
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u 
// 왜 u가 나타나냐면 (after: greeting.startIndex) after 메소드에 의해서 스타트인덱스 다음인덱스는 나타내기때문에.


## 문자 삽입과 삭제
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"
//welcome.index(before: welcome.endIndex)는 
위 값에 마지막 "!" 있기에 "!" 이전에 추가한다
그렇기에 hello! -> !앞에 there 를 추가해서
hello there! 가 나타난다.

welcome.insert(contentsOf: "tom", at: welcome.index(before: welcome.endIndex))
// hello there!tom

한번 추가한 문자는 지속된다. 

welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there"
"!" 이부분이 삭제된다.

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome now equals "hello"
"hello there" 여기서 끝부분 부터 6자리를 지운다
<welcome.endIndex 코드는 welcome 문자열에서 끝에서부터 앞쪽으로 6개의 인덱스를 삭제 진행한다. "hello" 만 나타난다.


let greeting1 = "Hello, world!"
let index1 = greeting1.firstIndex(of: ",") ?? greeting1.endIndex
// "," 처음으로 나타나는 인덱스 "," 가 없으면 끝에 인덱스로 나타낸다.
let beginning = greeting1[..<index1]
// "," 를 기준으로 , 이전 문자열을 추출한다.
// beginning is "Hello"

// Convert the result to a String for long-term storage.
let newString = String(beginning)
// "," 가없다면 그냥 "Hello, world!" 출력된다.
index1 조건으로 엔드 이전껄 추출하기때문에




let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]

var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 2 ") {
        act1SceneCount += 1
    }
}
print("There are \(act1SceneCount) scenes in Act 1")
// Prints "There are 5 scenes in Act 1"


let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]


var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        act1SceneCount += 1
    }
}
print("There are \(act1SceneCount) scenes in Act 1")
// Prints "There are 5 scenes in Act 1"


var mansionCount = 0
var cellCount = 0
for scene in romeoAndJuliet {
    if scene.hasSuffix("Capulet's mansion") {
        mansionCount += 1
    } else if scene.hasSuffix("Friar Lawrence's cell") {
        cellCount += 1
    }
}
print("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
// Prints "6 mansion scenes; 2 cell scenes"
