# NLP(자연어 처리): 텍스트 분류

## 비즈니스 사례

고객들이 가지고 있는 요구사항을 충족하고, 실제로 제품을 만들고 제공하는 일은 아주 어려운 일 입니다. 오늘 당신은 아마존 이커머스 팀의 머신러닝 팀에 조인 했습니다. 이커머스 웹페이지에는 각 상품의 고객으로 부터 리뷰가 많이 쌓여 있습니다. 여러분의 제품 오너들은 부정적인 의견에 대해서 **즉시** 알고 싶어 합니다. 최종적으로 제품 오너들은 리뷰가 왜 부정적인지를 알고 싶어 합니다.

[역자 추가] **아래의 예시는 부정 의견을 분석하여 3개의 주제로 분류하고, 부정적인 단어가 영향이 큰 것을 워드 클라우드로 가시화 했습니다.**<br>
한번 아래와 같은 워드 클라우드를 만들어서 제품 오너에게 제공하면 어떨까요?

![0.az-groc-3](Images/0.az-groc-3.png)

## 토픽 모델링
여러분의 리서치 팀은 리뷰의 긍정, 부정에 대한 레이블링 작업을 마치었습니다. 이제 여러분은 모델링 작업을 할 준비가 되었습니다.
여러분의 일은 부정적인 리뷰의 주제별 분류를 하는 겁니다. 
- 아래 언급된 데이타셋을 다운로드 하고, 리뷰에서 부정적인 것만 추출 하세요.
- 부정적인 리뷰를 Amazon Comprehend에 로딩하세요. 아래 컴프리핸드 문서를 읽어 보세요.
    - https://docs.aws.amazon.com/comprehend/latest/dg/what-is.html 
    - 여러분은 컴프리핸드 콘솔 혹은 여러분의 쥬피터 노트북에서 작업할 수 있습니다. 노트북에서 작업을 한다면, Sagemaker execution role에 Comprehend role을 꼭 추가를 해주세요.
- 여러분이 주제들을 추출한 후에, 주제들을 읽어보세요. 주제들이 의미가 있습니까? 또한 주제들에 대해서 설명을 써보세요. 아마도 쉽지은 않을 겁니다. 
- [역자] 위의 컴프리핸드의 한글에 대한 토픽 모델링은 품질이 떨어집니다. 옵션으로서 생각하시고, 아래 확장으로 넘어가셔도 좋습니다.

## 확장
컴프리핸드를 사용한 후에, 여러분은 두개의 방향으로 개선할 수 있습니다. 고급 단계로서 여러분은 두개의 방향을 모두 할 수 도 있습니다.

(1) 여러분 자신의 토픽 모델러를 만드세요. SageMaker는 두개의 내장 알고리즘인 Latent Dirichlet Allocation and Neural Topic Modeling를 가지고 있습니다. 한개 혹은 두개를 선택한 후에 여러분의 데이터를 학습 해보세요. 결과로 나온 주제들이 어떻습니까? 주제들이 컴프리핸드에서 나온 것과 더 좋습니까? 안 좋습니까? 
- [역자 추천: Neural Topic Modeling 으로 접근 해보세요. Latent Dirichlet Allocation 보다 성능이 더 좋다는 논문 결과가 있습니다.]

(2) 여러분의 데이터를 다시 레이블링 하세요. 발견된 리뷰의 세부 카테고리들 혹은 서로 연관된 리뷰 중에서 일부 리뷰를 추출하여, 여러분은 그 리뷰에 추가적인 레이블링을 할 수 있습니까? SageMaker Ground Truth를 사용하면 추가 포인트를 받을 수 있습니다. 여러분은 분류한 세부 카테고리들을 인지하는 모델을 만들수 있을까요? 


## 데이터 셋 설명 (본래 요구사항은 영문 Amazon.com 리뷰를 사용 함)
[역자 추가] 데이터 세트는 Amazon.com의 상품 리뷰내용을 가져와서 사용합니다. 영문이기에 Amazon Translate로 한글로 번역을 한 이후에 사용 합니다. 리뷰 등급이 1-2 만을 가져와서 부정 리뷰로 사용을 합니다. 아래의 샘플 코드 섹션에 데이터 다운로드 및 코드의 URL이 있습니다.<br>
또한 여러분이 공개적으로 얻을 수 있는 한글 데이터를 사용해서 테스트 해보시면 좋습니다.


# 연구 진행 사항
여러분의 리서치 팀은 convolution을 사용하여 텍스트를 분류하는 발전된 모델을 개발했습니다. 자세한 사항은 아래 URL을 참조 하세요. http://xzh.me/docs/charconvnet.pdf 
- [역자]: 위는 원문의 추천내용 입니다. 참고만 하세요.

# 샘플 코드
[역자 추가] 샘플 코드는 "토픽 모델링을 사용한 온라인 상품 부정 리뷰 분석" ( https://github.com/gonsoomoon-ml/topic-modeling ) Git Repo를 이용하세요. 이 Repo보다 조금더 발전된 것을 만들어 보세요.
