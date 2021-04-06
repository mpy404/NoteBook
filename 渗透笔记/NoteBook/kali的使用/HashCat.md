# HashCat

## 扫描模式

1. 字典破解：Straight【0】

 - 基于字典破解

2. 组合破解：Combination【1】

 - 基于多个字典

3. 掩码暴力破解：Brute-force【3】

 - 基于掩码设置破解

4. 字典 + 掩码破解：Hydrib Wordlist + Mask【6】

5. 掩码 + 字典破解：Hydirb Mask + Wordlist【7】


## 掩码设置

| 参数 |              说明               |
| ---- | :-----------------------------: |
| l    |         a-z26个小写字母         |
| u    |         A-Z26个大写字母         |
| d    |             0-9数字             |
| h    |        0-9和a-z小写字母         |
| H    |        0-9和A-Z大写字母         |
| s    |            特殊字符             |
| a    |         代表上面的全部          |
| b    | 0x00-0xff【用来匹配空格这种的】 |

## 常用指令

| 参数        |                      说明                      | 案例                                                   |
| ----------- | :--------------------------------------------: | :----------------------------------------------------- |
| -a          |                  指定破解模式                  | -a 0【字典破解】<br>-a 1 【组合破解】                  |
| -m          |         指定破解的Hash类型，默认是md5          |                                                        |
| -o          |                  保存到文件中                  |                                                        |
| --force     | 忽略破解过程中的警告信息【跑单条Hash可能用到】 |                                                        |
| --show      |      显示已经破解的Hahs值及Hash对应的明文      |                                                        |
| --increment |             增量破解，指定密码长度             | --increment-min【最小值】<br>--increment-max【最大值】 |

## 密码组合

1. 八位数字密码

```
?d?d?d?d?d?d?d?d
```

2. 八位数字字母密码【前4个小写字母或数字，后4个大写字母后者数字】

```
?h?h?h?h?H?H?H?H
```

3. 八位未知密码

```
?a?a?a?a?a?a?a?a
```

4. 二到十位小写字母密码

```
--increment --increment-min 2 --increment-max 10 ?l?l?l?l?l?l?l?l
```

5. 二到十位未知密码

```
--increment --increment-min 2 --increment-max 10 ?a?a?a?a?a?a?a?a
```

6. 前面三个未知中间是root后面两个未知

```
?a?a?aroot?a?a
```

## 案例

### 通过掩码破解MD5值

```
hashcat.exe -a 3 -m 0 46f94c8de14fb36680850768ff1b7f2a ?d?d?d?l?l?l
```

### 通过字典破解MD5值

 - 先写Hash值，后写密码文件

```
hashcat.exe -a 0 -m 0 hash.txt passwords.txt ?d?d?d?l?l?l
```