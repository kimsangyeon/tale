---
layout: post
title: "NodeJs Express multer?"
author: "Yeon"
---

# NodeJs Express Server 만들기

### NodeJs Express multer?
>Multer는 파일 업로드를 위해 사용되는 multipart/form-data 를 다루기 위한 node.js 의 미들웨어 입니다. 효율성을 최대화 하기 위해 busboy 를 기반으로 하고 있습니다.
busboy : node.js module for parsing incoming HTML form data.

### multer option
>Multer는 옵션 객체를 허용합니다. 그 중 가장 기본 옵션인 dest 요소는 Multer에게 파일을 어디로 업로드 할 지를 알려줍니다. 만일 옵션 객체를 생략했다면, 파일은 디스크가 아니라 메모리에 저장될 것 입니다.
기본적으로 Multer는 이름이 중복되는 것을 방지하기 위해서 파일의 이름을 재작성 합니다. 필요에 따라 해당 함수는 커스터마이징이 가능합니다.

Multer로 전달 가능한 옵션들은 다음과 같습니다.

- dest or storage : 파일이 저장될 위치
- fileFilter :어떤 파일을 허용할지 제어하는 함수
- limits :업로드 된 데이터의 한도
- preservePath :파일의 base name 대신 보존할 파일의 전체 경로

### upload method
#### .single(fieldname)
- fieldname 인자에 명시된 이름의 단수 파일을 전달 받습니다. 이 파일은 req.file 에 저장될 것 입니다.

#### .array(fieldname[, maxCount])
fieldname 인자에 명시된 이름의 파일 전부를 배열 형태로 전달 받습니다. 선택적으로 maxCount 에 명시된 값 이상의 파일이 업로드 될 경우 에러를 출력할 수 있습니다. 전달 된 배열 형태의 파일은 req.files 에 저장될 것입니다.

#### .fields(fields)
fields 인자에 명시된 여러 파일을 전달 받습니다. 파일 객체는 배열 형태로 req.files 에 저장될 것입니다.

#### .none()
오직 텍스트 필드만 허용합니다. 만일 파일이 업로드 되었을 경우, "LIMIT_UNEXPECTED_FILE" 와 같은 에러 코드가 발생할 것입니다. 이는 upload.fields([]) 와 같은 동작을 합니다.

#### .any()
전달된 모든 파일을 허용합니다. 파일 배열은 req.files 에 저장될 것입니다.


[참고: multer README-ko.md](https://github.com/expressjs/multer/blob/master/doc/README-ko.md)