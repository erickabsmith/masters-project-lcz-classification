Random Forest Tutorial Videos
================

## Statquest: Random Forests Part 1 - Building, Using, and Evaluating

[Video Link](https://www.youtube.com/watch?v=J4Wdy0Wc_xQ)

-   rfs are built out of decision trees. Decision trees aren’t very
    accurate though, they aren’t flexible with classifying new samples.
-   rfs have this flexibility, but keep some of the simplicity of a
    decision tree

Make one:

1.  Create a bootstrapped dataset
2.  Create a decision tree using the bootstrapped dataset, but only use
    a random subset of variables at each step
    1.  He’s only using 2 variables at each step but there’s ways to
        determine the optimal number of variables to select at each
        step.
    2.  Root node, randomly select two variables as candidates. One of
        them will do the best job separating the samples, and it will
        become the root node.
    3.  Then consider a random subset of variables at each step until
        the tree is complete.
3.  End up with a bunch of trees. A random forest.
4.  Using it.
    1.  Get a new sample
    2.  run it down the first tree that was made and see what the
        prediction is for the variable of interest (i.e. yes to heart
        disease)
    3.  Do step 2 again. Keep score.
    4.  Do it for all the trees. Which option got the most votes? That’s
        our decision!

“**B**ootstrapping the data + using the **agg**regate to make a decision
is called **Bagging**”

Now how do we evaluate it?

Typically about 1/3 of the original data doesn’t end up in bootstrapped
dataset. This leftover data is called the **Out-Of-Bag Dataset**
(Statquest likes “Out-of-Boot Dataset” but that’s not the name)

We can evaluate by checking how well each tree does with the Out-of-Bag
Samples. The proportion of OOB samples that were incorrectly classified
is called the **Out-Of-Bag Error** and tells us about how accurate our
random forest is.

SO one of the main dials you can turn is the number of variables
randomly selected at each step. Typically you’d start with the square of
the total number of variables, and hover around that value to compare

## Statquest: Random Forests Part 2 - Missing data and clustering

[video link](https://www.youtube.com/watch?v=sQ870aTKqiM&t=0s)

Two types of missing data:

1. Missing in original dataset
    * Make an initial guess that might be bad, then refine it
    * Starts with same filling methods as decision tree
    * To refine, make a bunch of decision trees. When samples end up in the same 
    leaf, they are similar. Use this information to create a proximity matrix
    for the sample with missing data. The proximity values are used as weights to 
    re-predict the missing value via a weighted average. Then you do it again,
    6 or 7 times, until the missing values converge
    * _Note, 1-proximity values is distance. You can draw a heat map with distances, 
    and an MDS plot._
2. Missing in new sample
    * Create two copies of data, one with one value of predicted variable, one 
    with the other. 
    * Run these samples through all the trees in the forest. See how often it's
    correctly labeled. The option that is correctly labeled the most is the one
    that "wins" (is used to fill the missing point)
