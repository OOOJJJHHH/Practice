# 연산자 활용
```R
산술 : v1 ( +, -, /, %/%, %% ) v2

비교 : v1 ( >, <, >=, <=, ==, &, | ) v2

- 벡터에서 조건에 맞는 값 추출 : v1[v1 > 5]
- v1배열 안에서 5보다 큰 값만 추출
```

# 벡터 작성
- 벡터는 동일한 타입을 가진 값들의 집합

## 벡터 생성 방법
```R
x = c(1,2,3,4)
x = c("a","b","c","d")

x = c(1:4)

seq(1:10, by=2)
- 1부터 10까지수를 1부터 2씩 증가하면서 배열에 추가

rep(1:3, times=2)
- 1부터 3까지의 값을 2번 반복
```

## 벡터 속성 확인
```R
length(x)
- 벡터의 길이

class(x)
- 데이터 타입

typeof(x)
- 내부 저장 방식
```

## 벡터 연산
```R
x = c(1,2,3)

x + 1
- x벡터의 모든 값에 1더함
x * 2
- x벡터의 모든 값에 2곱함

x = c(1,2,3)
y = c(21,22,23)
x + y
- 배열의 같은 인덱스끼리 합
- 만약 배열의 길이가 다르다면 짧은 쪽의 배열이 재활용 되면서 더해짐

cat(1, NA, 2)
- NA 포함해서 출력 1, NA, 2

cat(1, NULL, 2)
- NULL 빼고 출력 1, 2

sum(1, NA, 2)
- NA 값

sum(1, NULL, 2)
- NULL 제외하고 계산
```

## 벡터 조건에 맞는 값 출력
```R
x <- c(10, 20, 30, 40)

x[1]
- 첫 번째 요소

x[2:3]
- 2~3번째 요소

x[-1]
- 첫 번째 요소 제외

x[x > 30]
- 10보다 큰 값만 추출
```

# 벡터 형 변환
```R
as.character(c(1, 2, 3))
- 숫자 → 문자

as.numeric(c("4", "5"))
- 문자 → 숫자

c(1, "a", TRUE)
- 만약 문자형(String)이 하나라도 있으면 나머지 모든 데이터의 형태가 String으로 변환
```

# 백터 활용 함수
```R
sum(x) : 합계
mean(x) : 평균
max(x) : 최대값
min(x) : 최소값

sort(x)
- 오름차순으로 정렬

order(x)
- 오름차순으로 정렬하는데 출력되는 값은 저장되어있는 실제 값의 인덱스 값이 보여짐
- c(3,1,2) -> 2, 3, 1

unique(x)
- 중복을 제거하고 출력

duplicated(x)
- 중복여부를 TRUE/FALSE로 반환

x = c(10, 20, 30)
names(x) = c("apple", "banana", "cherry")
- 벡터 생성 후 이름 지정
- 만약 names 길이가 더 작으면 리사이클링 수행
x <- c(apple = 10, banana = 20, cherry = 30)
- 벡터 생성 시 이름 지정

x["banana"]
- x 백터의 banana 이름을 가지고 있는 값을 출력
x[c("cherry", "apple")]
- x 백터의 cherry, apple 이름을 가지고 있는 값을 순서대로 출력
```
# 날짜 관련 ( Date, POSIXct, POSIXlt )
### Date
- 날짜만 저장 (yyyy-mm-dd)
- 시간 없음

`as.numeric(as.Date("2023-01-02"))`
- 결과 : 19358 (1970-01-01부터 19358일)
- 일(day)로 저장

### POSIXct
- 날짜 + 시간 저장 (숫자 기반)

`as.numeric(as.POSIXct("1970-01-02 00:00:00"))`
- 결과 : 86400초 = 하루
- 1970-01-01부터의 초(second)로 저장

### POSIXlt
- 날짜 + 시간 + 구조 분해 가능

- 내부적으로 리스트 구조로 저장됨 (연, 월, 일, 시, 분 등 나눠서 접근 가능)
```R
t <- as.POSIXlt("2023-01-01 15:30:00")
t$hour   # 15
t$mon    # 0 (1월은 0부터 시작!)
t$wday   # 0 (일요일)
```

### 날짜 형변환
```R
Date → POSIXct
as.POSIXct(as.Date("2023-01-01"))

POSIXct → Date
as.Date(as.POSIXct("2023-01-01 15:30"))

POSIXct → POSIXlt
as.POSIXlt(as.POSIXct("2023-01-01 15:30"))

POSIXlt → POSIXct
as.POSIXct(as.POSIXlt("2023-01-01 15:30"))
```

### 날짜 다양한 포맷 지정
```R
datetime = as.POSIXct("2023-04-21 15:30:45")

format(datetime, "%Y-%m-%d")
- "2023-04-21"

format(datetime, "%d/%m/%Y")
- "21/04/2023"

format(datetime, "%H:%M:%S")
- "15:30:45"

format(datetime, "%Y-%m-%d %H:%M")
- "2023-04-21 15:30"

format(datetime, "%Y년 %m월 %d일 %H시 %M분")
"2023년 04월 21일 15시 30분"
```

### lubridate 패키지를 사용할 때 제공되는 함수
```R
year()
- 연도 추출	2023

month()
- 월 추출	4

day()
- 일(day of month) 추출	21

wday()
- 요일 (숫자, 기본적으로 일요일=1)	6

wday(date, label = TRUE)
- 요일이 숫자가 아닌 한국어로 요일을 출력

hour()
- 시 추출 (시간 포함일 경우)	13 등

minute()
- 분 추출	30

second()
- 초 추출
```

# MATRIX
```R
mat <- matrix(1:9, nrow = 3, ncol = 3)
- 1부터 9까지의 숫자를 3x3 행렬로 변환
- 왼쪽부터 세로로 값이 추가 됨

byrow = TRUE
- 기능 추가할 시 가로로 숫자가 채워짐

rownames(mat) = c("Row1", "Row2", "Row3")
- 왼쪽에 row(가로)줄 앞쪽마다 이름 생성

colnames(mat) = c("Col1", "Col2", "Col3")
- 위쪽에 column(세로)줄 위쪽마다 이름 생성

mat[1, 2]  # 4
- 첫 번째 행, 두 번째 열의 값 추출

mat[2, ]   # 2 5 8
- 두 번째 행, 모든 열을 추출

mat[, 1]   # 1 2 3
- 모든 행, 첫 번째 열을 추출


```


# LIST














