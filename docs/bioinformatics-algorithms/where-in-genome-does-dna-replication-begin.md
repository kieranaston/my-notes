# Where in the genome does DNA replication begin?

Replication begind in a genomic region called the replication origin (denoted $oriC$).

In the context of gene therapy it is important to figure out where the $oriC$ is within the genome so that it can be preserved. This is because it is necessary for gene replication, which is an important part of gene therapy.

Research has shown that the region of the bacterial genome encoding $oriC$ is typically a few hundred nucleotides long.

### Finding the $oriC$

One way we can try to find the $oriC$ is by looking for the $DnaA$ box, a DNA sequence that is essentially a message telling the $DnaA$ protein: "bind here!"

We want to look for something that stands out in $oriC$, in other words, some sort of pattern.

One way we can define this problem is as a pattern counting problem, where we search for the most frequent $k$-mers, or, strings of length $k$.

We can use the following algorithm:

```python
def pattern_count(text, pattern):
    count = 0
    for i in range(0, len(text)-len(pattern)):
        if text[i:(i+len(pattern))] == pattern:
            count += 1
    return count
```

### The Frequent Words problem

Let us extend this further. We can generalize to wanting to find the most frequent $k$-mer for all values of $k$ possible for the text.

We say that $Pattern$ is a most frequent $k$-mer in $Text$ if it mazimizes `pattern_count(text, pattern)` among all $k$-mers.

So our problem is as follows:

**Input**: A string $Text$ and an integer $k$

**Output**: All most frequent $k$-mers in $Text$

There will be $|Text|-k+1$ $k$-mers to check in a given string $Text$.

To implement this algorithm `frequent_words` we need to store an array `count` containing the number of occurrences of each pattern $Pattern = Text(i,k)$, where `count[i]` stores `count(text, pattern)` for $Pattern = Text(i,k)$. So if we have a pattern of length 3, `count[2]` would be the number of occurrences of the substring from index 2 to index (2 + 3) - 1 = 4.

Here is the algorithm:

```python
def frequent_words(text, k):
    count = []
    frequent_patterns = []
    max_count = 0
    for i in range(0, len(text)-k):
        pattern = text[i:(i+k)]
        count.append(pattern_count(text, pattern))
        if count[i] > max_count:
            max_count = count[i]
    for i in range(0, len(text)-k):
        if count[i] == max_count:
            frequent_patterns.append(text[i:(i+k)])
    frequent_patterns = list(dict.fromkeys(frequent_patterns))
    return frequent_patterns
```

This works, but it is not very efficient.

Each $k$-mer requires $|Text| - k + 1$ checks, each requiring as many as $k$ comparisons, so overall # of steps of `pattern_count(text, pattern)` is $(|Text| - k + 1) \cdot k$.

Additionally, `frequent_words` must call `pattern_count` $|Text| - k + 1$ times (once for each $k$-mer of $Text$), so its overall number of steps is $(|Text| - k + 1) \cdot (|Text| - k + 1) \cdot k$.

To simplify, its complexity is $\mathcal{O}(|Text|^2\cdot k)$.

## References

Compeau, P., & Pevzner, P. (2015). *Bioinformatics algorithms: An active learning approach* (Vol. 1). Active Learning Publishers.