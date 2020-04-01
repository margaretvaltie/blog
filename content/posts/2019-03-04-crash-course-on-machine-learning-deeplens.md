---
title: 'Crash Course on Machine Learning & DeepLens'
author: mvaltie
date: 2019-03-04T21:34:18+00:00
url: /2019/03/04/crash-course-on-machine-learning-deeplens/
categories:
  - AWS
  - AWS meetup
  - Chicago
tags:
  - AI
  - AWS
  - awschicago
  - Chicago
  - deep learning
  - machine learning

---
## My first presentation at the Chicago AWS user group &#8211; Deep Learning and Hotdogs

<img src="/wp-content/uploads/2019/03/IMG-1607-1024x768.jpg" alt="" class="wp-image-2263" /> <figcaption>Evidence I did more than talk about the user group!</figcaption></figure> 

Believe it not, last Thursday night was my first-ever presentation in front of the Chicago user group. I've been organizing the thing for more than 5 years now, but this was my first presentation beyond a "state of the user group" talk. I always had it in my head that I had to let others do all the presentations or else it would be un-authentic. Going to re:Invent and interacting with other user group leaders made me realize most of my peers are regular speakers. I'd better step up my game!

The first and most fitting topic for me was the DeepLens. Back in August 2018 AWS sent user group leaders a DeepLens and a generic deck to share with the group. I messed around with the DeepLens, forgot the root password, and put it on the shelf. The user group had some great content lined up in the Fall, plus there was re:Invent news, which would just overshadow anything else at the end of the year. 

Re:Invent news did overshadow the little DeepLens (hello, DeepRacer!) but I decided it was still a good excuse to present on a topics I wasn't familiar with at all &#8211; AI, Machine Learning and DeepLearning. <figure class="wp-block-image">

<img src="http://18.223.210.174/wp-content/uploads/2019/03/ML-stack-1024x572.png" alt="" class="wp-image-2264" /> <figcaption>AWS' Machine Learning Stack, with some * new additions from re:Invent</figcaption></figure> 

First up, putting all the services in context: the AWS Machine Learning stack. AWS offers 3 levels of Machine Learning services from very hands on to applied tools. At the bottom are the frameworks and interfaces for folks who really know what they're doing. They can use PyTorch on an EC2 instance, or since re:Invent they can now use the AWS TensorFlow AMI [(AMI has 3 syllables!!). ][1]

Moving on up to the platform layer, there is the 400 pound service, [SageMaker.][2] Amazon SageMaker is a managed service Machine Learning offering. An AWS SA described it as "end to end deep learning" &#8211; you can build, train, and deploy your learning models all within SageMaker. Plus, from my 15 minutes of poking around with Sagemaker Ground Truth I'm pretty pumped about the things it will do. SageMaker Ground Truth helps you build training datasets with Mechanical Turk! You can hone your datasets with real human input, which is the most laborious part of getting data whipped into shape for deep learning. <figure class="wp-block-image">

<img src="http://18.223.210.174/wp-content/uploads/2019/03/sagemakergroundtruth-1024x929.png" alt="" class="wp-image-2265" /> <figcaption>Setting up SageMaker Ground Truth to get some specific hotdog datasets!</figcaption></figure> 

At the top of the AWS service stack is the applied Machine Learning tools, like Polly for text to speech, plus the 3 more announced at re:Invent. Over to the side of the stack is our friend the DeepLens. It's a great idea for taking Machine Learning out into the world to get hands on with more use cases. 

## All deep learning is AI, but not all AI is deep learning

[One of the best posts out there][3] describes Artificial Intelligence (AI) as a Russian doll: Deep learning is a subset of machine learning, which is a subset of AI. Or Deep learning is part of AI in the same way that all squares are rectangles but not all rectangles are squares.

Artificial intelligence can be simplified to computers simulating human intelligence. AI can include everything from visual recognition, decisions, translations, and pattern detection. Within AI, is Machine Learning (ML), which uses patterns to make predictions without as many sets of rules. Computers used to need a lot of programming to give us outputs, but as data sets grew and we can easily use higher CPUs we can "train" computers to recognize patterns and make predictions. 

And the little doll inside is Deep Learning. It's "deep" because the machine learning model goes through multiple layers or repetitions of training. Our data or input goes through layers and layers, or "epochs" of Machine Learning to find patterns. Running models through so many trainings mimics a neural network, like human brains, to link patterns and make connections. DeepRacer suddenly made sense to me once I learned that! I just image the little thing going around and around the track and learning as it goes. 

## Data is the air that lets Deep Learning breathe

There are 3 key parts of deep learning: 

  1. Large Data sets
  2. Model training
  3. Inferences (aka predictions)

Data! Large data sets are so important to deep learning and all the way up the doll stack. Not just any data, though. First, data must be Annotated. Annotation is just labeling data: "this is a picture of a hotdog, this is not a picture of a hotdog." Next, Preprocess, or make data uniform. We have to get all our little hotdog images the same dimensions, same light conditions, and so on. Finally, we'll split data set into 2 sets: 

  *  “training” set &#8211; for learning over and over 
  * “testing” set of similar but new data

#### Model training with DeepLens

DeepLens, our portable(ish) little smart camera relies on SageMaker for projects. A project requires a Lambda function and model. For the model you can build or borrow. There's a [great Community area for DeepLens projects][4] out there. To get the DeepLens making predictions, you have to deploy the model onto the DeepLens to run "training data” live against the model inside DeepLens. 

DeepLens has GreenGrass and Lambda natively running, and the lambda checks new input with model to validate. Together, the model and the lambda function can make simple inference (aka predictions) from DeepLens input. Take a look at that hotdog through a DeepLens and it knows it's a hotdog, live on your Project Output Stream. 

On the DeepLens, Lambda does 3 things

  1. Collects the input
  2. Runs data against deep learning model
  3. Displays output 
      * Device stream = live stream of video
      * Project stream = deep learning
      <figure class="wp-block-image">

<img src="http://18.223.210.174/wp-content/uploads/2019/03/deeplens-hotdogs-1024x525.png" alt="" class="wp-image-2266" /> <figcaption>DeepLens hotdog detection workflow</figcaption></figure> 

## Interacting with other AWS services

First up, there are Lambda running around throughout DeepLens. There are function that collect video input, run input agaist the model locally, and functions that send the output to the two streams. 

Depending on where you send that output, you can use more Lambda functions to send output back to AWS via Kenesis or IoT Gateway, Amazon Rekognition, S3 storage, DynamoDB, and more. 

And on the front end of DeepLens, don't forget SageMaker. Using SageMaker you can build data sets, edit models and train models. Plus with SageMaker Ground Truth you can annotate and create new data sets, like Chicago hotdogs vs regular hotdogs. Nobody steal that idea before I get around to it!<figure class="wp-block-image">

<img src="http://18.223.210.174/wp-content/uploads/2019/03/aws-deeplens-journey-1024x561.png" alt="" class="wp-image-2267" /> <figcaption>A hotdog's journey through a DeepLens</figcaption></figure> 

## Chicago ugroup library

Yes, there are cool projects online and everyone could buy their own DeepLens but I propose we have a library card checkout system with the DeepLens. I'm inviting any Chicago AWS user group member to check out this DeepLens and do cool stuff. Just tell me what you want to do, how long you'll work on it, and then check it back in so others can do cool stuff too.

 [1]: https://twitter.com/QuinnyPig/status/1098511266002264066?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1098512429158486016&ref_url=https%3A%2F%2Ftechnodrone.blogspot.com%2F2019%2F03%2Fami-has-3-syllables-ami-aws.html
 [2]: https://aws.amazon.com/sagemaker/
 [3]: https://skymind.ai/wiki/ai-vs-machine-learning-vs-deep-learning
 [4]: https://aws.amazon.com/deeplens/community-projects/