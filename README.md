# Poker_hand_predictor

Gambling! What's your first thought when you hear that word. Black-jack? Roulette? Or even those arcade machines to get the stuffed animals. When I think of gambling, I think of poker. Poker is a big deal!

> Millions of Americans spend as estimated $6 billion annually on it, according to the [National Bureau of Economic Research](https://www.nber.org/system/files/working_papers/w17023/w17023.pdf).

Given its widespread influence, I decided to make a model, focusing in on making a machine learning algorithm that would identify the best 5-card hand on a table (pair, 3 of a kind, flush, straight). While I could achieve this with a simple algorithm, I thought it would the perfect project to employ a **decision tree model**.

> [IBM](https://www.ibm.com/think/topics/decision-trees) defines a decision tree as a "non-parametric supervised learning algorithm, which is utilized for both classification and regression tasks. It has a hierarchical, tree structure, which consists of a root node, branches, internal nodes and leaf nodes."

***

## Data Processing

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

***

## Model Accuracy


Also show that you tried 100,000 elements and it still worked with good accuracy (1/10 of original data)
