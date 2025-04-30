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

## Another way of doing this

With the goal of making our algorithm more efficient, we can address the main issue: we look through the entire string for every different $k$-mer pattern. Our new idea is to pass through the string once for each $k$, maintaining a count of each possible $k$-mer and adding to each $k$-mer's count whenever we pass over it. Since these strings are made up of four different possible characters, we will have $4^k$ possible $k$-mers for each value of $k$.

We define the frequency array of a string $Text$ as an array of length $4^k$, where the $i$-th element of the array holds the number of times that the $i$-th $k$-mer (in the lexographic order) appears in $Text$.

To make this work we need to be able to transform strings to integers and back to strings. We can figure out the possible $k$-mers, order them lexographically, then number them based on that ordering. Based on that numbering we can encode our string as an integer, where each $k$-mer is described by its number in the lexographic ordering.

The following algorithms are for encoding and decoding out representations:

**Encoding**:

```python
def pattern_to_number(pattern):
    if not pattern:
        return 0
    symbol_to_number = {'A': 0, 'C': 1, 'G': 2, 'T': 3}
    result = 0
    for char in pattern:
        result = result * 4 + symbol_to_number[char]
    return result
```

**Decoding**:

```python
def number_to_pattern(index, k):
    if k == 0:
        return ""
    number_to_symbol = {0: 'A', 1: 'C', 2: 'G', 3: 'T'}
    prefix_index = index // 4
    remainder = index % 4
    symbol = number_to_symbol[remainder]
    if k == 1:
        return symbol
    else:
        prefix_pattern = number_to_pattern(prefix_index, k-1)
        return prefix_pattern + symbol
```

We can now move on to the problem of generating frequency arrays. We can first initialize every $4^k$ elements in the frequency array to zero, then make a single pass down the string. For each $k$-mer we encounter, we add 1 to the value of the frequency array corresponding to it.

If working in Python we can use a dict for our frequency array:

```python
def frequency_array(k):
    frequencies = {}
    for i in range(0, (4**k)):
        frequencies[number_to_pattern(i, k)] = 0
    return frequencies
```

This uses our previously built `number_to_pattern` function to populate our dictionary with keys corresponding to each possible $k$-mer, in lexicographical order.

We can now put it all together with a complete algorithm that is faster than our original solution:

```python
def faster_frequent_words(text, k):
    frequencies = frequency_array(k)
    for i in range(len(text) - k + 1):
        frequencies[text[i:i+k]] += 1
    max_value = max(frequencies.values())
    print(frequencies)
    return [key for key, value in frequencies.items() if value == max_value]
```

This algorithm initializes a dict of all possible $k$-mers. It then iterates through $Text$ and adds each $k$-mer occurrence to the frequency dict. We then get the maximum value of the frequency dict, and iterate through the frequency dict to check for strings that match that maximum value. Strings that have occurrences equal to the max are returned.

## How do you compute number to pattern?

They use a recursive algorithm.

We observe that if we remove the final symbol from all lexicographically ordered $k$-mers, the resulting list is still ordered lexicographically.

We also see that once we do this, every ($k$-1)-mer in the resulting list is repeated four times.

So, in the case of $3$-mers and the pattern of $AGT$ we see that

$PatternToNumber(AGT) = 4 \cdot PatternToNumber(AG) + SymbolToNumber(T) \\
 = 8 + 3 = 1$

Where $SymbolToNumber(symbol)$ is the function transforming symbols $A, C, G, T$ into their respective integers 0, 1, 2, and 3.

By removing the final symbol of $Pattern$, denotes $LastSymbol(Pattern)$, we obtain a $(k-1)$-mer that we denote as $Prefix(Pattern)$.

We can generalize this observation to the following formula:

$
PatternToNumber(Pattern) = 4 \cdot PatternToNumber(Prefix(Pattern)) + SymbolToNumber(LastSymbol(Pattern))
$

So we can construct the following recursive algorithm:

```python
def pattern_to_number(pattern):
    if not pattern:
        return 0
    symbol = pattern[-1]
    prefix = pattern[:-1]
    return 4 * pattern_to_number(prefix) + symbol_to_number(symbol)
```

## References

Compeau, P., & Pevzner, P. (2015). *Bioinformatics algorithms: An active learning approach* (Vol. 1). Active Learning Publishers.