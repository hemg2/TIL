# 파싱 진행

- 기본적으로 에셋 파일에 있는 데이터 파싱 을 진행할때
```swift
func test() {
                에셋 파일에 접근
        guard let asset = NSDataAsset.init(name: "exposition_universelle_1900") else { return }
         파싱 확인 진행
        guard let json = String(data: asset.data, encoding: .utf8) else { return }
        print(json)
        
        let decoder = JSONDecoder()
        
        do {              여기서 모델을 파싱하여 레이블에 넣어준다.
            let a = try decoder.decode(Exposition.self, from: asset.data)
            titleLabel.text = a.title
            visitorLabel.text = "방문객 : \(a.visitors) 명"
            locationLabel.text = "개최지 : \(a.location)"
            openPeriodLabel.text = "개최 기간 : \(a.duration)"
            descriptionLabel.text = a.description
        } catch {
            print(error)  파싱이안될시 에러 처리
        }
    }
```


지금 진행중인 테이블뷰의 데이터 파싱 진행중

```swift  
 func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        guard let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as? ItemListTableViewCell else { return UITableViewCell() }
        
        if let asset = NSDataAsset(name: "items") {
            let contentData = asset.data
            let json = JSONDecoder()
            
//            let json11 = String(data: asset.data, encoding: .utf8)
//            print(json11!)
            
            
            do {
                let itemInfo: Item = try json.decode(Item.self, from: contentData)

                cell.setModel(model: itemInfo)
                //                cell.titleLabel.text = itemInfo.name
                //                cell.descriptionLabel.text = itemInfo.shortDescription
                //                cell.mainImageView.image = UIImage(named: itemInfo.imageName)
            } catch {
                print("에러\(error)")
            }
        }
        
        //        let model = mainItem[indexPath.row]
        //        cell.setModel(model: model)
        
        return cell
    }
```
