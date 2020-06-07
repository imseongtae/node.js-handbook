# Node.js
<img width="256" alt="logos_nodejs" src="https://user-images.githubusercontent.com/60806840/83941064-40a37f80-a823-11ea-9980-64cf9caae050.png">

## What is the Node.js?
Node.js 교재에 대해 피드백을 전해드립니다.

## 피드백 목록
1. [Table Of Contents](#table-of-contents)
1. [개념과 설명 분리](#개념과-설명-분리)
1. [코드 정리](#코드-정리)
1. [학습목표 제시](학습목표-제시)
1. [모바일 사용자 고려 마크업](#모바일-사용자-고려-마크업)

---


## Table Of Contents
- **Table of Contents**의 항목을 클릭하면 문서내 요소로 이동하는 기능이 작동하지 않는 문제점이 있는데, 이를 해결하기 위해 링크 마크업은 **영문 소문자**를 사용하여 마크업하기를 요청드립니다. 
  - 목록의 **REST API**와 **Blocking** 문서는 이 점을 개선하였으니 참고해보시면 좋을 것 같습니다.

**[⬆ back to top](#피드백-목록)**

## 개념과 설명 분리
- 교재를 학습하면서 **개념**과 **덧붙이는 설명**이 다른 표기법으로 표현되면 더 좋지 않을까 생각이 들었습니다. 이는 마크다운 문법을 분리해 사용하면 해결할 수 있을 것 같은데, **NonBlocking** 문서의 내용으로 간단하게 예시를 적용해봤는데 어떻게 생각하시는지 궁금합니다.

- 개념은 순서 없는 목록 표기법 사용
- 덧붙이는 설명은 인용구 표기법 사용

### 블로킹에 대한 개념 설명
- Node.js 프로세스에서 추가적인 JavaScript의 실행을 위해 JavaScript가 아닌 작업이 완료될 때까지 기다려야만 하는 상황
- 일반적으로 NodeJS의 I/O 논블로킹으로 앞선 작업이 완료될때까지 후순위 작업이 기다려주지 않음
- I/O란 인풋,아웃풋으로 일반적으로 시스템 디스크 및 네트워크와 상호작용하는 것으로 이해하면 됨

### 선생님의 덧붙이는 설명

> 선생님👨‍🏫: 이것이 바로 백엔드와 클라이언트가 통신하는 방식입니다  
> 선생님👨‍🏫: 논블로킹을 사용하는 이유는 웹앱의 퍼포먼스를 극대화 하기 위함입니다.  
> 선생님👨‍🏫: 데이터를 불러올 때마다 지연이 발생하고, 다른 작업이 완료되지 못한다면 앱의 성능이 확연히 떨어질 것입니다.


## 코드 정리
- 몇몇 코드의 들여쓰기가 정리되어 있지 않습니다. `eslint`와 `prettier`를 활용해서 **코드 포맷팅 이후에 교재에 삽입**하면 더 높은 가독성을 가질 수 있을 것 같습니다.

### 기존 코드
```js
    module.exports.getList = (connection, options) => {
        connection.query('SELECT * FROM schools ', options.schoolName,  function (error, results, fields) {
            if (error) {
                res.status(404).json({result:false})
                    throw error;
            }                   
            connection.commit(async function(err) {
                if (err) {
                    res.status(404).json({result:false})
                    throw err;                    
                }                
                console.log('results : ',results)
                return results;
            });                
        });    
    });
```

### 코드 포맷팅이 완료된 코드

```js
module.exports.getList = (connection, options) => {
  connection.query('SELECT * FROM schools ', options.schoolName,  function (error, results, fields) {
    if (error) {
      res.status(404).json({result:false})
        throw error;
    }                   
    connection.commit(async function(err) {
      if (err) {
        res.status(404).json({result:false})
        throw err;                    
      }                
      console.log('results : ',results)
      return results;
    });                
  });    
});
```

## 학습목표 제시
- 각 **챕터의 학습목표**에 대한 조금 더 친절한 설명(?)이 있으면 좋겠습니다. 해당 챕터를 숙달하면 구현할 수 있게 되는 기능이 무엇인지 등 수업시간에 간략하게 설명해주시는 내용이 교재에도 첨부되어 있으면 좋을 것 같습니다. 
  - 가령, REST API를 학습하면 프론트엔드 개발자와 협업할 수 있는 이해가 생긴다.

**[⬆ back to top](#피드백-목록)**

## 모바일 사용자 고려 마크업
- 코드 블럭을 위한 마크업 표기법으로 텍스트를 표현하면 **모바일에서 가독성이 나빠집니다.** 이 점이 개선되었으면 좋겠습니다. 가독성 문제는 아래에서 이미지를 첨부하여 설명드리겠습니다.

**👇아래는 모바일 기기에서 교재를 확인할 때 가독성 비교**

### 코드블럭(`)으로 텍스트를 표현할 경우
- 가로 스크롤이 생겨서 모바일 기기에서 **가독성이 안 좋음**
- 교재를 이동 중에도 학습하는 경우가 많은데 휴대폰에서는 보기 불편함  

![order](https://user-images.githubusercontent.com/60806840/83944098-e367f800-a83b-11ea-966c-e20132ec6423.jpg)

### 순서가 없는 목록 문법(-)으로 텍스트를 표현할 경우
- 모바일에서 가로 스크롤이 생기지 않아서 훨씬 나은 가독성을 보임
- 코드와 텍스트를 명확히 분리할 수 있음

![none-order](https://user-images.githubusercontent.com/60806840/83944102-e7941580-a83b-11ea-8fdf-504bfb141f40.jpg)


**[⬆ back to top](#피드백-목록)**