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

# 实验原理
## k泄露
![image](https://user-images.githubusercontent.com/105578152/181257219-7e20a766-bae0-41f7-8c65-55b34fd22c20.png)

可以通过标红的公式恢复私钥d_A

## k重用
![image](https://user-images.githubusercontent.com/105578152/181257431-2147cbb8-3d9c-413d-9862-bf237c28d840.png)

可以通过最后一行公式恢复私钥d_A

## 多个用户重用k
![image](https://user-images.githubusercontent.com/105578152/181257601-690f0d88-cbf7-458f-b10a-9dbe8474d08e.png)

Alice可以通过签名推断出Bob的私钥d_B,同样地，Bob亦可以通过签名推断出Alice的私钥d_A

## 使用与ECDSA相同的d与k
![image](https://user-images.githubusercontent.com/105578152/181257960-44cd1332-dbf8-488e-8835-79ecf07e1678.png)

可以通过最后一行公式恢复私钥d

