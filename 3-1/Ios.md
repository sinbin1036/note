swift 언어
변수 : 지정된 값을 변경할수 있는데이터
- var
상수 : 한번 값을 할당하면 변경 할수 없는 데이터
- let
컬렉션 타입
- 배열
```
var shoppingList: [String] = ["Eggs", "Milk"]
print(shoppingList) // 출력: ["Eggs", "Milk"]

```
- 세트
```
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"] print(favoriteGenres) // 출력: ["Rock", "Classical", "Hip hop"]
```
`.inset` : 값 추가
`.remove` : 값 제거
`.contains` : 세트 값 포함 여부 확인
- 딕셔너리
```
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
print(airports) // 출력: ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```

for문
```
let fruits = ["Apple", "Banana", "Cherry"]

for fruit in fruits {
    print(fruit)
}

```

- where 절을 활용한 조건부 반복
```
let numbers = [10, 20, 30, 40, 50]

for number in numbers where number > 30 {
    print(number)
}

```

- 인덷스와 값 순회
```
let animals = ["Dog", "Cat", "Bird"]

for (index, animal) in animals.enumerated() {
    print("\(index + 1)번째 동물은 \(animal)입니다.")
}
```

repeat-while
```
repeat {
    // 조건이 참인 동안 반복해서 실행되는 코드
} while 조건
```

함수
```
func 함수이름(매개변수이름: 매개변수타입) -> 반환타입 {
    // 함수가 수행할 작업
    return 반환값
}

//예제
func greet(person: String) -> String {
    let greeting = "Hello, \(person)!"
    return greeting
}

let greetingMessage = greet(person: "Alice")
print(greetingMessage) // 출력: Hello, Alice!
```

- 내부 매개변수와 외부 매개변수
```
func greet(person: String, from hometown: String) -> String {
    return "Hello, \(person) from \(hometown)!"
}

print(greet(person: "Diana", from: "Seoul")) // 출력: Hello, Diana from Seoul!
//외부에선 hometown이 아닌 from으로 호출시 사용됨
```

- 튜플 반환
```
func addAndMultiply(a: Int, b: Int) -> (sum: Int, product: Int) {
    let sum = a + b
    let product = a * b
    return (sum, product)
}

let result = addAndMultiply(a: 3, b: 4)
print("합은 \(result.sum)이고, 곱은 \(result.product)입니다.") // 출력: 합은 7이고, 곱은 12입니다.

```


클래스 구조체 차이점
- 클래스는 참조 타입 : 전달
- 구조체는 값 타입 : 복사

상속
- 속성 재정의 : 자식 클래스가 부모클래스의 속성를 재정의할수 있다 
	override
- 메소드 재정의 : 자식 클래스가 부모클래스의 메서드를 재정의할수 있다
- super 키워드 : 키워드는 서브 클래스에서 슈퍼 클래스의 속성과 메서드를 참조할 때

참조
- 동일성 검사 : 서로 동일한 인스턴스를 참조 하고 있는지 확인하는것
- 강한 참조 사이크 :  서로가 서로를 참조하여 메모리가 해제되지 않는 상황
- 약한 참조와 미소유 참조 : 약한 참조 weak와 미소유 참조unowned를 이용해 메모리 무한 뺑뺑이를 방지 할수 있다

스위프트 장점
- 빠르고 강력하다
- 완전한 플렛폼이다
- 현대적이다
- 상호반응적인 플레이그라운드
- 오픈소스이다
- 안전을 위한 설계가능하다

스토리보드
- 화면간의 흐름 및 전체적인 모양을 시작적인 방식으로 연결하고 표현하여 직관적으로 앱의 흐름을 확인 할수 있게 만든 기능




## Swift iOS 앱 개발 정리본 (03~05장)

---

### ✅ 기본 UI 컴포넌트 개념 정리

#### 📌 UIImageView

- 역할: 이미지를 보여주는 뷰
    
- 주요 메서드/속성: `.image`, `UIImage(named:)`
	`.image` = 이미지뷰에 보여줄 이미지를 생성할때 사용
    `UIImage(named:)` = 프로젝트에 포함된 이미지 파일을 로드한다
- 주의사항: 아웃렛 변수 연결 후 사용 / 뷰 모드 설정(Aspect Fit 등)
    

#### 📌 UIDatePicker
- picker : 아이폰에서 원하는 항목을 선택 할수 있게 해주는 객체
	
- 역할: 날짜 및 시간 선택 객체로서, 시계, 알람탑에서 자주사용되는 기능중 하나
    
- 주요 메서드: `.date`, `addTarget()` 또는 `@IBAction`
    
- 포맷 지정: `DateFormatter()` 사용하여 출력 형식 지정
    

#### 📌 UIPickerView

- 역할: 여러 항목 중 선택할 수 있는 휠 형태의 뷰
    
- 필수 프로토콜: `UIPickerViewDataSource`, `UIPickerViewDelegate`
    
- 주요 메서드: `numberOfComponents`, `numberOfRowsInComponent`, `titleForRow`, `didSelectRow`
    
- 커스텀 출력: `viewForRow()` 이용 가능 (이미지 출력 등)
    
- 델리게이트 : 어떤 객체의 행동이나 상태 변화에 대해 대신 처리하는 객체를 지정하는 프로                      그래밍 패턴

---

### ✅ 스토리보드 구성 순서

1. 새 프로젝트 생성 (Single View App)
    
2. 스토리보드에 객체 추가 (ImageView, Picker, Label, Button 등)
    
3. 아웃렛 변수 연결 → `@IBOutlet`
    
4. 액션 함수 연결 → `@IBAction`
    
5. 기능 구현 (변수 변경, 타이머, 이미지 변경 등)
    

---

### ✅ Swift 문법 / 개념 요약

#### 🔸 @IBOutlet / @IBAction

- Interface Builder와 코드 연결할 때 사용하는 특수 속성
    
- IBOutlet: UI 요소 → 변수 연결
    
- IBAction: UI 이벤트 → 함수 연결
    

#### 🔸 옵셔널

- `?`: 값이 있을 수도, 없을 수도 있음 → Optional 타입
    
- `!`: 강제 언래핑 (nil이면 앱 크래시 위험)
    
- `if let`, `guard let`: 안전한 언래핑 방법
    

#### 🔸 배열 & 데이터 연동

- `let imageNames = ["1.jpg", "2.jpg"]`
    
- PickerView나 TableView에서 배열 기반 항목 출력 가능
    

#### 🔸 DateFormatter

- 날짜 포맷 지정
    

```swift
let formatter = DateFormatter()
formatter.dateFormat = "yyyy-MM-dd HH:mm:ss"
```

#### 🔸 Timer 사용 예시

```swift
Timer.scheduledTimer(timeInterval: 1, target: self, selector: #selector(timerAction), userInfo: nil, repeats: true)
```

---

### ✅ 마무리 체크리스트

---

💡 위 내용을 기준으로 직접 코드 예제와 실습 화면을 정리하면 완성형 정리본이 됨. 필요시 챕터별 코드 블록과 스크린샷도 첨부 가능.
