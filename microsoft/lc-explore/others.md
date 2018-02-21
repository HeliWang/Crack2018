# Best Time to Buy and Sell

# 

# Minimum Path Sum

# 

# Word Break

# 

# Sentence Screen Fitting

Given a`rows x cols`screen and a sentence represented by a list of**non-empty**words, find**how many times**the given sentence can be fitted on the screen.

**Note:**

1. A word cannot be split into two lines.
2. The order of words in the sentence must remain unchanged.
3. Two consecutive words
   **in a line**
   must be separated by a single space.
4. Total words in the sentence won't exceed 100.
5. Length of each word is greater than 0 and won't exceed 10.
6. 1 ≤ rows, cols ≤ 20,000.

Idea:

![](/assets/Screen Shot 2018-02-20 at 9.35.41 PM.png)

Solution:

```cpp
int wordsTyping(vector<string>& sentence, int rows, int cols) {
    string newSentence;
    for (auto word: sentence) newSentence += word + " ";
    int len = newSentence.length();
    int start = 0;
    for (int i = 0; i < rows; i++) {
        start += cols;
        if (newSentence[start % len] == ' ') start++;
        else {
            while (start > 0 && newSentence[(start - 1) % len] != ' ') start--;
        }
    }
    return start / len;
}
```



