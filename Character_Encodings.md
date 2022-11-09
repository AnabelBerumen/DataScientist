## Character Encodings



UTF-8 is the standard text encoding, strings are UTF-8 by default in Python 3.
```python
# start with a string
before = "This is the euro symbol: €"

# check to see what datatype it is
type(before)
>>> str
```
## 
##### bytes([source[, encoding[, errors]]]) 
> Return a new “bytes” object, which is an immutable sequence of integers in the range 0 <= x < 256.
The other data is the bytes data type, which is a sequence of integers. You can convert a string into bytes by specifying which encoding it's in:
```python
# encode it to a different encoding, replacing characters that raise errors
after = before.encode("utf-8", errors="replace")

# check the type
type(after)
>>> bytes

after
>>> b'This is the euro symbol: \xe2\x82\xac'
```
##
```python
# convert it back to utf-8
print(after.decode("utf-8"))
>>> This is the euro symbol: €
```
```python
# Receta para encontrar el encoding
# look at the first ten thousand bytes to guess the character encoding
with open("../input/kickstarter-projects/ks-projects-201801.csv", 'rb') as rawdata:
    result = chardet.detect(rawdata.read(10000))

# check what the character encoding might be
print(result)
>>> {'encoding': 'Windows-1252', 'confidence': 0.73, 'language': ''}
```
```
# open() parameters

"r" - Read - Default value. Opens a file for reading, error if the file does not exist

"a" - Append - Opens a file for appending, creates the file if it does not exist

"w" - Write - Opens a file for writing, creates the file if it does not exist

"x" - Create - Creates the specified file, returns an error if the file exist

In addition you can specify if the file should be handled as binary or text mode

"t" - Text - Default value. Text mode

"b" - Binary - Binary mode (e.g. images)
```

```python
# save our file (will be saved as UTF-8 by default!)
kickstarter_2016.to_csv("ks-projects-201801-utf8.csv")
```
## 
```python
# Example
sample_entry = b'\xa7A\xa6n'
print(sample_entry)
print('data type:', type(sample_entry))

>>> b'\xa7A\xa6n'
>>> data type: <class 'bytes'>

before = sample_entry.decode("big5-tw")
new_entry = before.encode()
```

```python
# TODO: Load in the DataFrame correctly.
with open("../input/fatal-police-shootings-in-the-us/PoliceKillingsUS.csv",'rb') as rawdata:
    result = chardet.detect(rawdata.read(20000))
    
police_killings = pd.read_csv("../input/fatal-police-shootings-in-the-us/PoliceKillingsUS.csv", encoding= result.get('encoding'))
```
