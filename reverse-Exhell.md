# [2021 HackPack CTF] Exhell writeup
- difficulty : hard
- type : reverse

## Content
I'm tired of the IT department laughing at me when they see how much I spend on cans of effervescent water.
That's why I've decided to secure my expences with password, so that nobody will laugh at me ever again! 😤

## Provided File
exhell.xlsx 

## Analysis
![image](https://user-images.githubusercontent.com/67114268/115354570-becb0380-a1f4-11eb-8192-81972b8a8faf.png) <br> <br>
If you enter the correct password in place of flag{...}, you can see that the value changes. <br>
**In other words, the flag{...} we are looking for becomes the password.** <br> <br>


Let's see the logical_test.
```
=IF(IF(ISERROR(sUpErSeCrEt!$K$1), FALSE(), sUpErSeCrEt!$K$1), "Welcome back king ;.;",  "nope")
```

If you enter the correct password, you can expect 'sUpErSeCrEt!$K$1' to be true. <br>
Then, what is this value?

```
'sUpErSeCrEt' is the sheet name.
'$K$1' is the coordinate of the cell.
```

![image](https://user-images.githubusercontent.com/67114268/115354809-ff2a8180-a1f4-11eb-8f63-f5d29629cb7b.png) <br> <br>
Column k is affected by the boolean value of column j, and column j is affected by column i. <br>
So, if you put the correct value in column A, the value will be automatically filled up to K. <br> <br>


![image](https://user-images.githubusercontent.com/67114268/115355023-39941e80-a1f5-11eb-8c17-2d5691c42a4a.png) <br> <br>
What column A means is the H8 cell of the Buget sheet. <br>
This was a cell to input password. <br>
Column B can be filled through the values in column C, and if you break 8 rows in column B, it becomes one row in column A. <br>

![image](https://user-images.githubusercontent.com/67114268/115355112-516ba280-a1f5-11eb-8c69-e82f67ba23e7.png) <br> <br>
A value filled with FALSE is an OR operation, and a value filled with TRUE is an AND operation.
Thus, you can infer a boolean value that is not filled with this, and you can get A.
If you convert this to ASCII code, a flag appears.

```
flag{0h_g33z_th4t5_a_l0t_sp3nt_0n_L3Cr0ix}
```
