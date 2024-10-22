# 🎬 망곰무비
"트렌드한 미디어 콘텐츠들을 탐색하고, 원하는 리스트로 추가해 관리해 보세요!"
<br>

## 📱 **주요 기능**
| HOME | SEARCH | FAVORITE |
|---------------|---------------|---------------|
| <img src="https://github.com/user-attachments/assets/8b1e1c40-7e3a-4178-b7f3-02efc7cb7cc9" width="200" /> | <img src="https://github.com/user-attachments/assets/852c924a-32f4-4577-a6cd-6909360f86a3" width="200" /> | <img src="https://github.com/user-attachments/assets/6594a960-f6f6-43b2-be28-22897dfa249e" width="200" /> |

> 🔥 지금 뜨는 영화/TV 시리즈 추천
    
> 🔍 영화 검색
    
> 👀 콘텐츠 상세 정보 확인
    
> 🎞️ 비슷한 콘텐츠 조회
    
> 💖 콘텐츠 찜하기
  
<br>


## 💻 개발 환경
<p align="left">
<img src ="https://img.shields.io/badge/Swift-5.10-ff69b4">
<img src ="https://img.shields.io/badge/Xcode-15.4-blue">
<img src ="https://img.shields.io/badge/iOS-15.0+-orange">
<br>
    
- **기간**: 2024.10.08 ~ 2024.10.13 (**약 1주**)
- **인원**: iOS 3명

    
<br> 

## 🔧 아키텍처 및 기술 스택

- `UIKit` / `RxSwift`
- `MVVM` + `Clean-Architecture` 
- `Moya` + `Router Pattern`
- `Realm` 
- `SnapKit`
- `XCTest`
    
<br>    


## 🏗️ 설계 고려 사항
### > 🧪 Testable Code
Testable한 코드를 위해 의존성 이슈를 보완하고자 **클린 아키텍처** 채택
> Protocol, DI를 통해 DIP를 따르도록 구현
    
- 사용자의 UI 경험 향상을 위한 테스팅 진행 => **Code Coverage 60%** 달성
    
    <img width="800" alt="Testing" src="https://github.com/user-attachments/assets/b618d9e1-a500-4ba1-b80d-ffb36ecb6fbd"> 
    
---
### > 👩🏻‍🔬 **Domain** Layer

📂 **`Entities`**
> View에 따라 필요한 데이터가 상이함
> ❗️통합 Entity 모델을 사용할 경우, 각 View에 요구되지 않는 API들까지 매번 호출하게 되는 문제 인식
- 불필요한 메모리&리소스 낭비 및 성능 저하를 발생시키지 않기 위한 **적절한 Entity 분리 기준**에 대해 고려하게 되었습니다
- View마다 필요한 API 종류의 정도를 따져 본 결과
간소화한 Compact 모델과, 보다 많은 속성을 지닌 Detail 모델 두 가지로 분리할 수 있었습니다
- Presentation Layer에 더욱 적절한 Entity 모델을 제공해 줌으로써, **Overfetching 문제를 방지**하였습니다 
<br>

📂 **`UseCases`**
> 기능 단위로 UseCase를 나눠 보았을 때 
❗️적절한 여러 카테고리로 분류되지 않아, 너무 자잘하거나 비대해지게 되는 문제 인식
> 서로 다른 종류의 매우 자잘한 기능들로 이루어져 있어 모두 분리하기도, 묶기도 곤란하게 됨
- Presenter에게 자잘하게 많은 UseCase를 사용하도록 설계한다면, 본래 UseCase의 존재 의미가 흐려질 것이라 판단했습니다
- 여러 UseCase를 Presenter가 하나하나 조합해 처리하게 되어 계층 간의 책임이 모호해지는 것과, 
하나의 ViewModel이 많은 UseCase에 의존하게 되는 것을 개선하고자 **UseCase 단위**에 대해 고려하게 되었습니다
- 다양한 기준의 Trade-off를 따져 본 결과,
View를 기준으로 두어 **하나의 ViewModel이 하나의 UseCase를 가지도록** 분리하였습니다
- 각 ViewModel과 UseCase의 책임을 명확하게 해 줌으로써 **복잡도를 낮추고**, 관심사를 집중시켜 **응집도를 높였습니다**
<br>
    
📂 **`Repository Interfaces`** 
- 각 UseCase에서 필요한 데이터에 따라 Repository를 유연하게 조합할 수 있도록, 각 **API를 고려**하여 분리했습니다
- 필요한 기능만을 가진 각각의 Repository를 다양한 UseCase에서 선택해 사용함으로써, **Repository의 재사용성**을 높였습니다
    
<br>    

## 🚧 기타 해결 사항
### > ♻️ RxSwift 타입 리팩토링
기존 **`BehaviorRelay` 타입** 사용 시, 초깃값 설정 init 구문 필요
```swift
init() {
    self.type = .movie
    self.id = 0
    self.imagePath = ""
    self.genre = [""]
    self.title = ""   
}
```
-> **`ReplayRelay` 타입**으로 리팩토링 진행 => 불필요한 **초깃값 설정 코드 제거**

---
### > 💥 CONFLICT
<img width="200" alt="Conflict" src="https://github.com/user-attachments/assets/5f9bf683-b6e5-4156-aad0-95c1383f6dfa">  
    
프로젝트 자체가 열리지 않는 파일 충돌 발생
-> **`.pbxproj` 파일**을 통해 충돌 부분 수정하여 해결
    
<br> 
