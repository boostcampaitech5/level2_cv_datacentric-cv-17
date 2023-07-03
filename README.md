## level2_DataCentric_cv17_sixseg

### 글자 검출 프로젝트

<img width="80%" src="https://github.com/boostcampaitech5/level2_cv_datacentric-cv-17/assets/70469008/e1fb12f5-b231-4b2d-a17e-5015185ec919" />

OCR (Optimal Character Recognition) 기술은 사람이 직접 쓰거나 이미지 속에 있는 문자를 얻은 다음 이를 컴퓨터가 인식할 수 있도록 하는 기술로, 컴퓨터 비전 분야에서 현재 널리 쓰이는 대표적인 기술 중 하나입니다.

OCR task는 글자 검출 (text detection), 글자 인식 (text recognition), 정렬기 (Serializer) 등의 모듈로 이루어져 있으나, 본 대회에서는 '글자 검출' task 만을 해결하게 됩니다.

#### Team Members

강대호
강정우
박혜나
서지훈
원유석
정대훈

#### Point

본 대회는 데이터를 수집하고 활용하는 방법이 주요 내용이므로, 모델 관련 코드 및 test dataset에 대한 수정이 불가합니다. (상세 파일은 아래 참고)
따라서 해당 프로젝트는 annotation 파일의 구조와 노이즈 여부를 직접 살펴보고 이를 수정 및 개선하는 과정에 집중하였으며,
최종 제출 모델과 별개로 진행한 추가 실험 관련 코드만 업로드한 점 참고 부탁드립니다.

#### 프로젝트 진행 순서

1. 데이터 셋 EDA 및 노이즈 확인
2. 베이스 라인 성능 분석
3. 외부 데이터 셋을 사용한 성능 변화 여부 확인
4. Data re-labeling
5. Epoch 별 성능 체크
6. (추가 실험) data augmentation - canny
7. (추가 실험) multi-split, train&check, nms, ensemble 등을 활용한 train dataset 노이즈 제거 시도

#### Wrap-up Report

(추후 추가 예정)

#### Dataset

- "medical"이라는 이름의 진료비영수증 데이터셋
  - Input : 글자가 포함된 전체 이미지
  - Output : bbox 좌표가 포함된 UFO Format (글자 영역에 대한 bounding box 정보 외의 다른 정보는 필요로 하지 않기 때문에 전체 UFO 형식 중 "points"에 해당하는 값들만 포함)
    <img width="80%" src="https://github.com/boostcampaitech5/level2_cv_datacentric-cv-17/assets/70469008/eb3e3e9c-18bb-4131-993e-33cb8f925424" />
- train
  - 총 300장 (기본 제공 100장 + 캠퍼들이 직접 라벨링을 진행하여 노이즈가 많은 200장)
  - 개인정보에 해당되는 영역은 masking 처리되어 있으며 중요하지 않은 텍스트 정보는 blur 처리
- test
  - 이미지 내 단어 수의 평균이 300개, 최대 약 600개 까지 있는 데이터로 다양하게 구성
  - 언어는 주로 한국어이고, 영어도 일부 포함
  - 총 100장 (Public 테스트셋으로는 50%인 50장이 공개되고, 나머지 데이터 50장은 Private 테스트셋으로 활용)

#### Competition Rules

- 평가방법은 7강에서 소개되는 DetEval 방식으로 계산되어 진행됩니다.
- ['masked', 'excluded-region', 'maintable', 'stamp'] 에 해당되는 영역은 ignore 처리하므로 검출하지 않아도 됩니다.
- 베이스라인 모델인 EAST 모델이 정의되어 있는 아래 파일들은 변경사항 없이 그대로 이용해야 합니다.
  - model.py / loss.py / east_dataset.py / detect.py
  - 변경이 금지된 파일들의 내용을 이용하지 않고 모델 관련 내용을 새로 작성해서 이용하는 것도 대회 규정에 어긋나는 행위입니다.
- 성능 향상을 위해 공공 데이터셋 혹은 직접 수집한 데이터셋을 추가적으로 이용하는 것을 제한하지 않습니다.
