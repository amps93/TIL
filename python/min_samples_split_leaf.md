# 랜덤포레스트에서 min_samples_split과 min_samples_leaf의 차이점

* min_samples_split : 분할 할 수 있는 샘플 수 지정
  * min_samples_split = 4이면 샘플수 4까지 분할(3개 이하는 분할 안함)
* min_samples_leaf : 분할해서 leaf가 될 수 있는 샘플 수 지정
  * min_samples_leaf = 4이면 분할 했을떄 샘플수가 4이하이면 분할 안함(상위 규칙노드의 샘플수가 6이고 분할 했을때 샘플수가 3 / 3 이렇게 되면 상위 규칙노드가 분할하지 않고 리프 노드가됨(분할된 샘플이 4 이하이기 때문에))



min_samples_split = 6 개이고, min_samples_leaf가 4개인데, 6개의 sample로 Node에 개별 클래스 값이 각각 3개씩 들어가 있으면 min_samples_leaf의 최소 갯수가 4개이기 때문에 leaf node로 만들수 없어서 분할하지 못함