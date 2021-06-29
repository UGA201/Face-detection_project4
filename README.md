# Face-detection_project4
- 딥러닝 얼굴 인식을 통한 데뷔 컨셉 추천 시스템
- 이미지 크롤링을 통한 기존 그룹 데이터 확보
- 전처리 및 모델선정, 학습
- 결과 분석
- 활용방안 제안
- 동일한 컨셉을 적용한 웹앱 제작 (ur-debut-concept 레포에 업로드)
<br>

### _**PPT 슬라이드와 아래 설명을 참고해 주세요.**_

![](https://images.velog.io/images/hability24/post/cc18b4f9-b24c-4c5a-a979-481749ab91c6/image.png)

![](https://images.velog.io/images/hability24/post/5e25953b-7e3b-4a15-b284-3c1f963db774/image.png)

![](https://images.velog.io/images/hability24/post/909d1536-3890-4895-960b-cd6717d0bf8b/image.png)

## 가설
- 엔터테인먼트 회사의 A&R 로서, 새로운 걸그룹 런칭에 앞서 어떠한 컨셉을 기획할지 고민 중

- 딥러닝의 힘을 빌려보겠습니다.

![](https://images.velog.io/images/hability24/post/737f7737-1c74-446c-b73b-daf80c11c2c3/image.png)
## 분석 방법
- 데뷔조 연습생들의 얼굴 이미지를 분석해서 기존 걸그룹 중 어떤 분들과 가장 매치가 되는지 살펴보기

- (기존 걸그룹) 그룹 색이 확고하고 큰 성공을 거둔 7팀을 선정

- 각 그룹의 멤버별 사진 50장을 구글 이미지 크롤링을 통해 수집해서 학습,

- 연습생의 사진을 넣고 인식하였을 때 어떤 그룹의 얼굴과 가장 유사하게 나오는지 확인


![](https://images.velog.io/images/hability24/post/3b1733cf-07b0-4547-8228-1b1739ff416b/image.png)

## 이미지 추출 및 전처리
### 이미지 크롤링
- 구글 이미지 검색에서 멤버 이름으로 검색해서 50장씩의 사진을 저장

- 약 1500장, 파이썬 셀레니움을 활용해서 자동 크롤링

### Face Detection
- Deepface의 detect_face 기능을 사용

- 사용할 모델에 맞게 전체 이미지 Resize

### Augmentation
- 이미지 회전, 반전 등으로 수량을 증폭시킴

### Label 지정
- 그룹별로 0~6번 까지를 부여


![](https://images.velog.io/images/hability24/post/d625d30d-c0d3-475b-b948-6820a86fe0af/image.png)

## 모델 선정
### CNN(Convolutional Neural Network, 합성곱 신경망) 
- 이미지 분석에서 많이 사용

- 은닉층에 Convolution과 Pooling layer를 사용해서 이미지 데이터의 특징을 잘 추출한다는 장점

### ResNet50
- 이미지 분류에서 좋은 성능을 가지고 있는 ResNet50 모델의 레이어 구성과

- imagenet에서 학습된 가중치를 가지고 얼굴인식에 적용 시, 좋은 성능을 얻지 못함

### VGGFace
- 얼굴 인식에 좀 더 특화된 모델 조사(VGGFace, FaceNet, OpenFace, DeepFace 등)

- DeepFace의 VGGFace를 basemodel로 활용

- VGGFace는 VGG16을 기반으로 하여 얼굴 인식에 적합하게 학습된 모델임

- 모델 성능은 test set의 loss 값을 기준으로 2->1로 감소

- 5번의 Cross validation을 통해 일반화 성능도 확인

![](https://images.velog.io/images/hability24/post/90039407-965b-45fa-9988-9de759674eed/image.png)

## 분석 결과
- 분석할 사진은 학습에 쓰이지 않은 타그룹 분들의 얼굴 이미지를 사용

- 가설대로 데뷔조의 이미지 분석을 한다면 그 분들의 사진을 입력하여 사용

- 분석결과는 가장 높은 비율로 나온 그룹의 명칭이 얼굴 사진 윗쪽에 나옴

- (예시) 왼쪽 위 사진 분석 결과 : 아이즈원의 컨셉이 잘 맞을 것

- (해석) 아이즈원의 컨셉이 어떤 것이냐를 판단할 방법
  1) 도메인지식 : 귀엽고 친근한 이미지이지만 음악적인 부분에서는 고급스러운 느낌을 강조한 것이 아이즈원의 컨셉이라고 보고 새 그룹 런칭에 활용

  2) 자연어처리 : 아이즈원의 기사, 뉴스 등의 키워드를 분석해서 빈출되는 단어들을 뽑아본 후 이를 참고하여 새 그룹 런칭에 활용

![](https://images.velog.io/images/hability24/post/00caf5d7-ab7a-49c5-b261-e7c32b76eb2d/image.png)

## 활용 방안

1) 자신의 얼굴을 입력하면 어떤 그룹과 매치되는지 알려주는 서비스(구현 완료)

  - (바로가기) <a href='https://ur-debut-concept.herokuapp.com/' target="_blank">사이트</a>

  - (GitHub) [https://github.com/UGA201/ur-debut-concept](https://github.com/UGA201/ur-debut-concept){: target="_blank"}

2) AI 그룹 런칭

  - Kpop에 AI를 접목시키려는 시도

  - Style GAN을 사용하면 상당히 선명하고 자연스러운 이미지를 얻을 수 있으므로

  - 세상에 없는 얼굴을 가지고 우리가 원하는 컨셉에 맞게 조정해서 AI 그룹을 런칭해볼 수 있지 않을까?

