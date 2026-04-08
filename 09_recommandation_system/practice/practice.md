# 사용자 기반 협업 필터링 실습

## 데이터셋
영화 데이터 https://grouplens.org/datasets/movielens/

`recommended for education and development` 섹션 하위 `ml-latest-small.zip` 다운로드

---

## 1. 데이터 로드 및 전처리

### 문제 1-1
`../data/ml-latest-small/movies.csv`, `../data/ml-latest-small/ratings.csv` 파일을 읽고 각각의 shape를 출력하시오.

### 문제 1-2
`ratings_df`와 `movies_df`를 `movieId` 기준으로 병합하여 `movie_rating_df`를 생성하시오.

### 문제 1-3
`pivot_table()`을 사용하여 사용자-영화 평점 행렬 `user_movie_df`를 생성하시오.
- index: `userId`
- columns: `title`
- values: `rating`
- 평점이 없는 값은 `0`으로 채우시오.

---

## 2. 사용자 기반 협업 필터링 준비

### 문제 2-1
`cosine_similarity()`를 사용하여 사용자-사용자 유사도 행렬을 계산하시오.
결과를 `user_sim_df` DataFrame으로 저장하시오.

(힌트: 사용자 기반 협업 필터링에서는 사용자-영화 행렬을 그대로 사용한다.)

### 문제 2-2
실제 평점이 있는 위치에서만 MSE를 계산하는 `movie_rating_mse(actual, pred)` 함수를 작성하시오.

### 문제 2-3
특정 사용자가 보지 않은 영화 목록을 반환하는 `get_unseen_movies(user_idx)` 함수를 작성하시오.

---

## 3. 사용자 기반 예측 평점 계산

### 문제 3-1
상위 유사 사용자 `topn`명을 이용해 모든 사용자의 모든 영화에 대한 예측 평점을 계산하는 `predict_ratings_user_based(topn=20)` 함수를 작성하시오.

다음 흐름을 따르시오.
1. 각 사용자마다 유사도가 높은 다른 사용자를 찾는다.
2. 자기 자신은 제외한다.
3. 상위 `topn`명의 평점만 사용한다.
4. 실제로 평점을 준 영화만 반영한다.
5. 유사도를 가중치로 사용하여 예측 평점을 계산한다.
6. 분모가 0이면 0으로 처리한다.

### 문제 3-2
예측 결과를 `rating_pred_user_df` DataFrame으로 변환하시오.

### 문제 3-3
사용자 기반 협업 필터링의 예측 MSE를 출력하시오.

---

## 4. 사용자 기반 영화 추천

### 문제 4-1
특정 사용자가 보지 않은 영화 중 예측 평점이 높은 영화를 추천하는 `recommend_movies_user_based(user_idx, topn=20)` 함수를 작성하시오.

반환 형식은 아래 컬럼을 갖는 DataFrame으로 하시오.
- `title`
- `pred_rating`
- `user_rating`

### 문제 4-2
예시로 `recommend_movies_user_based(100)`의 결과를 확인하시오.

---

## 5. 해석

### 문제 5-1
아이템 기반 협업 필터링과 사용자 기반 협업 필터링의 차이를 한두 문장으로 정리하시오.
