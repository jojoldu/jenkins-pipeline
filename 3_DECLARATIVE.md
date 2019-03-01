# 3. Declarative 문법

Declarative 문법은 Jenkins에서 **전통적으로 수행 하던 방식과 유사**합니다.  
이렇게 설명드리면 좀 애매하실텐데요.  
최대한 젠킨스 **웹 페이지의 기능 혹은 설정과 유사한 형태를 문법으로 옮겨놓은 것**이라고 생각하시면 될 것 같습니다.  
  
구조화되어있어, UI로 전환하기가 쉬운데요.  
그래서 [젠킨스의 블루오션](https://novemberde.github.io/devops/2017/10/21/Jenkins.html) 등도 이 문법으로 작성됩니다.  

## 3-1. 장점과 단점

Declarative 문법의 장점과 단점은 다음과 같습니다.

### 장점

* 잘 정의되고, 강제화된 구조를 가짐
  * 젠킨스의 웹 페이지에 있는 양식과 같다고 보시면 됩니다.
* 가독성이 좋습니다
  * 아무래도 구조적으로 잘 잡혀 있어, 읽기 쉽습니다.
* 논리적인 내용을 정의하기 보다는 좀 더 상위의 개념적인 접근에 어울립니다.
* Blue Ocean을 통해 생성 가능
* 예전부터 있던 젠킨스의 개념들 (알람 등)에 매핑되는 문법이 존재
* 더 나은 문법 검사 및 오류 식별
* 파이프라인 간의 일관성 증가

### 단점

* 반복 로직에 대한 지원이 적습니다
  * Scripted에서 ```for```를 사용하는 것과 달리 Declarative는 지원이 약합니다.
* try ~ catch 등의 지원 약함
* 아직도 발전하고 있습니다 (전통적인 젠킨스의 기능이 100% 다 구현된게 아니라는 말)
* 너무 견고한 구조 
  * 사용자가 파이프라인 코드를 다루기가 어려움
* 현재 기준으로 더 복잡한 파이프 라인이나 워크 플로우에는 적합하지 않습니다.


## 3-2. 문법

Declarative 문법에는 별도의 기능을 지원하는 Directive (지시어 정도로 이해해주세요.)가 있습니다.  
이런 Directive를 이용해 필요한 파이프라인 작업들을 작성합니다.  
아래는 대표적인 Directive들 입니다.

| Directive   |  설명   |
|  ---  |  ---  |
|  ```pipeline```     |    |
|  ```stages```     |      |
|  ```stage```     |       |
|   ```steps```    |     |
|  ```post```     |   |
|  ```when```     |  |

> 위의 Directive는 Declarative 전용입니다.  
즉, **Scripted 문법에서는 사용할 수 없습니다**.

## 3-3. 사용법

```groovy
pipeline {
  agent any
  stages { 
     stage('name1') { 
       steps {      
          ...
       } 
       post {
         ...
       }
     }
     stage('name2') {
       steps {
          ...
       }
     }
  }
  post {
    ...
  } 
}
```

좀 더 자세한 설명을 원하시면 [공식 문서 - declarative-pipeline](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) 을 참고해보세요
