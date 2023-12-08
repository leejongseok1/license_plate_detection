# 차량 번호판 인식 프로젝트

## 프로젝트 파일 구조
- train.py : 모델 class를 인스턴스로 선언하고 For-loop을 돌면서 gradient descent를 수행하면서 파라미터를 업데이트 하는 로직
- evaluate.py / test.py : Training된 파라미터를 불러와서 evaluation이나 test/inference를 진행하는 로직
- model.py : Keras Subclassing 형태의 모델 구조 class 정의
- dataset.py : 데이터 전처리 및 batch 단위로 묶는 로직
- utils.py : 딥러닝 메인 로직 외에 유틸리티성 기능들을 모아놓은 로직
- loss.py : 모델의 Loss Function을 정의

## 문제 영역
- Text Detection : 이미지 내에 텍스트가 존재하는 영역의 위치정보를 Bounding Box로 찾는 문제 영역
- Object Detection 과의 차이점 : rotation angle 까지 고려하여 Detection 진행. 보통의 Object Detection은 rotation angle 고려하지 않음

## EAST (Efficient and Accuracy Scene Text)
- 2017년도에 text detection을 위해서 제안된 모델.
- ![image](https://github.com/leejongseok1/algorithm/assets/79849878/9b0d7d24-019a-4dea-a3fa-59b98d0bf318)
  > Multi-channel FCN 구조를 거쳐 Thresholding & NMS을 적용해서 간결한 형태의 두 가지 프로세스만 거쳐 Text Detection을 수행
- FCN Architecture : feature extractor stem layer(특징 추출), feature-merging branch layer, output layer


## CRAFT (Character Region Awareness For Text detection)
- 기존의 text detection은 rigid word-level bounding boxes를 네모로 검출하기 때문에 비는 공간이 많아지는 것을 보완하기 위해 만들어진 모델
- 단어 단위 예측이 아닌 **Character** 단위로 한 글자씩 예측하여 Character 간의 유사 정도를 **affinity**로 예측
- 한 글자씩 예측하면 완전 곡선 형태의 글자도 처리할 수 있는 것이 장점
- Character 단위로 예측하면 어느 글자까지가 하나의 의미 단어인지 파악하기 쉽지 않기 때문에 Character 단위로 예측한 것을 affinity score 기반으로 이을지 말지를 결정하여 단어 단위로 묶음
- ![image](https://github.com/leejongseok1/algorithm/assets/79849878/8ea0f59f-0aa8-4d34-8c76-987c0c41d296)

