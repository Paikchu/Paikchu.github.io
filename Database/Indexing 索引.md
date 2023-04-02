##### Types of Index
+ Hash Tables
  + Hashing
  + Good fror equality selections
  + Cannot support range searches
+ B+ Trees
  + Built on sorted data
  + Good for range queries

## B+ Tree Index
[[B+ Tree Indexing]]


## Hash Index
Hash-based indexed are best for equality selections. ==Cannot support range searches.==

#### 静态哈希
可能存在很长的overflow链。
[[Static Hashing]]

#### 可扩展哈希
避免了overflow，使用一个directory保持对每个数据块的track，在填满时，对于directory进行翻倍。
由于数据分布不均匀(shewed data)，可能导致占用很多空间，进而导致更多的I/O
[[Extensible Hash Tables]]

#### Linear Hashing
不需要使用directory，允许overflow的存在，但overflow不会太长，空间的利用率可能比可扩展哈希要低，因为不一定会处理存在overflow的数据块。
[[Linear Hashing]]





