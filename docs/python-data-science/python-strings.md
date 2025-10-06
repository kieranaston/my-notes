# Working with strings in Python

## Regular expressions

```python
import re

regex_split = re.split(r'\+', "2 + x + x^2")
# This splits the string on the '+' character

# The following regex matches one or more digits
pattern = r'\d+'
text = "There are 2 apples and 13 oranges"
matches = re.findall(pattern, text)

# Replacement
placement = re.sub(r'apples', 'bananas', text)
```

Regex is difficult to remember so best used as you go, looking online for resources depending on what you want to do.