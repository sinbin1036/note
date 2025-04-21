## Swift iOS 앱 개발 정리본 (03~05장)

---

### ✅ 기본 UI 컴포넌트 개념 정리

#### 📌 UIImageView

- 역할: 이미지를 보여주는 뷰
    
- 주요 메서드/속성: `.image`, `UIImage(named:)`
    
- 주의사항: 아웃렛 변수 연결 후 사용 / 뷰 모드 설정(Aspect Fit 등)
    

#### 📌 UIDatePicker

- 역할: 날짜 및 시간 선택 위젯
    
- 주요 메서드: `.date`, `addTarget()` 또는 `@IBAction`
    
- 포맷 지정: `DateFormatter()` 사용하여 출력 형식 지정
    

#### 📌 UIPickerView

- 역할: 여러 항목 중 선택할 수 있는 휠 형태의 뷰
    
- 필수 프로토콜: `UIPickerViewDataSource`, `UIPickerViewDelegate`
    
- 주요 메서드: `numberOfComponents`, `numberOfRowsInComponent`, `titleForRow`, `didSelectRow`
    
- 커스텀 출력: `viewForRow()` 이용 가능 (이미지 출력 등)
    

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