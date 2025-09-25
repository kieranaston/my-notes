# Importing and cleaning data

## Some info on libraries

BeautifulSoup helps parse HTML and other markup languages like XML.

Reads a csv into a pandas dataframe.

Might be good idea to examine the names of the attributes, the types, etc. Because pandas guesses what typing to use for basic csv files without any metadata determining types.

So sometimes you might have to change the typing of some of the attributes.

Figure out how to see a preview of a cleaned dataframe on the same line in VScode after importing it. This must be a vscode things.

Markup files like XML or JSON can be viewed nicely in a browser because you can open and collapse branches of the tree.

Function for parsing XML:

```python
def parse_xml(path):
    tree = ET.parse(path)
    root = tree.get_root()
    return pd.DataFrame([{el.tag: el.text for el in row} for row in root])
```

Using BeautifulSoup to parse XML:

```python
soup = BeautifulSoup(requests.get(xml_url).content, 'xml')
```

Can use cross tabulation to see relationship between two different attributes in a dataframe.

SQL not case-sensitive.