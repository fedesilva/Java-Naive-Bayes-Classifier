Java Naive Bayes Classifier
==================

Nothing special. It works and is well documented, so you should get it running without wasting too much time searching for other alternatives on the net.

Example
------------------

Here is an excerpt from the example. The classifier will classify sentences (arrays of features) as sentences with either positive or negative sentiment. Please refer to the full example for a more detailed documentation.

```java
// Create a new bayes classifier with string categories and string features.
Classifier<String, String> bayes = new BayesClassifier<String, String>();

// Two examples to learn from.
String[] positiveText = "I love sunny days".split("\\s");
String[] negativeText = "I hate rain".split("\\s");

// Learn by classifying examples.
// New categories can be added on the fly, when they are first used.
// A classification consists of a category and a list of features
// that resulted in the classification in that category.
bayes.learn("positive", Arrays.asList(positiveText));
bayes.learn("negative", Arrays.asList(negativeText));

// Here are two unknown sentences to classify.
String[] unknownText1 = "today is a sunny day".split("\\s");
String[] unknownText2 = "there will be rain".split("\\s");

System.out.println( // will output "positive"
    bayes.classify(Arrays.asList(unknownText1)).getCategory());
System.out.println( // will output "negative"
    bayes.classify(Arrays.asList(unknownText2)).getCategory());

// Get more detailed classification result.
((BayesClassifier<String, String>) bayes).classifyDetailed(
    Arrays.asList(unknownText1));

// Change the memory capacity. New learned classifications (using
// learn method are stored in a queue with the size given here and
// used to classify unknown sentences.
bayes.setMemoryCapacity(500);
```

Forgetful learning
------------------

This classifier is forgetful. This means, that the classifier will forget recent classifications it uses for future classifications after - defaulting to 200 - classifications learned.
This will ensure, that the classifier can react to ongoing changes in the user's habbits.

Possible Performance issues
------------------

Performance improvements, I am currently thinking of:

- Store the natural logarithms of the feature probabilities and add them together instead of multiplying the probability numbers

The MIT License (MIT)
------------------

Copyright (c) 2012 Philipp Nolte

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
