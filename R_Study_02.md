### 데이터 프레임 만들기

```r
english <- c(90, 80, 60, 70)
math <- c(50, 60, 100, 20)

df_midterm <- data.frame(english, math)
df_midterm
```

```r
class <- c(1, 1, 2, 2)

df_midterm <- data.frame(english, math, class)
df_midterm

mean(df_midterm$english)
mean(df_midterm$math)
```

### 엑셀 파일 불러오기

-   install.packages("readxl") : 엑셀 파일을 불러오는 패키지

```r
library(readxl)

# getwd()를 통해 작업 폴더를 확인, setwd()를 통해 작업 폴더를 설정
df_exam <- read_excel("./Data/excel_exam.xlsx")
df_exam

mean(df_exam$english)
```

-   엑셀 시트가 여러 개 존재하면 시트 번호를 지정하여 읽기

```r
df_exam_sheet <-
  read_excel("./Data/excel_exam_sheet.xlsx", sheet = 3)
df_exam_sheet
```

-   col_names = F : 첫 번째 행을 변수명이 아닌 데이터로 인식(...숫자)

```r
df_exam_novar <- read_excel("./Data/excel_exam_novar.xlsx")
df_exam_novar

df_exam_novar <- read_excel("./Data/excel_exam_novar.xlsx", col_names = F)
df_exam_novar
```

### CSV 파일 불러오기 및 저장

-   csv 파일 불러오기

```r
df_csv_exam <- read.csv("./Data/csv_exam.csv")
df_csv_exam
```

-   서수형으로 되어있는 것은 stringsAsFactors = TRUE로 설정

```r
df_csv_exam <- read.csv("./Data/csv_exam.csv", stringsAsFactors = TRUE)
df_csv_exam
```

-   csv 파일 저장

```r
df_midterm <- data.frame(
  english = c(10, 20, 30, 50),
  math = c(20, 60, 80, 90),
  class = c(1, 2, 3, 2)
)

# 데이터 프레임을 csv 파일로 저장
write.csv(df_midterm, file = "./Data/df_midterm.csv")
```
