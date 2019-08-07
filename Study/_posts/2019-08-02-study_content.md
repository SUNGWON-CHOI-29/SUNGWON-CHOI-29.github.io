---
layout: post
title: 부스트코스 - Swift&iOS - 3주차
description: >
  커넥트 재단의 Swift와 iOS 강의, 그리고 현업 선배님들의 리뷰를 통해 배우게 된 것을 정리하기 위한 포스팅 입니다.
author: author

---

Swift&iOS 강의 3주차 학습 내용 리뷰

\#부스트코스 \#iOS프로그래밍

## 학습목표
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_3.png"/>
</center>
## TableView
테이블 뷰는 정보를 리스트 형태로 보여줄 수 있는 레이아웃으로써 많은 앱에서 활용되는 사용자 인터페이스 입니다. 해당 강의를 통해 테이블 뷰의 기본적인 구성과 형태에 대해 알 수 있었습니다. 테이블 뷰는 하나의 열과 다수의 행으로 구성되며 <b>Cell</b> 하나가 하나의 <b>행</b>에 해당합니다.
<center>
<img src="https://cphinf.pstatic.net/mooc/20180120_75/1516452980003BId4E_PNG/123_2.png"/>
</center>
기본 스타일의 테이블 뷰
{:.figure}

<center>
<img src="https://cphinf.pstatic.net/mooc/20180120_207/1516452998158XgYpC_PNG/123_3.png"/>
</center>
섹션을 그룹으로 구분 짓는 테이블
{:.figure}

<center>
<img src="https://cphinf.pstatic.net/mooc/20180208_290/1518017999963lFHYL_PNG/123_1.png"/>
</center>
테이블 뷰의 헤더와 푸터, 섹션의 영역
{:.figure}

## TableViewDataSource
뷰 컨트롤러에서 테이블 뷰의 셀에 데이터를 넣어주기 위해서는 TableViewDataSource 델리게이트를 사용해야 합니다. 해당 델리게이트를 준수하기 위해서는 다음과 같은 2개의 메소드를 구현해야 합니다.

```
//테이블 뷰의 열의 갯수를 리턴
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return row.count
}

//하나의 셀을 생성하여 반환하는 메소드
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        guard let cell: UITableViewCell = tableView.dequeueReusableCell(withIdentifier: self.cellIdentifier, for: indexPath)
        //indexPath를 이용하여 몇 번째 열의 셀인지 확인할 수 있음
        return cell
    }
```
Android의 리사이클러뷰에 데이터를 넣어주기 위한 어댑터의 역할을 iOS에서는 데이터소스가 수행하는 것 같았습니다.

## CustomTableViewCell
Xcode에서 제공하는 기본적인 스타일의 셀이 아닌 커스텀 셀을 만들기 위해서는 커스텀 셀을 위해 클래스를 만들어야 합니다. 해당 클래스에서 셀에서 사용할 IBOutlet과 같은 UI 요소들과 변수들을 선언해놓으면 해당 테이블 뷰를 가지고 있는 뷰 컨트롤러에서 셀을 생성하고 데이터를 넣어줄 때 커스텀 셀의 정보를 사용할 수 있습니다.

## 뷰의 재사용
테이블을 구성하는 셀이 매우 많을 경우 화면에 표시되는 셀의 갯수를 생각하면 모든 셀에 메모리를 할당하는 것은 무척이나 비효율적인 메모리 사용일 것입니다. 따라서 화면에 표시되지 않는 셀은 회수하여 다음 셀을 만들 때 재활용 됩니다. 이것을 위해 사용되는 메소드는 다음과 같습니다.

```
tableView.dequeueReusableCell(withIdentifier: self.cellIdentifier, for: indexPath)
```

## 스토리보드 세그
해당 강의에서는 뷰 컨트롤러간 이동을 할 때 데이터를 전달해주는 방법에 대해 알 수 있었습니다. <b>segue.destination</b>을 사용하여 원하는 뷰컨트롤러로 이동하는 세그 액션인지 확인할 수 있으며 <b>sender를 as로 캐스팅</b>하여 해당 뷰 컨트롤러의 데이터를 접근할 수 있습니다.

## JSON Decode
해당 강의에서는 Json파일을 디코딩하여 배열의 형태로 가지고 있다가 cell에 하나씩 넣어주는 것을 배웠습니다. Json으로 디코딩 될 구조체는 <b>Codable</b> 프로토콜을 준수해야 합니다.

## 과제 중점사항
과제를 수행하는데 있어서 코드 리팩토링을 고려한 두가지 사항입니다.
### 1. 구조체의 타입 메소드와 프로퍼티 활용
Json 디코딩이 필요한 뷰 컨트롤러에서 중복되는 코드를 줄이기 위해 Json 디코딩 정보를 가질 콜렉션 변수들을 타입 프로퍼티로 가지는 구조체를 선언했습니다. 데이터 로드 부분을 해당 구조체의 타입 메소드로 구현했습니다.

```
struct JsonDecoder {
    static var nations: [Nation] = []
    static var cities: [City] = []

    static func nationCount() -> Int {
        return nations.count
    }
    static func cityCount() -> Int {
        return cities.count
    }

    static func loadData(assetName: String, type: String, tableView: UITableView) {
        let jsonDecoder: JSONDecoder = JSONDecoder()
        guard let dataAsset: NSDataAsset = NSDataAsset(name: assetName) else{
            return
        }
        do {
            if type == "City" {
                self.cities = try jsonDecoder.decode([City].self, from: dataAsset.data)
            } else {
                self.nations = try jsonDecoder.decode([Nation].self, from: dataAsset.data)
            }
        } catch {
            print(error.localizedDescription)
        }
        tableView.reloadData()
    }
}
```
### 2. 커스텀 셀을 생성할 때 as! 처리
커스텀 셀을 생성할 때 as 캐스팅이 실패하면 기본적인 테이블 뷰의 셀을 리턴하도록 하였습니다.
```
guard let cell: CityTableViewCell = tableView.dequeueReusableCell(withIdentifier: self.cellIdentifier, for: indexPath) as? CityTableViewCell else {
            return tableView.dequeueReusableCell(withIdentifier: self.cellIdentifier, for: indexPath)
        }
```
## 리뷰 결과
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult3_1.png"/>
</center>
## Summary
* 테이블뷰의 기본 구성과 셀에 대해서 알 수 있었으며 셀을 커스텀하여 원하는 테이블 뷰를 만들 수 있게 되었습니다.
* 스토리보드 세그를 통해 뷰 컨트롤러간 데이터를 주고 받는 법에 대해서 알 수 있었습니다.
* JSON파일을 디코딩 하여 Xcode에서 사용하는 법을 알 수 있었습니다.
* 구조체의 타입 메소드, 타입 프로퍼티를 활용하여 중복되는 코드를 줄일 수 있었습니다.
* <b>코드 줄이는데 집중하여 MVP 디자인 패턴을 위반하는 일이 있었음, 다음 프로젝트 때는 더욱 주의해야겠습니다.
* 일부 네이밍이 적절치 않은 항목과 코드 블록의 규칙이 지켜지지 않은 곳이 있었습니다. 더욱 꼼꼼히 코드를 확인해야 겠습니다.</b>
