# Machine Learning Intro

[Source: Google](https://developers.google.com/machine-learning/crash-course/)

## ML Concepts

- Why: ML as a valuable tool to help make sense of data

- What: Supervised ML systems learn how to combine input to produce useful predictions on never-before-seen data

- Benefits:
  - reduce time programming: ML creates own algorithms by giving examples
  - customize and scale products: ML algo can be used for derivates (e.g. other languages)
  - complete seemingly unprogrammable tasks: e.g. read peoples' body language

## Framing

- Features: an input variable — the x variable in simple linear regression: e.g. `Email from:`, `Word Count`

- Label: the thing we're predicting — the y variable in simple linear regression: e.g. `Spam` or `Not Spam`

- Example: a particular instance of data: x:

  - Labeled Example has (feature, label): (x, y) => used to train the model
  - Unlabeled Example has (features, ?): (x, ?) => used for making predictions on new data

- Model: defines the relationship between features and label: y => defined by internal parameters, which are learned:

  - Training means creating or learning the model. You show the model labeled examples and enable the model to gradually learn the relationships between features and label.
  - Inference means applying the trained model to unlabeled examples. You use the trained model to make useful predictions (y). For example, during inference, you can predict medianHouseValue for new unlabeled examples.

- Regression vs. classification:

  - A regression model predicts continuous values. Regression models make predictions that answer questions like the following:

    - What is the value of a house in California?
    - What is the probability that a user will click on this ad?

  - A classification model predicts discrete values. Classification models make predictions that answer questions like the following:

    - Is a given email message spam or not spam?
    - Is this an image of a dog, a cat, or a hamster?

- Suppose you want to develop a supervised machine learning model to predict whether a given email is "spam" or "not spam.". Which of the following statements are true?

  - [x] Emails not marked as "spam" or "not spam" are unlabeled examples: Because our label consists of the values "spam" and "not spam", any email not yet marked as spam or not spam is an unlabeled example
  - [x] The labels applied to some examples might be unreliable: It's important to check how reliable your data is. The labels for this dataset probably come from email users who mark particular email messages as spam. Since most users do not mark every suspicious email message as spam, we may have trouble knowing whether an email is spam. Furthermore, spammers could intentionally poison our model by providing faulty labels
  - [ ] Words in the subject header will make good labels: Words in the subject header might make excellent features, but they won't make good labels.
  - [ ] We'll use unlabeled examples to train the model: We'll use labeled examples to train the model. We can then run the trained model against unlabeled examples to infer whether the unlabeled email messages are spam or not spam.

- Suppose an online shoe store wants to create a supervised ML model that will provide personalized shoe recommendations to users. That is, the model will recommend certain pairs of shoes to Marty and different pairs of shoes to Janet. Which of the following statements are true?
  - [x] Shoe size is a useful feature: Shoe size is a quantifiable signal that likely has a strong impact on whether the user will like the recommended shoes. For example, if Marty wears size 9, the model shouldn't recommend size 7 shoes
  - [x] User clicks on a shoe's description is a useful label: Users probably only want to read more about those shoes that they like. User clicks is, therefore, an observable, quantifiable metric that could serve as a good training label.
  - [ ] The shoes that a user adores is a useful label: Adoration is not an observable, quantifiable metric. The best we can do is search for observable proxy metrics for adoration.
  - [ ] Shoe beauty is a useful feature: Good features are concrete and quantifiable. Beauty is too vague a concept to serve as a useful feature. Beauty is probably a blend of certain concrete features, such as style and color. Style and color would each be better features than beauty.

## Descending into ML

## Reducing Loss

## First Steps with TF

## Generalization

## Training and Test Sets

## Validation

## Representation

## Feature Crosses

## Regularization: Simplicity

## Logistic Regression

## Classification

## Regularization: Sparsity

## Introduction to Neural Nets

## Training Neural Nets

## Multi-Class Neural Nets

## Embeddings
