# Poker_hand_predictor

Gambling! What's your first thought when you hear that word. Black-jack? Roulette? Or even those arcade machines to get the stuffed animals. When I think of gambling, I think of poker. Poker is a big deal!

> Millions of Americans spend as estimated $6 billion annually on it, according to the [National Bureau of Economic Research](https://www.nber.org/system/files/working_papers/w17023/w17023.pdf).

Given its widespread influence, I decided to make a model, focusing in on making a machine learning algorithm that would identify the best 5-card hand on a table (pair, 3 of a kind, flush, straight). While I could achieve this with a simple algorithm, I thought it would the perfect project to employ a **decision tree model**.

> [IBM](https://www.ibm.com/think/topics/decision-trees) defines a decision tree as a "non-parametric supervised learning algorithm, which is utilized for both classification and regression tasks. It has a hierarchical, tree structure, which consists of a root node, branches, internal nodes and leaf nodes."

***

## Data Acquisition

The poker hand .data files were acquired from UCI's [machine learning repository](https://archive.ics.uci.edu/dataset/158/poker+hand). The page my data came from, Poker Hand, has 10 features (the suite and card # as separate features for 5 cards). The predicted target variable is the CLASS of the hand, which is basically the name of the best hand.

Feature and Target variable breakdown from the Poker Hand dataset.

1) S1 "Suit of card #1"
    Ordinal (1-4) representing {Hearts, Spades, Diamonds, Clubs}

2) C1 "Rank of card #1"
    Numerical (1-13) representing (Ace, 2, 3, ... , Queen, King)

3) S2 "Suit of card #2"
    Ordinal (1-4) representing {Hearts, Spades, Diamonds, Clubs}

4) C2 "Rank of card #2"
    Numerical (1-13) representing (Ace, 2, 3, ... , Queen, King)

5) S3 "Suit of card #3"
    Ordinal (1-4) representing {Hearts, Spades, Diamonds, Clubs}

6) C3 "Rank of card #3"
    Numerical (1-13) representing (Ace, 2, 3, ... , Queen, King)

7) S4 "Suit of card #4"
    Ordinal (1-4) representing {Hearts, Spades, Diamonds, Clubs}

8) C4 "Rank of card #4"
    Numerical (1-13) representing (Ace, 2, 3, ... , Queen, King)

9) S5 "Suit of card #5"
    Ordinal (1-4) representing {Hearts, Spades, Diamonds, Clubs}

10) C5 "Rank of card 5"
    Numerical (1-13) representing (Ace, 2, 3, ... , Queen, King)

11) CLASS "Poker Hand"
    Ordinal (0-9)

    0: Nothing in hand; not a recognized poker hand 
    1: One pair; one pair of equal ranks within five cards
    2: Two pairs; two pairs of equal ranks within five cards
    3: Three of a kind; three equal ranks within five cards
    4: Straight; five cards, sequentially ranked with no gaps
    5: Flush; five cards with the same suit
    6: Full house; pair + different rank three of a kind
    7: Four of a kind; four equal ranks within five cards
    8: Straight flush; straight + flush
    9: Royal flush; {Ace, King, Queen, Jack, Ten} + flush

The training-true data file contained approximately 25,000 datapoints of the 5 cards suite and #. The testing data has 1m+ datapoints. This leads me to suspect that they misnamed the datafiles, so I used the training data as testing data and the testing data for training data, swapping them.

## Data processing and parsing

When creating my Decision Tree model, I decided to *alter* the standard features to better fit my choice of model. 

When classifying hands, it is important to know whether or not **suites** of cards match. So, I created 10 Boolean variables (S1==S2, S2==S5, etc.) that are true or false depending on whether the suites of respective cards match. Consequently, I removed the suite features as they were now unnecessary for classifying a hand. 

> Despite this, my model was still relatively inaccurate, getting stuck at a low 60% accuracy.

Next, I created a similar Boolean matching system, but for the cards (C1==C2, C1=C3, etc.) to aid the models classification.

> I *didn't* get rid of the card feature since it would still be necessary for classification.

Below is the short python script I used to parse and manipulate the original dataset.

![Parsing script](https://github.com/aadhavjawahar-sys/Poker_hand_predictor/blob/main/images/DecisionTree_1.png)

The datafile looks like...

![Data File Here](https://github.com/aadhavjawahar-sys/Poker_hand_predictor/blob/main/images/DecisionTree_2.png)

***

## Model Accuracy

Going through testing, the model has deplorable accuracy, being at about 0-66% in the first two stages. But, in stage 3, after implementing the Boolean variable features in place of the original suite and card features alone, the accuracy jumped to perfect or near perfect. Below shows the [confusion matrix](https://towardsdatascience.com/performance-metrics-confusion-matrix-precision-recall-and-f1-score-a8fe076a2262/) and accuracy of the model, along with its precision and handle.

> **Precision**: Out of all the positive predicted, what percentage is truly positive.
> **Recall**: Out of the total positive, what percentage are predicted positive.

![Accuracy Description](https://github.com/aadhavjawahar-sys/Poker_hand_predictor/blob/main/images/DecisionTree_3.png)

>> I was able to get similar accuracy with 1/10 of the training data (100,000 datapoints), showing the quick learning and efficiency of the model

***

## Demonstration of Working Model

In order to interact with my model, I built a simple graphical user interface system. Initially, the user sees this page with several input boxes, asking for both the suite and card # classification.

![Input Boxes](https://github.com/aadhavjawahar-sys/Poker_hand_predictor/blob/main/images/DecisionTree_4.png)

After selecting the desired classifications, hit the ***submit*** button.

![Submit](https://github.com/aadhavjawahar-sys/Poker_hand_predictor/blob/main/images/DecisionTree_5.png)

Finally, take a look at the predicted hand section on the gradio page.

![Answer?](https://github.com/aadhavjawahar-sys/Poker_hand_predictor/blob/main/images/DecisionTree_6.png)

***

## Future Direction

IF I have more time to work on developing this model, I would likely tidy up the GUI, making it so you can choose to add cards. If I can attain more datasets featuring the best hands with fewer cards, I would like to add that to the model. My hope is that people new to poker would be able to experiment with diversifying their hands and better learning the classifications of each hand. Thanks for reading!
