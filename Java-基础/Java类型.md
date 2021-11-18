* [基本类型](#基本类型)
  * [float或者double怎么判断＝0?](#float或者double怎么判断0)
* [包装类型](#包装类型)
  * [包装类型的equals](#包装类型的equals)

# 基本类型
|  基本类型   | 大小  | 备注  |
|  ----  | ----  | --- |
| int  | 4字节 32位 | Java默认的整数类型 |
| short  |  2字节 16位 | --- |
| byte  | 1字节 8位 | --- |
| float  | 4字节 32位 | --- |
| double  | 8字节 64位 | Java默认的小数类型 |
| long  | 8字节 64位 | --- |
| boolean  | 1字节 |  true/false  |
| char  | 2字节 16位 | --- |

### float或者double怎么判断＝0?

- 一般而言用误差内比较float为1e-6，double为1e-15，即如果Math.abs(a)<1e-6即可认为=0
- 如果非常严格要求精度 BigDecimal

# 包装类型

|  包装类型   | 缓存  |
|  ----  | ----  | 
| Integer  | IntegerCache [-128,127] | 
| Short  |  ShortCache.cache [-128,127] | 
| Byte  | [-128, 127] | 
| Float  | 4字节 32位 | 
| Double  | 8字节 64位 |
| Long  | [-128, 127] |
| Boolean  | TRUE FALSE | 
| Character  | [0, 127] | 

## 包装类型的equals
- 包装类的equals首先会判断是否是本类型如果不是直接返回false
- 否则比较值
- 装箱其实就是调用了 包装类的valueOf()方法，拆箱其实就是调用了 xxxValue()方法。`Integer i = 10 等价于 Integer i = Integer.valueOf(10)
  int n = i 等价于 int n = i.intValue()`; 

## 判断创建多少个对象
因为大多包装类型都用cache，在判断时考虑是否超出了cache范围，否则会创建新对象