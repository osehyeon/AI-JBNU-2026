# GPU 커널, Triton으로 직접 짜 보기

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/osehyeon/AI-JBNU-2026/blob/main/notebooks/triton_lab.ipynb)

**위 Open In Colab 버튼을 누르면 바로 시작합니다.** 설치할 것은 없고 Google 계정만 있으면 됩니다.

파이썬으로 GPU 커널을 쓰고, 왜 빨라지는지 직접 잽니다. 끝나면 내 GPU에서 잰 결과 그래프가 남습니다.

```text
같은 Softmax 세 가지 ──▶ 벡터 덧셈 커널 ──▶ Softmax 커널 ──▶ 내 GPU 그래프
```

강의 자료는 [`slides.pdf`](slides.pdf)에 있습니다.

## 따라 하기

1. 위의 **Open In Colab** 버튼을 누르고 Google 계정으로 로그인합니다.
2. 메뉴 **런타임 > 런타임 유형 변경**에서 **T4 GPU**를 고르고 저장합니다.
3. 위에서부터 셀 왼쪽의 ▶를 눌러 하나씩 실행합니다. Google이 만든 노트북이 아니라는 경고가 나오면 **계속 실행**을 누릅니다.
4. `TODO`가 적힌 줄을 고치고 그 셀을 다시 실행합니다.
5. **5. 결과 그래프** 셀의 그림을 우클릭해 저장합니다.

수업을 놓쳤으면 메뉴 **런타임 > 모두 실행**을 누릅니다.

## 노트북 순서

| 번호 | 내용 | 내가 하는 일 |
| --- | --- | --- |
| 1 | GPU 확인 | 셀 실행 |
| 2 | 같은 Softmax인데 왜 시간이 다를까 | 커널 수와 시간 비교 |
| 3 | 실습 1: 벡터 덧셈 | `BLOCK_SIZE` 바꿔 보기 |
| 4 | 실습 2: Softmax custom kernel | 계산 한 줄 고치기, 속도 비교 |
| 5 | 결과 그래프 | 그림 저장 |
| 6 | 선택 과제: 행렬곱과 autotune | `RUN_MATMUL = True`로 바꿔 실행 |

## 막힐 때

| 증상 | 해결 |
| --- | --- |
| GPU가 연결되지 않았다는 오류 | 런타임 > 런타임 유형 변경 > T4 GPU를 고르고 모두 실행 |
| GPU를 할당받지 못했다는 안내 | 무료 GPU는 사용량이 많으면 막힐 수 있습니다. 옆 사람과 같이 보거나 다른 Google 계정으로 시도합니다 |
| `name 'results' is not defined` | 위 셀을 건너뛰었습니다. 런타임 > 모두 실행 |
| 2번 셀에 `triton_` 이름이 안 보임 | 일부 환경에서는 프로파일러가 이름을 잡지 못합니다. 커널 수만 봐도 됩니다 |
| 실습 2에서 `정답과 같은가: False` | `num`을 `tl.sum(num, axis=0)`으로 나눴는지 봅니다. 그래도 안 되면 정답 셀을 엽니다 |
| 메모리 부족(`CUDA out of memory`) | 런타임 > 세션 다시 시작 후 모두 실행. `n`을 줄입니다 |

## 폴더

| 위치 | 내용 |
| --- | --- |
| `notebooks/triton_lab.ipynb` | 실습 노트북 |
