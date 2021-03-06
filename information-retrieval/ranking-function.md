# Ranking Function
핵심적인 ranking function 으로 tf-idf 와 BM25가 있다. 

## TF-IDF
여러 문서로 이루어진 문서군이 있을 때 어떤 단어가 특정 문서 내에서 얼마나 중요한 것인지를 나타내는 통계적 수치이다. 

### tf(Term Frequency)
- 용어빈도, 단어가 그 문서에서 나타난 횟수
- "데이터" 이라는 단어가 문서 내에 몇 번 출현했는가

### idf(Inverse Document Frequency)
- df 를 역수 취한 값
  - df: 문헌빈도, 해당 단어가 나타난 문서의 수 (단어 t가 포함된 문서의 수/전체 문서의 수)
  - df 가 높을수록, 많은 문서들에서 출현한 단어이므로 별로 중요하지 않은 단어를 의미하게 됨
- idf 는 역수이므로 높을수록 단어가 희귀하고 낮을수록 일반적인 단어가 됨
> 역수를 취하게 되면 문서의 수가 많아짐에 따라 idf 의 값이 기하급수적으로 커지기 때문에 로그를 씌운 값을 취한다. 

따라서, TF * IDF는 주어진 텍스트에서 용어의 상대적인 집중 정도를 측정한다. 
한 문서에서 "데이터" 라는 단어가 일반적으로 나타나지만, 다른 문서에서는 비교적 드물게 출현할 경우 TF * IDF 점수가 높다. 
반대로 "데이터" 단어가 있지만 다른 많은 문서에서도 굉장히 빈번하게 나타난다면 상대적으로 낮은 점수를 받게 된다.

추가적으로 **문서의 길이**도 측정을 해야한다. 예를 들어 600페이지에 달하는 굉장히 긴 문서에서 "데이터" 라는 단어가 
딱 세 번만 출현했다면, 그 문서는 "데이터"에 대해 거의 얘기하고 있지 않다고 보아야 한다. 
더 짧은 문서는 해당 단어와 관련이 있을 가능성이 높기 때문에 더 높은 점수를 받아야 한다. 
"fieldNorms" 라는 바이어스를 도입함으로서 문서의 길이에 대해서도 고려할 수 있다. 

## BM25
BM25 는 용어빈도(tf)의 영향을 제한하고, 필드 길이를 평균으로 조정한다. 
> tf-idf 에서 짧은 필드(제목 등)는 높은 점수를 받는다. 

### Tf on BM25

### Idf on BM25

### Document Length
