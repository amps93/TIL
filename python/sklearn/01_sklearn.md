# 사이킷런

+ `pip install scikit-learn`



## 프로세스

1. 데이터 세트 분리 : 데이터를 학습 데이터와 테스트 데이터로 분리
2. 모델 학습 : 학습데이터를 기반으로 ML알고리즘을 적용해 모델을 학습
3. 예측 수행 : 학습된 ML 모델을 이용해 테스트 데이터의 분류를 예측
4. 평가 : 이렇게 예측된 결과값과 테스트 데이터의 실제 결과값을 비교해 ML 모델 성능을 평가 



## 교차검증

* 교차 검증을 활용하는 이유 : 모델의 과적합(특정 테스트 데이터에만 잘 작동되고 새로운 데이터가 들어왔을때 정확도가 떨어지는 경우)를 방지하기 위해



## KFold vs Stratified KFold

* 150개의 데이터르 3개의 데이터셋으로 나눈다는 가정하의 인덱스 number
  * KFold : 
    * [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50]
    * [51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
    * [101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 123, 124, 125, 126, 127, 128, 129, 130, 131, 132, 133, 134, 135, 136, 137, 138, 139, 140, 141, 142, 143, 144, 145, 146, 147, 148, 149, 150]
  * Stratified KFold : 
    * [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  50
        51  52  53  54  55  56  57  58  59  60  61  62  63  64  65  66 100 101
       102 103 104 105 106 107 108 109 110 111 112 113 114 115]
    * [ 17  18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  67
        68  69  70  71  72  73  74  75  76  77  78  79  80  81  82 116 117 118
       119 120 121 122 123 124 125 126 127 128 129 130 131 132]
    * [ 34  35  36  37  38  39  40  41  42  43  44  45  46  47  48  49  83  84
        85  86  87  88  89  90  91  92  93  94  95  96  97  98  99 133 134 135
       136 137 138 139 140 141 142 143 144 145 146 147 148 149]

* 위와 같은 이유로 보통은 Stratified KFold를 사용하나 Stratified KFold는 회귀분석이 불가능함 (회귀의 결정값은 이산값 형태의 레이블이 아니라 연속된 숫자값이기 때문에 결정값별로 분포를 정하는 의미가 없기 때문)
