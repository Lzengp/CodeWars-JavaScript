## [1.int32 to IPv4](https://www.codewars.com/kata/52e88b39ffb6ac53a400022e/train/javascript)
### 级别：5 kyu

## 题目
Take the following IPv4 address: 128.32.10.1

This address has 4 octets where each octet is a single byte (or 8 bits).

* 1st octet 128 has the binary representation: 10000000
* 2nd octet 32 has the binary representation: 00100000
* 3rd octet 10 has the binary representation: 00001010
* 4th octet 1 has the binary representation: 00000001

So **128.32.10.1 == 10000000.00100000.00001010.00000001**

Because the above IP address has 32 bits, we can represent it as the unsigned 32 bit number: 2149583361

Complete the function that takes an unsigned 32 bit number and returns a string representation of its IPv4 address.

Examples
```
2149583361 ==> "128.32.10.1"
32         ==> "0.0.0.32"
0          ==> "0.0.0.0"
```
## 思路
首先题目的意思是：输入的是一个十进制数据，转换成32位的二进制，然后按照8位分割，然后又把这个8位二进制的字符转换成十进制，中间通过 . 号隔离。
具体做法就是先把十进制的转换成二进制，然后前面补0，一定是32位字符串，这个是通过slice来完成的，拿到32位数之后就是按照8位数来分割，通过parseInt再把二进制转十进制

## 解题代码
```
function int32ToIp(int32){
    let s = '';
    for (let i = 0; i < 32; i++) {
      s += '0';
    }
    const r = (s + Number(int32).toString(2)).slice(-32);
    return `${parseInt(r.slice(0, 8), 2)}.${parseInt(r.slice(8, 16), 2)}.${parseInt(r.slice(16, 24), 2)}.${parseInt(r.slice(24, 32), 2)}`;
}
```

## 优解
```
function int32ToIp(int32){
    return (int32>>>24) + '.' + (int32<<8>>>24) + '.' + (int32<<16>>>24) + '.' + (int32<<24>>>24)
}
```
