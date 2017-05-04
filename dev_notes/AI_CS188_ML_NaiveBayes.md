
# ML: Naive Bayes

 - Up until now: how use a model to make optimal decisions
 - Machine learning: how to acquire a model from data / experience
    - Learning parameters (e.g. probabilities)
    - Learning structure (e.g. BN graphs)
    - Learning hidden concepts (e.g. clustering)
 - Today: model-based classification with Naive Bayes


## Classification

### Example: Spam Filter
 
 - Input: an email
 - Output: spam/ham
 - Setup:
    - Get a large collection of example emails, each labeled “spam” or “ham”
    - Note: someone has to hand label all this data!
    - Want to learn to predict labels of new, future emails
 - Features: The attributes used to make the ham / spam decision
    - Words: FREE!
    - Text Patterns: $dd, CAPS
    - Non-text: SenderInContacts
    - ...



### Example: Digit Recognition

 - Input: images / pixel grids
 - Output: a digit 0-9
 - Setup:
    - Get a large collection of example images, each labeled with a digit
    - Note: someone has to hand label all this data!
    - Want to learn to predict labels of new, future digit images
 - Features: The attributes used to make the digit decision
    - Pixels: (6,8)=ON
    - Shape Patterns: NumComponents, AspectRatio, NumLoops
    - ...

## Model-Based Classification

 - Model-based approach
    - Build a model (e.g. Bayes’ net) where both the label and features are random variables
    - Instantiate any observed features
    - Query for the distribution of the label conditioned on the features
 - Challenges
    - What structure should the BN have?
    - How should we learn its parameters?


## Naïve Bayes for Digits

 - Naïve Bayes: Assume all features are independent effects of the label
    - ![][1] 
 - Simple digit recognition version:
    - One feature (variable) Fᵢⱼ for each grid position `<i,j>`
    - Feature values are on / off, based on whether intensity is more or less than 0.5 in underlying image
    - Each input maps to a feature vector, e.g.
        - 1 -> F<sub>0,0</sub>=0, F<sub>0,1</sub>=1, ... , F<sub>15,15</sub> =0
    - Here: lots of features, each is binary valued
 - Naïve Bayes model:
    - P(Y|F<sub>0,0</sub> ... <sub>15,15</sub>) ∝ P(Y)·∏<sub>i,j</sub> P(F<sub>i,j</sub>|Y)
 - What do we need to learn?

## General Naïve Bayes

 - A general Naive Bayes model:
    - ![][1]
    - P(Y,F₁...F<sub>n<sub>) = P(Y)·∏ᵢP(Fᵢ|Y)
        - from |Y|x|F|ⁿ values
        - to n x |F| x |Y| parameters
 - We only have to specify how each feature depends on the class
 - Total number of parameters is linear in n
 - Model is very simplistic, but often works anyway

### Inference for Naïve Bayes

 - Goal: compute posterior distribution over label variable Y
    - Step 1: get joint probability of label and evidence for each label
    - Step 2: sum to get probability of evidence
    - Step 3: normalize by dividing Step 1 by Step 2

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/cs188_naive_Bs_inference.png)


## General Naïve Bayes, Cont.

 - What do we need in order to use Naïve Bayes?
    - Inference method (we just saw this part)
        - Start with a bunch of probabilities: P(Y) and the P(Fᵢ|Y) tables
        - Use standard inference to compute P(Y|F₁…F<sub>n<sub>)
        - Nothing new here
    - Estimates of local conditional probability tables
        - P(Y), the prior over labels
        - P(Fᵢ|Y) for each feature (evidence variable)
        - These probabilities are collectively called the parameters of the model and denoted by θ
        - Up until now, we assumed these appeared by magic, but…
        - …they typically come from training data counts: we’ll look at this soon

### Example: Conditional Probabilities

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/cs188_naive_Bs_example_CP.png)



    


---

 [1]: https://raw.githubusercontent.com/mebusy/notes/master/imgs/cs188_naive_BNs_bn4Digits.png







