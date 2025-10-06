# Reading data

## CSV

`df_csv = pd.read_csv('file_name.csv')`

## Excel

`df_excel = pd.read_excel('file_name.xlsx', sheet_name=0)`

## Fixed width

`df_fwf = pd.read_fwf('file_name.txt', widths=[12, 7, 3, 5])`

## XML (local)

```python
import xml.etree.ElementTree as ET

def parse_xml(path):
    tree = ET.parse(p)
    root = tree.getroot()
    return pd.DataFrame([{el.tag: el.text for el in row} for row in root])
```

`df_xml = parse_xml('file_name.xml')`

## XML (remote)

```python
from bs4 import BeautifulSoup

xml_url = "https://www.w3schools.com/xml/cd_catalog.xml"
soup = BeautifulSoup(requests.get(xml_url).content, 'xml')
cd_list = [{tag.name: tag.text for tag in cd.find_all()} for cd in soup.find_all("CD")]
df_cd = pd.DataFrame(cd_list)
```

## JSON

```python
import json

with open('./input/data.json') as f:
     data_json = json.load(f)
     df_json = pd.DataFrame(data_json)
```

## Checking what the data looks like

`print('Column names:', df_csv.columns.tolist())`

`print('Types:', df_csv.dtypes)`

`print('Shape:', df_csv.shape)`

`print('First 5 rows:', df_csv.head(5))`