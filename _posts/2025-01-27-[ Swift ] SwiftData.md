---
title: "[Swift] SwiftData"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    swiftData,
    json,
    dataBase
  ] 
image: "/assets/img/title/swift2.png"
---

# SwiftData
* SwiftData는 애플이 제공하는 로컬 데이터 관리 프레임워크
* 내부적으로 SQLite 기반으로 동작하며, 데이터를 관계형 데이터베이스처럼 관리
* SwiftUI와 통합되어 자동 UI 갱신이 가능
* 데이터를 저장하고 검색하며, 앱 내에서 데이터 추가/수정/삭제 작업을 쉽게 처리 가능

> JSON과 SwiftData를 함께 사용하는 이유
* JSON의 역할
    * 초기 데이터 로드.
    * 서버와의 데이터 교환(API 통신).
    * 앱 외부 데이터를 처리하거나 저장.
* SwiftData의 역할
    * 앱 내 로컬 데이터 저장.
    * 실시간 데이터 검색 및 관리.
    * SwiftUI와 통합하여 UI와 데이터의 상태 동기화.

> 언제 SwiftData를 사용하는가
* 앱에서 데이터를 추가, 수정, 삭제해야 하는 경우.
* 관계형 데이터를 효율적으로 관리하려는 경우(예: 가수와 스크립트 간 관계).
* 네트워크 연결 없이 오프라인 모드에서도 데이터를 관리해야 하는 경우.
* *I와 데이터 상태 동기화가 중요한 경우.
> JSON만으로 충분한 경우
* 데이터가 변경되지 않고, 읽기 전용으로 사용되는 경우.
* 서버에서 데이터를 받아와 즉시 UI에 표시하는 경우.

# SwiftData와 Json을 사용한 데이터처리 흐름
1. 서버에서 Json 데이터 가져오기
    * 서버에서 Json 데이터를 받아와 Swift에서 디코딩
    * 네트워크 요청은 `URLSession`을 사용
    ```swift
    let url = URL(string: "https://example.com/api/scripts")!
    URLSession.shared.dataTask(with: url) { data, response, error in
        guard let data = data else { return }
        do {
            let scriptsFromServer = try JSONDecoder().decode([Script].self, from: data)
            // 데이터를 SwiftData에 저장
        } catch {
            print("JSON 디코딩 실패: \(error)")
        }
    }.resume()
    ```

2. SwiftData로 데이터 저장
    * JSON 데이터를 디코딩한 후, SwiftData 모델 객체로 변환하여 저장
    * `modelContext.insert()`를 통해 데이터를 SwiftData에 저장
    ```swift
    let newScript = Script(
    title: "Test Video",
    script_KOR: "안녕하세요",
    script_JPN: "こんにちは",
    youtube_url: "https://youtube.com/example",
    artist: "BTS"
    )
    modelContext.insert(newScript)
    ```

3. SwiftData에서 데이터 읽기
    * `@Query`를 사용하여 데이터를 필터링 하거나 정렬하며 가져옴
    ```swift
    @Query(filter: #Predicate { $0.artist == "BTS" }) var scripts: [Script]
    ```
4. 데이터 업데이트
    * SwiftData 데이터를 변경하면 UI가 자동으로 갱신 됨


<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/68FC0D9D-FA38-49E3-807D-586E579DED7A_1_105_c.jpeg" width="800" />
</div>

# JSON에서 SwiftData로 변환 흐름

> ### JSON
```json
{
    "title": "Test Video",
    "artist": "BTS",
    "script_KOR": "[0:00] 안녕하세요\n[0:05] 오늘은 날씨가 좋네요",
    "script_JPN": "[0:00] こんにちは\n[0:05] 今日は天気がいいですね",
    "youtube_url": "https://youtube.com/watch?v=test123"
}
```
> ### SwiftData

| ID  | Title            | Artist      | Script_KOR                | Script_JPN                | YouTube URL                         |
| --- | ---------------- | ----------- | ------------------------- | ------------------------- | ----------------------------------- |
| 1   | Test Video 1     | BTS         | [0:00] 안녕하세요...       | [0:00] こんにちは...       | https://youtube.com/watch?v=test123 |
| 2   | Another Video    | BLACKPINK   | [0:00] 반갑습니다...       | [0:00] はじめまして...       | https://youtube.com/watch?v=test456 |

> ### 데이터 저장 흐름
```plaintext
서버 --------(JSON 데이터)--------------> 앱
  ↑                                    ↓
  SwiftData 저장소 <----(변환)---- JSON 디코딩
```