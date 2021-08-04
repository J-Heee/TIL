# Swift

## 2021.08.04

### 옵셔널 체이닝(Optional Chaining)
- Swift 코드를 간결하게 만들어주는 요소 중 하나
- 코드를 보면서 이해하는 것이 좋음
  - 예시) 옵셔널로 선언된 어떤 배열이 '빈 배열'인지 검사하려면? -> nil이 아니면서 빈 배열인지를 확인해보면 될 것
  ```swift
  let array: [String]? = []
  var isEmptyArray = false
  
  if let array = array, array.isEmpty {
    isEmptyArray = true
  } else {
    isEmptyArray = false
  }

  isEmptyArray
  ```
- 옵셔널 체이닝을 사용하면 동일한 코드를 더 간결하게 작성 가능
  ```swift
  let isEmptyArray = array?.isEmpty == true
  ```
- **옵셔널 체이닝은 옵셔널의 속성에 접근할 때, 옵셔널 바인딩 과정을 `?` 키워드로 줄여주는 역할을 함**
  - 아래의 3가지 경우의 수 생각 가능
  - array가 nil인 경우
    ```swift
    array?.isEmpty 
    ~~~~~
    여기까지 실행되고 `nil` 반환
    ```
  - array가 빈 배열인 경우
    ```swift
    array?.isEmpty 
    ~~~~~~~~~~~~~~ 
    여기까지 실행되고 `true` 반환 
    ```
  - array에 요소가 있는 경우
    ```swift
    array?.isEmpty 
    ~~~~~~~~~~~~~~ 
    여기까지 실행되고 `false` 반환 
    ```
  - `array?.isEmpty`의 결과로 나올 수 있는 값은 nil, true, false
  - 원래 `isEmpty`의 반환값은 `Bool`인데, 옵셔널 체이닝으로 인해 `Bool?`을 반환하도록 바뀐 것
  - 따라서, 값이 실제로 true인지를 확인하려면, `== true`를 해주어야 함

<br>

### 옵셔널 벗기기
- **옵셔널에 값이 있다고 가정하고, 값에 바로 접근할 수 있도록 도와주는 키워드 `!`를 붙여서 사용하는 것**
  - 옵셔널을 사용할 때마다 옵셔널 바인딩을 하는 것이 가장 바람직
  - But, 개발을 하다 보면 분명히 값이 존재할 것임에도 불구하고 옵셔널로 사용해야 하는 경우가 종종 발생, 그럴 때 사용함
  ```swift
  print(optionalEmail)  // Optional("devabc@gmail.com")
  print(optionalEmail!) // devabc@gmail.com
  ```
- 주의할 점) 옵셔널의 값이 nil인 경우에 사용할 경우, 런타임 에러 발생
  ```swift
  var optionalEmail: String? = nil
  let str = "i am " + optionalEmail!
  // fatal error: unexpectedly found nil while unwrapping an Optional value
  ```
  - 런타임 에러가 발생하면 iOS 앱은 강제 종료
  - Java의 NullPointerException과 비슷하다고 생각 가능

<br>

### 암묵적으로 벗겨진 옵셔널(Implicitly Unwrapped Optional)
- **옵셔널을 정의할 때 `?` 대신 `!`를** 붙이면 Implicitly Unwrapped Optional(암묵적으로 벗겨진 옵셔널)로 정의됨
  ```swift
  var email: String! = "devabc@gmail.com"
  print(email)  // devabc@gmail.com
  let str = "i am " + email
  ```
- 이렇게 정의된 옵셔널은 nil을 포함할 수 있는 옵셔널이긴 한데, 접근할 때 옵셔널 바인딩이나 옵셔널을 벗기는 과정을 거치지 않고도 바로 값에 접근할 수 있다는 점에서 일반적인 옵셔널과 차이점을 가짐
- 옵셔널 벗기기와 마찬가지로, 값이 없는데 접근을 시도하면 런타임 에러 발생
  ```swift
  var email: String! = nil
  print(email)  // 런타임 에러! fatal error: unexpectedly found nil while unwrapping an Optional value
  ```
- 일반적인 옵셔널을 사용해서 정의하고, 옵셔널 바인딩 또는 옵셔널 체이닝을 통해 값에 접근하는 것이 가장 바람직함