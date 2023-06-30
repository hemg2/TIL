# lldb

### 함수 이름 이용해서 함수 브레이크 걸기
- breakpoint set --name viewDidLoad
- b -n viewDidLoad    이렇게 줄일수있다.
- 브레이크는 그 위에 걸고 실행하면된다

### 파일 이름과 line번호 로 브레이크 걸기
- br s --file ViewController.swift -- line 20 -> 뷰컨파일 20번째 줄 브레이크
- br s -f ViewController.swift -l 20  줄임말


### condtion
 – contidion (-c) option을 이용하면, breakpoint에 원하는 조건을 걸 수도 있습니다. -c option 뒤의 expression이 true인 경우에만 breakpoint에서 멈춥니다.
- viewWillAppear 호출시, animated가 true인 경우에만 break
- breakpoint set --name "viewWillAppear" --condition animated
- br s -n "viewWillAppear" -c animated



- `expression` Command를 이용해서 변수를 직접 선언해서 사용할 수도 있습니다. 단, 사용하고자 하는 변수명 앞에 $ 문자를 붙여줘야 합니다.
- expr let $someNumber = 10 이런식으로 생성가능

- expr var $view = UIView(frame: CGRect(x:100, y:100, width: 80, height:80))
- expressionn
- 1-> $view.backgroundColor = UIColor.blue
- 2-> self.view.addSubview(view)
이렇게하면 없었지만 뷰를 만들고 컬러 주고 에드서브뷰로 추가해서 뷰가 생긴것을 확인할수있다.
브레이크 포인트는 뷰디드로드의 슈퍼뷰디드로드부분
이런식으로 다른 부분도 넣어서 체크확인을 진행할수있다.



