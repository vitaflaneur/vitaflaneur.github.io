---
title: "머신러닝에서 베이지안(Bayesian)과 빈도주의자(Frequentist) 접근의 차이"
date: 2019-05-03 17:00 +0900
categories: 
  - ML
  - Theory
tags:
  - bayesian
  - frequentist
  - vs
published: true
---

##  Basics

### 빈도주의자 관점은?

- [빈도주의자 관점](https://en.wikipedia.org/wiki/Frequentist_probability){:target="_blank"}에서는 불확실성을 야기하는 ground truth가 있다는 가정 하에서 inference가 이루어진다.
- 불확실성(Uncertainty) 하에서 일어나는 어떤 이벤트가 있을 때, 빈도주의자 관점에서는 이 이벤트에 대한 데이터를 확률시행(random experiment)의 결과로 보고, 이를 반복하여 관찰해 나온 상대적 빈도(relative frequency)를 해당 이벤트의 불확실성에 대한 척도(measure), 즉 확률(probability)로 본다. 즉, 이 관점 하에서는 확률은 해당 이벤트의 발생가능도(likelihood, propensity, ...)를 표현하는 데 활용된다. 
- Ground truth를 모수 $\mathcal{T}$로, 데이터를 $\mathcal{D}$로 추상화하면 $p(\mathcal{D}\vert \mathcal{T})$로 표현되는 구조를 활용한 통계적 추정을 하는 것이다. 추정 자체에서는 오차를 고려하기 위해 $\mathcal{D}$에 대한 분포를 나타내는 $p(\mathcal{D})$를 활용하지만, $\mathcal{T}$는 고정되어 있어 $p(\mathcal{T})$를 고려하진 않는다. 
- 즉, **상대적 빈도를 통해 발생가능도를 추정함으로써 불확실성을 발생시키는 고정된 구조를 해석하는 것**이 빈도주의자 관점의 방식이라 할 수 있을 것이다. 
- 빈도주의자 관점에서 데이터는 확률시행의 결과이므로 randomness가 있고, 모수는 확률변수가 아닌 고정값이다. 

### 그렇다면 베이지안 관점은?

- [베이지안 관점](https://en.wikipedia.org/wiki/Bayesian_probability){:target="_blank"}에서는 불확실성을 야기하는 구조에 대한 주관적인 믿음(subjective belief)이 있고, 이를 데이터를 통해 수정하는 방식으로 inference가 이루어진다. 
- 불확실성 하에서 일어나는 어떤 이벤트가 있을 때, 관찰자는 이 이벤트가 어떠한 구조의 불확실성을 가지고 있다는 주관적인 가설을 가지고 있는데, 이 가설을 얼마나 신뢰할 수 있느냐를 사전확률(prior)로 나타낸다. 해당 이벤트에 대한 데이터는 발생한 증거(evidence)로서, 관찰자는 가지고 있던 가설 하에서 이 데이터가 얼마나 발생가능했는지(likelihood)를 활용해 사전의 가설을 수정한 새로운 가설을 얻게 되고, 이 새로운 가설에 대한 신뢰도를 사후확률(posterior)로 표현한다. 
- 사전 가설을 $\mathcal{H}$로, 데이터를 $\mathcal{D}$로 추상화하면 $p(\mathcal{H'}) = p(\mathcal{H}\vert \mathcal{D}) \propto p(\mathcal{D}\vert \mathcal{H}) \times p(\mathcal{H})$로 표현되는 구조를 활용한 통계적 추정을 하는 것이다. $p(\mathcal{H})$를 prior, $p(\mathcal{D}\vert \mathcal{H})$를 likelihood, $ p(\mathcal{H}\vert \mathcal{D})$를 posterior로 부른다. 
- 즉, **불확실성을 발생시키는 구조에 대한 가설의 신뢰도를 확률로 정량화 하고 데이터를 통해 이 가설을 수정해 나가는 것**이 베이지안 관점의 방식이라 할 수 있다. 
- 빈도주의자 관점과 정반대로 베이지안에서 데이터는 발생한 증거이므로 randomness 가 없고, 모수는 확률변수로 표현된다. 

------



## 예를 들면..

- 빈도주의자 관점을 "클래식"한 관점이라고 부르기도 하고, 우리나라 교육과정에서 처음 확률을 가르치는 방법과 맥락이 닿아있기도 한 덕에 아무래도 일상에서 확률을 떠올리다 보면 자연스럽게 빈도를 연상하곤 한다. 그러나 막상 불확실한 상황을 받아들이는 사고구조는 베이지안의 관점을 차용하는 경우가 종종 있다. 

- 다른 곳에서도 많이 인용하는 예로, 의사에게 진단을 받는 상황을 생각해보자. 병원에 가면 의사가 이런저런 진찰을 한 뒤 진단을 내려준다. 실제 엊그제도 골반이 아파 병원에 갔는데, 의사가 이것저것을 물어보고 엑스레이를 잔뜩 찍어 보더니 "내전근 염증인 것 같다"는 진단을 내려줬다. 

- 의사는 나를 포함한 비슷한 증상을 보이는 환자들을 여러명 치료한 이력이 있을 것이다. 이러한 사례들 중 내전근에 염증이 있었는 경우들의 빈도가 95%였다고 하자. 의사는 이 증상을 나타나게 하는 어떤 메카니즘이 있으며, 그 메카니즘(확률 모형) 하에서 일정한 빈도(모수) 만큼의 환자가 이러한 증상을 보이게 된다고 판단할 수 있다. 기존 환자들의 빈도를 토대로 의사는 해당 빈도를 95%로 추정하고, 이에 따라 "환자분은 95%의 확률로 내전근에 염증이 있을 것이다"라고 내게 말해준다. 그렇다면 의사는 빈도주의자적 관점을 취한 것이다. 

  의사는 다른 방식으로 이 문제에 접근을 할 수도 있다. 길고 긴 의대 시절을 통해 의사는 나와 같은 증상을 갖고 있을 때 원인이 내전근 염증일 확률이 90%라는 사전 지식(사전 확률)을 이미 갖고 있다. 공부를 마치고 실제로 환자들을 만나보니 내전근 염증이 있을 때 99%의 빈도로 해당 증상이 있었다.(발생가능도) 이에 의사는 90%라고 배웠던 사전 지식을 수정해서 해당 증상을 보일 때 95%정도 확률로 내전근에 염증이 있을 것으로 생각한다. (사후 확률) 이러한 경험 하에서 의사는 "환자분은 95%의 확률로 내전근에 염증이 있을 것이다"라고 내게 말해준다. 그렇다면 의사는 베이지안 관점을 취한 것이다. 

------



## 그럼 언제 어느 관점을 취하는 것이 옳을까?

- 빈도주의자 관점에서의 핵심은 반복적인 관찰이라고 할 수 있다. **'Long run'이 가능한 상황에서 prior로 인한 편향을 피하고, (한 번의 추정만을 수행할 경우) 베이지안에 비해 비교적 적은 계산으로도 불확실성을 모형화할 수 있다.** 예컨대, 동전의 앞면과 뒷면이 나오는 사건들에 대한 확률분포를 구하기 위해서는 반복해서 동전을 던진 뒤 각각의 면이 나오는 빈도를 세는 것으로 충분한 것이다. 이런 관점은 20세기 통계학과 과학적 방법론의 주요 흐름이었다. 

- 그러나, 이러한 접근이 언제나 가능한 것은 아니다. 특히, **빈도가 매우 낮은 사건에 대한 불확실성을 모형화하는 경우엔 빈도주의자적 접근이 현실적으로 가능하지 않은 경우가 많다**. Bishop 책에서 언급된 예시 중, '북극의 빙하가 이번 세기말까지 다 녹아 없어진다'라는 사건의 불확실성을 정량화하는 경우를 생각해보자. 북극의 빙하가 다 녹아 없어지는 빈도를 반복하여 센다는 것은 현실적이지 않기 때문에 이 사건은 빈도주의자 관점에서 모형화할 수 없다. 이럴 경우 베이지안 관점을 이용하는 것이 적절할 것이다. 

- 또한, **기계학습의 경우 데이터 전체를 활용하여 한번의 추정만을 할 수 있는 빈도주의자적 접근보다 새로운 데이터가 들어올 때마다 믿음을 수정하는 베이지안 접근이 더 높은 효용을 갖곤 한다.** 매일 쌓이는 데이터로 의사결정을 하는 경우를 생각해 보자. 빈도주의자적 접근의 경우 오늘의 새로운 의사 결정을 위해서는 어제까지 쌓여있는 데이터를 모두 다시 한 번 활용하여 추정을 수행하여야 한다. 시간이 흐르며 데이터가 쌓일수록 계산량은 많아질 것이며, 확률 시행 관점에서의 통제에 대한 문제도 고려해야 할 것이다. 반면, 베이지안 접근의 경우 오늘의 데이터만을 활용해 사후확률을 수정하고 이를 의사결정에 활용한다. 이는 효율적이고 직관적이라 할 수 있다. 

- 물론, 두 가지 관점이 다 가능한 경우도 있으며, 이런 경우 각각의 특징을 고려해서 선택을 하는 것이 적절할 것이다. 객관성의 필요, 계산량, 의사결정의 빈도, 가설의 불확실성에 대한 고려 여부 등의 포인트를 체크한다. 

  

------

## Technically

### Estimation

#### - 빈도주의자

- 빈도주의자 통계학의 추정을 언급하기 위해서는 우선 sampling distribution에 대해서 언급을 해야 한다. sampling distribution을 계산하기 위해 크게 두 가지 접근법이 있는데, Large sample theory로 analytic하게 접근하거나 bootstrap과 같은 Monte Carlo(MC) 테크닉을 사용하는 것이다. 	
  - 다음 함수들은 빈도주의자 관점과 large sample theory에서 활용되는 함수들이며 알아둘 필요가 있다. 
    - score function: $ s(\hat{\theta}) \triangleq \nabla \mathop{log}p(\mathcal{D}\vert \theta)\vert _{\hat{\theta}}$, log-likelihood의 $\hat{\theta}$에서의 기울기. 
    - observed information matrix: $ J(\hat{\theta}(\mathcal{D})) \triangleq -\nabla s(\hat{\theta}) =  - \nabla^2 \mathop{log}p(\mathcal{D}\vert \theta)\vert_{\hat{\theta}}$, negative score function의 $\hat{\theta}$에서의 기울기, 혹은 negative log-likelihood의  $\hat{\theta}$에서의 Hessian. 
    - Fisher information matrix: $ I_N (\hat{\theta}\vert \theta^{\ast}) \triangleq \mathop{var}_{\theta^{\ast}} \left[ \frac{d}{d\theta} \mathop{log} p(\mathcal{D}\vert \theta) \vert _{\hat{\theta}} \right] \overset{\hat{\theta}=MLE}{=} \mathbb{E} [ J(\hat{\theta}\vert \mathcal{D})] $

- 이렇게 구한 sampling distribution을 활용해서 Maximum Likelihood Estimator(MLE)로 point estimation을 하거나 confidence interval을 구할 수 있다. 



#### - 베이지안

- 베이지안 관점에서는 사후확률을 활용하고, 그 중 가장 유명한 것은 모수에 대한 point estimator로서 사후확률의 최빈값(mode)을 이용하는 maximum a posteriori (MAP) 추정이 있다. 
  - 사후확률 분포를 그대로 활용하거나 사후확률의 평균이나 중간값을 활용하는 방법도 있지만, MAP 추정을 수행하기 위한 효과적인 알고리즘이 대체로 존재하기 때문에 가장 일반적인 선택이다. 
  - Point estimator이기 때문에 uncertainty에 대한 measure가 없고, 때문에 overfitting을 초래할 수 있다. 
  - 모드는 일반적으로 분포에서 비전형적인(untypical)한 지점이기 때문에 이를 전체 분포에 대한 요약 지표로 활용하는 것은 기본적인 단점이 있다. 
  - 모수화에 의존, 즉, Reparameterization에 invariant하지 않다는 문제가 있다. 이를 해결하기 위해 Fisher information을 활용할 수 있다. 
- 위에서 언급된 MAP의 단점을 보완하기 위해 loss-function을 도입하면 사후확률의 평균이나 중간값을 사용하게 되기도 한다. 
- 베이지안 Interval estimator로서는 Credible Interval(CI)이나 Highest Posterior Density(HPD)를 주로 활용한다. 



###  Decision Theory & Model Selection

#### - 빈도주의자

- 빈도주의자의 경우 risk function을 결정 이론에 활용한다. 
  - risk function: $ \displaystyle R(\theta^{\ast}, \delta ) \triangleq \mathbb{E}_{p(\tilde{\mathcal{D}}\vert\theta^{\ast})} \left[ L(\theta^{\ast},\delta(\tilde{\mathcal{D}})) \right] = \int L(\theta^{\ast}, \delta(\tilde{\mathcal{D}}))p(\tilde{\mathcal{D}}\vert \theta^{\ast})d\tilde{\mathcal{D}} $
- 문제는 이때 우리가  $\theta^{\ast}$을 알지 못한다는 것이다. 따라서 $R(\theta^{\ast}, \delta )$를 $R(\delta)$의 형태로 만들어야 한다. 이를 해결하는 방법으로 bayes risk, minimax risk 등이 있다. 
  - Bayes risk: $R_B(\delta) \triangleq \mathbb{E}[R(\theta^{\ast}, \delta)]=\displaystyle \int R(\theta^{\ast}, \delta)p(\theta^{\ast} )d\theta^{\ast}$
    $\delta_B \triangleq \underset{\delta}{\mathop{argmin}} R_B(\delta)$  
    Bayes risk는 위와 같이 모든 truth parameter에 대한 average risk로 정의된다. 이를 최소하여 얻는 Bayes estimator는 posterior expected loss를 최소화 함으로써도 구할 수 있다. 
  - Minimax risk: $R_{max}(\delta)\triangleq \underset{\theta^{\ast}}{max}R(\theta^{\ast},\delta)$  
    $\delta_{MM} \triangleq \underset{\delta}{\mathop{argmin}} R_{max}(\delta)$
- 어떤 estimator는 가능한 모든 $\theta$에 대해 다른 estimator에 비해 큰 risk를 발생시킨다. 즉, dominate 당할 수 있다.  어느 estimator가 다른 estimator에게 dominate 되지 않을 떄, admissible하다고 한다. 그러나 admissibility 만으로는 estimator에 제약을 걸기는 충분하지 않다. Stein's paradox와 같은 경우를 통해 이를 확인할 수 있다. 
-  빈도주의자 결정 이론이 최적의 estimator를 선택하는 자동적인 방법을 제공하지 않기 때문에, 휴리스틱들을 사용해서 이를 보충한다. 이들은 consistency, unbiasedness, efficiency 등이며, 이런 성질을 갖는 estimator가 좋은 것으로 간주된다. 다만, bias-variance tradeoff 등의 현상을 통해 위 휴리스틱들을 동시에 만족하는 estimator를 찾을 수는 없다는 것이 알려져 있다. 
- 빈도주의자 결정 이론에서 risk의 계산은 실제 데이터 $\mathcal{D}$의 분포를 알아야 수행될 수 있다. 이를 알 수 없는 경우가 많기 때문에 $L(\theta, \delta(\mathcal{D}))$가 아닌 $L(y, \delta(x))$를 사용해 정의한다. 이때 $y$ 는 참이지만 알려지지 않은 반응값이고, $\delta(x)$는 입력 x에 대해 주어진 예측값이다. Unsupervised case일 경우 $L(y, \delta(x))$ 대신 $L(x, \delta(x))$를 활용하는데, 대표적인 예가 reconstruction error이다. 
- $p_{\ast}$ 가 unknown nature's distribution이라 가정하면 빈도주의자 관점의 리스크는 아래와 같이 표현되고, 이를 empirical distribution으로 대체하는 empirical risk를 정의할 수 있다.   
  - Frequentist risk: $$R(p_{\ast}, \delta ) \triangleq \mathbb{E}_{(\mathbf{x},y) \sim p_{\ast}} \left[ L(y, \delta(\mathbf{x}))\right] = \underset{\mathbf{x}}{\sum}\underset{\mathbf{y}}{\sum}L(y, \delta(\mathbf{x})) p_{\ast}(\mathbf{x},y)$$  
  - Empirical risk: $$R_{emp}(\mathcal{D}) \triangleq R(p_{amp}, \delta ) = \frac{1}{N} \sum_{i=1}^{N}L(y_i, \delta(\mathbf{x}_i)) $$  
  - Empirical risk minimization (ERM): $$\delta_{ERM}(\mathcal{D}) = \mathop{argmin}_{\delta} R_{emp}(\mathcal{D},\delta)$$  
  - Nature's distribution과 empirical distribution이 같을 경우 empirical risk는 bayes risk와 동일하다.   
- ERM은 드러난 데이터 만으로 분포를 가정해 추정을 하는 방식이기 때문에 overfitting의 위험이 있고 이를 피하기 위해 regularization 을 해야한다.  
  - Regularized risk minimization (RRM): $$\delta_{\lambda}=\mathop{argmin}_{\delta}[R_{emp}(\mathcal{D},\delta) + \lambda C(\delta)]$$
- 그러나 regularization strength인 $\lambda$를 정하는 문제를 해결해야 한다. 이를 해결하는 방식을 structural risk minimization이라고 부르고, 흔히 Cross validation(CV)와 theoretical upper bounds를 활용한다.  
  - Theoretical upper bound: $$ p\left(\underset{h \in \mathcal{H}}{\mathop{max}} \lvert R_{emp}(\mathcal{D},h) -R(p_{\ast} , h) \rvert>\epsilon \right) \leq 2dim(\mathcal{H})e^{-2N\epsilon^2}$$
- ERM과 RRM이 구하기 어려울 경우에는 surrogate loss function을 사용한다. log loss나 hinge loss가 그 예이다. 



#### - 베이지안

- 결정 이론에 대한 베이지안의 접근은 사후 예상 손실(posterior expected loss)을 최소화 하는 것이다. 0-1 loss일 경우 MAP가, L2 loss의 경우 posterior mean이, L1 loss일 경우 posterior median이 최적의 결정이 된다. KL loss를 사용할 수도 있다. 

- Model selection의 경우 모든 가능한 모델에 대해서 CV을 해서 구할 수도 있다. 그러나 그보다는 Bayesian model selection을 활용하는 것이 효율적일 수 있다.  즉, $p(m\vert \mathcal{D}) = \frac{p(\mathcal{D}\vert m)p(m)}{\sum_{m\in\mathcal{M}}{p(m,\mathcal{D})}}$에서부터 MAP, $\hat{m}=\mathop{argmax} p(m\vert \mathcal{D})$를 계산하는 것이다. 특히, 모델이 uniform prior를 가지고 있다고 가정하면, $\hat{m}=\mathop{argmax} p(m\vert \mathcal{D})=\mathop{argmax} p(\mathcal{D}\vert m) =\mathop{argmax}\int p(\mathcal{D}\vert \theta)p(\theta\vert m) d\theta $ 와 같이 쓸 수 있다. 이때 사용된 적분을 marginal likelihood라고 부르며, 이 방식으로 model selection을 할 경우 무조건 복잡한 모델이 선호되는 걸 막는 Bayesian's Occam's razor 효과를 갖는다. 

- 위 marginal likelihood의 적분은 계산하기 어려운 경우가 많다. 따라서 이를 근사하여 사용하곤 하는데, 가장 잘 알려진 방법은 Bayesian Information Criterion (BIC)을 활용하는 것이다. 
$$BIC \triangleq \mathop{log}p(\mathcal{D}\vert \hat{\theta}_{MLE}) - \frac{dof(\hat{\theta}_{MLE})}{2} \mathop{log}N \approx \mathop{log}p(\mathcal{D})$$

- 또한, full bayesian treatment라고도 불리우는 hierarchical bayesian model (HBM)을 사용할 수도 있다.  HBM은 hyperparameter를 도입함으로써 모델 parameter의 분포를 표현하는 방식으로 나타난다. 다만, HBM은 계산이 어려운 경우가 많다. 때문에 empirical bayesian model (EBM)을 활용해 근사하곤 한다. 

- 모수적 모델을 가정하고 parameter를 $\theta$, hyperparameter를 $\eta$로 표현할 때, 

  $$\displaystyle p(\theta\vert \mathcal{D}) = \frac{p(\mathcal{D}\vert \theta)p(\theta)}{p(\mathcal{D})}= \frac{p(\mathcal{D}\vert \theta)}{p(\mathcal{D})}\int{p(\theta\vert \eta)p(\eta)d\eta} $$  
  로 표현되는 HBM의 형식에서 적분이 어렵기 때문에,   
  
  $$\displaystyle p(\theta\vert \mathcal{D}) = \int {p(\theta\vert  \eta,\mathcal{D})p(\eta\vert \mathcal{D})d\eta} = \int{\frac{p(\mathcal{D}\vert \theta)p(\theta\vert \eta)}{p(\mathcal{D}\vert \eta)}p(\eta\vert \mathcal{D})d\eta} $$   
  $$\displaystyle p(\eta\vert \mathcal{D})=\int{p(\eta\vert \theta)p(\theta\vert \mathcal{D})d\theta}$$  

  와 같이 표현하고,  $\eta^{\ast} = \mathop{argmax}  p(\eta\vert \mathcal{D})$를 추정하여,   
  $$p(\theta\vert \mathcal{D})\simeq \frac{p(\mathcal{D}\vert \theta)p(\theta\vert \eta^{\ast})}{p(\mathcal{D}\vert \eta^{\ast})} $$  
  로 나타내면 EM algorithm으로 사후확률이 추정가능하다. 이 과정을 EBM이라 부른다. 

- $\eta^{\ast}$의 추정에서 균등사전확률을 가정하면, $\eta^{\ast} = \mathop{argmax}  p(\eta\vert \mathcal{D}) =  \mathop{argmax}  p(\mathcal{D}\vert \eta) $ 가 된다. 따라서 EBM을 type II maximum likelihood라고 부르며, ML에서는 evidence procedure라고 부르기도 한다. 또한, EBM은 prior가 data에 독립적이어야 한다는 원칙을 위배함으로써 계산적인 효용을 얻는 방식이다. 



## P.S.

더 깊은 수준의 정리를 원하시면 [Jake VanderPlas 버전의 정리](http://jakevdp.github.io/blog/2014/03/11/frequentism-and-bayesianism-a-practical-intro/){:target="_blank"}가 읽어볼 만합니다. 5개의 글로 나누어져 있고, 꽤나 자세합니다. 그냥 이 블로그를 복붙하고 번역하는 게 더 낫지 않았나 하는 생각도... 뭐, 짧은 버전의 메리트도 있는 법이니깐… 

또한, 이 포스팅은 기본적으로 [Murphy](https://mitpress.mit.edu/books/machine-learning-1) 책의 흐름을 따라가기도 하고 현재 제 의견도 반영하기도 하다보니 은연 중에 ML에서는 베이지안이 더 적합한 것으로 표현하고 있는데, [A Fervent Defense of Frequentist Statistics](https://www.lesswrong.com/posts/KdwP5i6N4E4q6BGkr/a-fervent-defense-of-frequentist-statistics)란 포스팅을 한 번 읽어보시면 빈도주의자 쪽의 디펜스도 접하실 수 있습니다. :)

------

## Reference

1. [Murphy's ML Book](https://mitpress.mit.edu/books/machine-learning-1){:target="_blank"}
2. [Bishop's PRML Book](https://www.microsoft.com/en-us/research/uploads/prod/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf){:target="_blank"}
3. Jake VanderPlas의 [blog](http://jakevdp.github.io/blog/2015/08/07/frequentism-and-bayesianism-5-model-selection/)와 [paper](https://arxiv.org/abs/1411.5018){:target="_blank"}
4. [데이터 사이언스 스쿨 - 확률의 의미 ](https://datascienceschool.net/view-notebook/9605664e26a0411b88f60e4ba9521dd9/){:target="_blank"}
5. Researcgate의 [한 thread](https://www.researchgate.net/post/What_is_the_difference_between_the_Bayesian_and_frequentist_approaches){:target="_blank"}
6. [A Fervent Defense of Frequentist Statistics](https://www.lesswrong.com/posts/KdwP5i6N4E4q6BGkr/a-fervent-defense-of-frequentist-statistics){:target="_blank"}



