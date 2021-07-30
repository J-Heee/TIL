# Swift

## 2021.07.30

### 옵셔널(Optional)
- 옵셔널(Optional): Swift의 가장 큰 특징 중 하나
  - 직역하면 '선택적인'이라는 뜻
  - 값이 있을 수도 있고 없을 수도 있는 것을 나타냄
- **`nil` : 값이 없는 경우를 나타낼 때 사용**
  - 예시) 문자열
    - 값이 있는 경우 -> "가나다"
    - 빈 값(값이 있는 문자열) -> ""
    - 값이 없는 문자열 -> nil 
  - 예시) 정수
    - 값이 있는 경우 -> 123
    - 0은 0이라는 숫자 '값'
    - 값이 없는 정수 -> nil
  - 예시) 배열, 딕셔너리
    - 빈 배열, 빈 딕셔너리는 '값이 없는'것이 아니라, '비어 있는 것'
    - '없는 값' -> nil
- 모든 변수에 nil을 넣을 수 있는 것은 아님
  - String 타입 변수 name에 nil을 넣으려 하면 에러 발생
  ```swift
  var name: String = "Minion"
  name = nil // 컴파일 에러! Nil cannot be assigned to type 'String'
  ```
- **값이 있을 수도 있고 없을 수도 있는 변수를 정의할 때는, 타입 어노테이션에 `?`를 붙여야 함**
  - -> 이렇게 정의한 변수를 옵셔널(Optional)이라고 함
  ```swift
  var name2: String?
  name2 = "Minion Bob"
  print(name2) // Optional("Minion Bob")
  name2 = nil
  let name3: String? = "kim"
  ```
- 옵셔널로 정의한 변수는 옵셔널이 아닌 변수와 다름
  - 아래와 같은 코드는 사용 불가능
  ```swift
  let optionalEmail: String? = "devabc@gmail.com"
  let requiredEmail: String = optionalEmail // 컴파일 에러! Value of optional type 'String?' not unwrapped; did you mean to use '!' or '?'?
  ```
  - requiredEmail 변수는 옵셔널이 아닌 String 타입이기 때문에, 항상 값을 가지고 있어야 함
  - optionalEmail 변수는 옵셔널로 선언된 변수이기 때문에, 실제 코드가 실행되기 전까지는 값 존재 유무를 알 수 없음
  - 따라서 Swift 컴파일러는 안전을 위해 requiredEmail에는 옵셔널로 선언된 변수를 대입할 수 없게 함
- 옵셔널은 개념적으로 표현해보기
  - 어떤 값 또는 nil을 가지고 있는 것
  ```
    ,-- 어떤 값 (String, Int, ...)
  Optional
    `-- nil
  ```


<br>

### 옵셔널 바인딩(Optional Binding)
- 옵셔널 바인딩(Optional Binding) : 옵셔널의 값을 가져오고 싶은 경우 사용하는 것
  - 옵셔널의 값이 존재하는지 검사한 후, 존재한다면 그 값을 다른 변수에 대입시켜줌 
- **`if let` 또는 `if var` 사용**
  - 옵셔널의 값을 벗겨서 값이 있다면 if문 안으로 들어가고, 값이 nil이라면 그냥 통과하게 됨
  - 예시) 아래의 코드에서 optionalEmail에 값이 존재한다면 email이라는 변수 안에 실제 값이 저장되고, if문 내에서 그 값 사용 가능
    - 만약 optionalEmail이 nil이라면 if문이 실행되지 않고 넘어감
  ```swift
  if let email = optionalEmail {
    print(email) // optionalEmail의 값이 존재한다면 해당 값이 출력
  }
  // optionalEmail의 값이 존재하지 않는다면 if문을 그냥 지나침
  ```
- 하나의 if문에서 콤마(,)로 구분하여 여러 옵셔널 바인딩 가능
  - 사용된 모든 옵셔널의 값이 존재해야 if문 안으로 진입 
  ```swift
  var optionalName: String? = "Minion Bob" 
  var optionalEmail: String? = "devabc@gmail.com"

  if let name = optionalName, let email = optionalEmail {
    // name과 email 값이 존재
  }
  ```
  - Tip) 코드가 너무 길 경우에는, 여러 줄에 걸쳐서 사용하는 것 권장
  ```swift
  if let name = optionalName,
    let email = optionalEmail {
      // name과 email 값이 존재
  }
  ```
  - 위와 동일한 코드
  ```swift
  if let name = optionalName {
    if let email = optionalEmail {
      // name과 email 값이 존재
    }
  }
  ```
  - 한 번의 if문에서 여러 옵셔널을 바인딩할 수 있게 된 것은 Swift 1.2 버전부터
  - 이전 버전까지는 위의 코드처럼 여러 번으로 감싸진 옵셔널 바인딩을 사용
- 옵셔널을 바인딩할 때 `,`를 사용해서 조건도 함께 지정 가능
  - `,` 이후의 조건절은 옵셔널 바인딩이 일어난 후에 실행됨
  - 즉, 옵셔널이 벗겨진 값을 가지고 조건을 검사하게 되는 것
  ```swift
  var optionalAge: Int? = 22

  if let age = optionalAge, age >= 20 {
    // age의 값이 존재하고, 20 이상
  }
  ```
  - 위와 동일한 코드
  ```swift
  if let age = optionalAge {
    if age >= 20 {
      // age의 값이 존재하고, 20 이상
    }
  }
  ```
- **옵셔널 바인딩은 `if let` 대신 `guard let`을 사용하기도 함** 
  - `if let`은 옵셔널이 nil이 아니면 바디가 실행되지만, `guard let`은 옵셔널이 nil일 때 else {...}의 바디가 실행됨
  ```swift
  func greet(_ name: String?) {
    guard let unwrapped = name else {
      print("You didn't provide a name!")
      return
    }
    print("Hello, \(unwrapped)!")
  }
  ```
  - guard 문장에서 옵셔널 파라미터 name이 nil이면 else {...}가 실행
  - if let과 또 다른 점은 바인딩된 unwrapped가 guard 문장 이후에도 또다시 바인딩 할 필요 없이, 벗겨진 채로 함수 블록에서 사용 가능하다는 것
  - guard let은 주로 함수의 초기에 사용하는데, 파라미터를 먼저 조사해서 조건에 맞지 않으면 바로 함수를 종료해서 걸러내고, 조건에 맞으면 더 이상 조건을 신경 쓸 필요 없이 필요한 로직을 수행하고자 할 때 편리함