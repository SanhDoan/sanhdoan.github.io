---
title: Bloom filter
author: Sanh Doan
date: 2023-05-13 17:45:00 +0700
categories: [Data structure]
tags: []
---

Tiếng Việt phía dưới (Vietnamese below)

## English
- Bloom filter is a data structure used to check for the existence of an element in a set
- It uses a bit array to mark the elements that have been added.
- When an element is added to the bloom filter, it is passed through a number of hash functions to create a bit string, each bit in this sequence is placed in the corresponding bit array.
- When checking if an element belongs to the set, the bloom filter will re-apply the hash functions on that element and check the corresponding positions in the bit array. If all positions are marked, the bloom filter will return "element that may belong to the set", but if at least one position is unmarked, the bloom filter will return "element not available". belonging to the set".
- Bloom filter allows to check the existence of an element with linear time complexity, but can give false positive results.
- Bloom filter cannot remove an element that has already been added, so if an element is marked with an error it will never be repaired.
### Formula
```
size = -(n * ln(p)) / (ln(2)^2)
```
- n: number of element need to be stored.
- p: allowable error rate (false positive rate). For example, if you wanted to limit the margin of error to 1%, p would be 0.01.

```
numHashFunctions = (size / n) * ln(2)
```

## Vietnamese
- Bloom filter là một cấu trúc dữ liệu được sử dụng để kiểm tra sự tồn tại của một phần tử trong một tập hợp
- Nó sử dụng một mảng bit để đánh dấu các phần tử đã được thêm vào.
- Khi một phần tử được thêm vào bloom filter, nó được đưa qua một số hàm băm để tạo ra một chuỗi bit, mỗi bit trong chuỗi này được đặt vị trí trong mảng bit tương ứng.
- Khi kiểm tra xem một phần tử có thuộc tập hợp hay không, bloom filter sẽ áp dụng lại các hàm băm lên phần tử đó và kiểm tra các vị trí tương ứng trong mảng bit. Nếu tất cả các vị trí đều đã được đánh dấu, bloom filter sẽ cho kết quả "phần tử có thể thuộc tập hợp", nhưng nếu ít nhất một vị trí chưa được đánh dấu, bloom filter sẽ cho kết quả "phần tử không thuộc tập hợp".
- Bloom filter cho phép kiểm tra sự tồn tại của một phần tử với độ phức tạp thời gian tuyến tính, nhưng có thể cho ra kết quả sai dương.
- Bloom filter không thể xóa một phần tử đã được thêm vào, vì vậy nếu một phần tử được đánh dấu bằng lỗi thì nó sẽ không bao giờ được sửa chữa.
### Công thức tính kích thước mảng và số hàm băm
```
size = -(n * ln(p)) / (ln(2)^2)
```
- n: số lượng phần tử cần lưu trữ.
- p: giới hạn cho phép sai sót (false positive rate). Ví dụ: nếu bạn muốn giới hạn cho phép sai sót là 1%, p sẽ bằng 0.01.

```
numHashFunctions = (size / n) * ln(2)
```

## Sample implementation
```go
package main

import (
    "fmt"
    "hash/fnv"
)

type BloomFilter struct {
    bitArray []bool
    numHashFunctions int
}

func NewBloomFilter(size int, numHashFunctions int) *BloomFilter {
    return &BloomFilter{
        bitArray: make([]bool, size),
        numHashFunctions: numHashFunctions,
    }
}

func (bf *BloomFilter) Add(key string) {
    for i := 0; i < bf.numHashFunctions; i++ {
        h := fnv.New32()
        h.Write([]byte(key + string(i)))
        index := int(h.Sum32()) % len(bf.bitArray)
        bf.bitArray[index] = true
    }
}

func (bf *BloomFilter) Contains(key string) bool {
    for i := 0; i < bf.numHashFunctions; i++ {
        h := fnv.New32()
        h.Write([]byte(key + string(i)))
        index := int(h.Sum32()) % len(bf.bitArray)
        if !bf.bitArray[index] {
            return false
        }
    }
    return true
}

func main() {
    bf := NewBloomFilter(1000000, 10)
    bf.Add("apple")
    bf.Add("banana")
    bf.Add("orange")

    fmt.Println(bf.Contains("apple")) // true
    fmt.Println(bf.Contains("pear")) // false
    fmt.Println(bf.Contains("banana")) // true
}
```