# 기존 코드에서 달라진 것들

## .db 이름
db이름을 person에서 student로 전환.(sqliteManager.java의 SQLITE_FILE_DB_URL 변수)

## field에 학번 추가
#### int
일단 아무 생각없이 학번을 쳤는데 int < 학번 이어서 long으로 전환하자 생각했다.
#### long
학번은 계산하는 것이 아니기 때문에 굳이 정수형으로 하지 않아도 된다. string으로 전환해야 한다는 것을 알았다.
#### string
string으로 바꾸었다. 하지만 여전히 에러가 있었다. long 이후의 에러는 query 부분에서 나는 것이었다.
### 경험한 데이터 입력 불가 에러와 그 문제
두 가지 모두 정말 사소하지만, 절대 사소하지 않은 실수(?)였다.
1. ?,?,? 자릿수

    DMLService 에서 insert를 위해 정의할 때, table name 뒤에는 변수명을, 뒤에는 ?를 변수 개수만큼 넣어야 하는데, 이를 인지 하지 못하고 사달이 났다.
    ``` 
    참고 이미지
    ![image](https://user-images.githubusercontent.com/80017031/123920038-80a24b00-d9c0-11eb-82fc-8bf7a995a937.png)
    ```
3. 입력할 때 번호 매기기

    그 뒤에 각각의 변수들을 얻어야 하는데, data mapping을 하려면 위의 이미지에 나온 변수 순서대로 1부터 순서를 붙이고 입력을 하게 된다.
    이를 제대로 인지하지 못하고 그대로 복붙해서 붙였다가 계속 에러가 발생했다.
    update도 마찬가지로 문제가 있었다.
    ``` 
    ![image](https://user-images.githubusercontent.com/80017031/123920492-f7d7df00-d9c0-11eb-9876-670eaa6d413d.png)

    ```
    정말 깨알 같지만 너무 큰 문제점이었다.
