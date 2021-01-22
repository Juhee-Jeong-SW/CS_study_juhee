# 해시 테이블 구현

## 📌 **Hash Table 구현하기**

### 해시 테이블(Hash Table)

![https://blog.kakaocdn.net/dn/cXbBbC/btqBJfAGTn1/DT8PRbSzy7e9Ky6oijoz0K/img.png](https://blog.kakaocdn.net/dn/cXbBbC/btqBJfAGTn1/DT8PRbSzy7e9Ky6oijoz0K/img.png)

해쉬 테이블은 `키와 밸류를 기반으로 데이터를 저장`한다. 파이썬에서는 딕셔너리가 있어서 굳이 만들 필요는 없는데, 아무래도 파이썬으로 코드를 짜면 간단해서 파악하기가 쉽다는 장점이 있다.

위 이미지에서 문자열(John smith...) 데이터는 해쉬 함수를 거쳐 숫자로 변경된다. 변경된 이 값(해시)를 배열(buckets)의 키로 삼아 밸류를 저장한다. 따라서 데이터를 서칭하는 과정에서 배열을 순차적으로 탐색할 필요없이 **해시 함수를 거쳐 생성된 해시 값으로 데이터를 빠르게 찾을 수 있다**. 딕셔너리의 key-value 구조와 유사하다.

- **키(Key): 인풋 데이터 ***ex) John Smith, Lisa Smith

- **값(value): 저장할 데이터** *ex) 521-8976, 521-1234

- **해쉬 함수(Hash Function): '키'를 해시로 변경해주는 함수**

  - ****위 이미지에서 문자열 데이터가 hash function을 거쳐 숫자열 데이터로 변경된다.

    ex) John Smaith -> 02

- **해시(Hash): 인풋 데이터를 고정된 길이의 숫자열로 변환한 결과물 ***위 이미지에서 00~15가 해시다.

즉 문자열로 들어온 인풋 데이터를 해시 함수를 통해 숫자열로 변경해주고, 이 숫자를 키 값 삼아서 배열(buckets)에 값을 저장하는 구조다. (파이썬 해쉬 함수의 경우 환경마다 아웃풋이 달라서 hashlib의 sha1, sha256을 쓰기도 함)

### 해시 테이블 구현

```python
# Hash Table
class HashTable:
    def __init__(self, table_size):
        self.size = table_size
        self.hash_table = [0 for a in range(self.size)]
        
    def getKey(self, data):
        self.key = ord(data[0])
        return self.key
    
    def hashFunction(self, key):
        return key % self.size

    def getAddress(self, key):
        myKey = self.getKey(key)
        hash_address = self.hashFunction(myKey)
        return hash_address
    
    def save(self, key, value):
        hash_address = self.getAddress(key)
        self.hash_table[hash_address] = value
        
    def read(self, key):
        hash_address = self.getAddress(key)
        return self.hash_table[hash_address]
    
    def delete(self, key):
        hash_address = self.getAddress(key)
        
        if self.hash_table[hash_address] != 0:
            self.hash_table[hash_address] = 0
            return True
        else:
            return False

#Test Code
h_table = HashTable(8)
h_table.save('a', '1111')
h_table.save('b', '3333')
h_table.save('c', '5555')
h_table.save('d', '8888')
print(h_table.hash_table)
print(h_table.read('d'))

h_table.delete('d')

print(h_table.hash_table)
```