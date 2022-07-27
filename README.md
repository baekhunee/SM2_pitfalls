# 实验名称
SM2_pitfalls

# 实验简介
通过代码测试SM2签名存在的漏洞

# 实验完成人
权周雨 

学号：202000460021 

git账户名称：baekhunee

# 运行指导
代码可以直接运行

# 实验原理及对应代码实现
## k泄露
![image](https://user-images.githubusercontent.com/105578152/181257219-7e20a766-bae0-41f7-8c65-55b34fd22c20.png)

可以通过标红的公式恢复私钥d_A

## 核心代码
```
# k泄露
r,s = SM2_signature(m)
sk = (inverse(s + r,n) * (k - s))%n
print('\nLeaking k:')
print("Private key:",sk)
```

## k重用
![image](https://user-images.githubusercontent.com/105578152/181257431-2147cbb8-3d9c-413d-9862-bf237c28d840.png)

可以通过最后一行公式恢复私钥d_A

## 核心代码
```
# k重用
m1 = '20220430'
m2 = '20220601'
r1,s1 = SM2_signature(m1)
r2,s2 = SM2_signature(m2)
sk = ((s2 - s1) * inverse((s1 - s2 + r1 - r2),n))%n
print('\nReusing k:')
print("Private key:",sk)
```
## 多个用户重用k
![image](https://user-images.githubusercontent.com/105578152/181257601-690f0d88-cbf7-458f-b10a-9dbe8474d08e.png)

Alice可以通过签名推断出Bob的私钥d_B，同样地，Bob亦可以通过签名推断出Alice的私钥d_A

## 核心代码
```
# 不同用户重用k
r1,s1 = SM2_signature(m1)
r2,s2 = SM2_signature(m2)
sk1 = ((k - s1) * inverse(s1 + r1,n))%n
sk2 = ((k - s2) * inverse(s2 + r2,n))%n
print('\nReusing k by different users:')
print("Deduce private key1:",sk1)
print("Deduce private key2:",sk2)
```

## 使用与ECDSA相同的d与k
![image](https://user-images.githubusercontent.com/105578152/181257960-44cd1332-dbf8-488e-8835-79ecf07e1678.png)

可以通过最后一行公式恢复私钥d

## 核心代码
```
# 使用和ECDSA相同的d与k
e1 = hash(m)
r1,s1 = SM2_signature(m1)
r2,s2 = ECDSA_signature(m2)
sk = ((s1 * s2 - e1) * inverse((r1 - s1 * s2 - s1 * r2),n))%n
print('\nSame d and k with ECDSA:')
print("Private key:",sk)
```

# 测试截图
![image](https://user-images.githubusercontent.com/105578152/181258566-0a785bb6-f446-42d0-a022-a6c7298ce13e.png)
