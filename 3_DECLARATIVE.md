# 3. Declarative 문법

안녕하세요?  
이번 시간에는 젠킨스 파이프라인의 Declarative 문법을 소개드리겠습니다.  
  
지난 시간에 전달드린 Scripted 문법은 자유로운 문법을 자랑함을 알려드렸는데요.  
Declarative 문법은 Jenkins에서 **전통적으로 수행 하던 방식과 유사**합니다.  
이렇게 설명드리면 좀 애매한데, 최대한 젠킨스 **웹 페이지의 기능 혹은 설정과 유사한 형태를 문법으로 옮겨놓은 것**이라고 생각하시면 될 것 같습니다.  

## 3-1. 장점과 단점

Declarative 문법의 장점과 단점은 다음과 같습니다.

### 장점

* 명확하고 강제화된 구조
  * 젠킨스의 웹 페이지에 있는 양식 항목을 그대로 코드로 나타냈다고 보시면 됩니다.
* 가독성이 좋습니다
  * 아무래도 구조적으로 잘 잡혀 있어 읽기 쉽습니다.
* 논리적인 내용을 정의하기 보다는 좀 더 상위의 개념적인 접근에 어울립니다.
* [Blue Ocean](https://novemberde.github.io/devops/2017/10/21/Jenkins.html)을 통해 생성 가능
* 예전부터 있던 젠킨스의 개념들 (알람 등)에 매핑되는 문법이 존재
* 더 나은 문법 검사
  * 스크립트 시작 부분에서 바로 문법 오류 체크 (Scripted는 실행시점에 확인합니다.)
  * 아무래도 즉시 발견되다보니 시간 절감
* 파이프라인간의 일관성 증가

### 단점

* 반복 로직에 대한 지원 부족
  * Scripted에서 ```for```를 사용하는 것과 달리 Declarative에서는 직접적인 기능이 없습니다.
* try ~ catch 등의 지원 부족
  * 실패를 잡아 처리하는 로직이 필요하다면 예전에 작성한 [포스팅](https://jojoldu.tistory.com/409)을 참고해보세요.
* 아직도 발전하고 있습니다
  * 전통적인 젠킨스의 기능이 100% 다 구현된게 아닙니다.
* 너무 견고한 구조
  * 사용자가 파이프라인 코드를 다루기가 어려움
  * 지정된 구조 외에는 사용하기가 까다롭습니다.
* 현재 기준으로 더 복잡한 파이프 라인이나 워크 플로우에는 적합하지 않습니다.


## 3-2. 문법

Declarative 문법에는 별도의 기능을 지원하는 Sections와 Directive (지시어 정도로 이해해주세요.)가 있습니다.  
Sections와 Directive를 이용해 필요한 파이프라인 작업들을 작성합니다.  
아래는 대표적인 Sections와 Directive들 입니다.  
  
단, ```pipeline```의 경우 Directive 문법을 쓰기 위해선 항상 선언되어있어야만 합니다.

| 이름   | 타입 | 설명   |
|  ---  |  ---  | --- |
|  ```agent```     | Sections   |
|  ```stages```     |      |
|  ```stage```     |   Directive     |
|   ```steps```    |     |
|  ```post```     | **빌드가 끝난 후** 조건 (성공/실패 등)에 따라 실행할 내용 선언  |
|  ```when```     |  |
|  ```script```     | Declarative에서 Scripted 문법을 사용할 수 있게 지원합니다. |

> 위의 Directive는 Declarative 전용입니다.  
즉, **Scripted 문법에서는 사용할 수 없습니다**.

A valid Declarative pipeline must be defined with the “pipeline” sentence and include the next required sections:

* agent
* stages
* stage
* steps
 

Also, these are the available directives:

* environment (Defined at stage or pipeline level)
* input (Defined at stage level)
* options (Defined at stage or pipeline level)
* parallel
* parameters
* post
* script
* tools
* triggers
* when

## 3-3. 사용법

```groovy
pipeline {
  agent any
  stages {
     stage('name1') {
       steps {
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
    always {
      echo "Pipeline Executed!"
    }
  }
}
```

좀 더 자세한 설명을 원하시면 [공식 문서 - declarative-pipeline](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) 을 참고해보세요

## 




## 참고

* [how-to-use-the-jenkins-declarative-pipeline](https://www.blazemeter.com/blog/how-to-use-the-jenkins-declarative-pipeline)
