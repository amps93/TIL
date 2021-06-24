# jupyter lab 가상환경 만들기

1. anaconda prompt 실행
2. conda deactivate
3. `conda create --name 가상환경이름 python=파이썬버전`
4. `conda activate 가상환경이름`
5. `python -m ipykernel install --user --name 가상환경이름 --display-name "주피터랩 이름"`
6. `conda install -c conda-forge jupyterlab`

