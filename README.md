# Amazon Bedrock Titan Image Generator

Amazon Bedrock의 Titan Image Generator 모델을 활용한 이미지 생성 데모 프로젝트입니다.

## 개요

이 프로젝트는 Amazon Bedrock의 Titan Image Generator를 사용하여 다음과 같은 이미지 생성 기능을 실습합니다:
- Text-to-Image: 텍스트 프롬프트를 통한 이미지 생성
- Inpainting: 이미지 내 특정 객체 대체
- Outpainting: 이미지 배경 대체

> 2023년 11월 29일 re:Invent 2023에서 소개된 Amazon Titan 멀티모달 FM을 사용합니다.
> (2023년 11월 30일 기준 us-west-2 리전에서 사용 가능)

## 주요 기능

### 1. Text-to-Image
다양한 프롬프트를 통해 이미지를 생성할 수 있습니다. 구현된 예제:
- 자연물 (이구아나)
- 제품 디자인 (스포츠 가방)
- 가상 모델 (패션)
- 식품 마케팅 (신선한 소고기)
- 음식 프로모션 (한국식 라면)

### 2. Inpainting & Outpainting
- Inpainting: 이미지 내 특정 객체를 다른 객체로 대체
- Outpainting: 이미지의 배경을 새로운 배경으로 대체

## 환경 설정

1. 필수 패키지 설치:
```bash
pip install "pillow>=9.5,<10"
```

2. AWS 자격 증명 설정:
```python
os.environ["AWS_DEFAULT_REGION"] = "<REGION_NAME>"  # 예: "us-west-2"
os.environ["AWS_PROFILE"] = "<YOUR_PROFILE>"
os.environ["BEDROCK_ASSUME_ROLE"] = "<YOUR_ROLE_ARN>"  # 예: "arn:aws:..."
```

## 사용 방법

Jupyter 노트북 `titan-image-generator.ipynb`를 실행하여 각 예제를 순차적으로 실습할 수 있습니다.

### 이미지 생성 설정
```python
body = {
    "taskType": "TEXT_IMAGE",  # TEXT_IMAGE, INPAINTING, OUTPAINTING
    "textToImageParams": {
        "text": prompt,
        "negativeText": negative_prompts  # 선택사항
    },
    "imageGenerationConfig": {
        "numberOfImages": 1,    # 1-5 범위
        "quality": "premium",   # standard 또는 premium
        "height": 768,         
        "width": 1280,         
        "cfgScale": 7.5,       # 1.0-10.0 범위
        "seed": 42             # 0-214783647 범위
    }
}
```

## 참조 문서

- [Amazon Titan Image Prompt Engineering Guidelines](https://d2eo22ngex1n9g.cloudfront.net/Documentation/User+Guides/Titan/Amazon+Titan+Image+Generator+Prompt+Engineering+Guidelines.pdf)
- [Amazon Titan Image models API](https://docs.aws.amazon.com/ko_kr/bedrock/latest/userguide/model-parameters-titan-image.html#model-parameters-titan-img-random)

## 프로젝트 구조
```
.
├── README.md
├── titan-image-generator.ipynb    # 메인 데모 노트북
├── data/                         # 샘플 이미지 데이터
└── utils/                        # 유틸리티 함수
    └── bedrock.py               # AWS Bedrock 클라이언트 설정
