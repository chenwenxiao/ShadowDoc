#### 3.8
可以画出计算树为

	A1 * B1(1) A2 * B2(2) A3 * B3(3) A4 * B4(4)
        \        /            \       /
            +(5)                 +(6)
               \                 /
                       +(7)

流水为

| pipe\time | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11| 12 | 13 | 14 | 15 | 16 | 17 | 18 |
| :-: |
| 5 |   |   |   | 1 |   | 2 |   | 3 |   | 4 | 5 |   |   | 6 |   |   |   | 7 |
| 4 |   |   |   |   |   |   |   |   |   | 5 |   |   | 6 |   |   |   | 7 |   |
| 3 |   |   |   |   |   |   |   |   | 5 |   |   | 6 |   |   |   | 7 |   |   |
| 2 |   | 1 | 1 | 2 | 2 | 3 | 3 | 4 | 4 |   |   |   |   |   |   |   |   |   |
| 1 | 1 |   | 2 |   | 3 |   | 4 | 5 |   |   | 6 |   |   |   | 7 |   |   |   |

总时间为18△t

TP = 7 / (18△t) = 0.39 / △t
S = (4 * 4△t + 3 * 4△t) / (18△t) = 14 / 9 = 1.56
E = (4 * 4△t + 3 * 4△t) / (5 * 18△t) = 14 / 45 = 0.31

#### 3.9

##### (1)
先计算F = {1, 3, 4, 8} 对应二进制为
C0:
C0 = 10001101
C2 = 10101111
C5 = 10001101 = C0
C6 = 10001111
C7 = 10001101 = C0

C2:
C2_2 = 10101111 = C2
C2_5 = 10001101 = C0
C2_6 = 10001111 = C6
C2_7 = 10001101 = C0

C6:
C0   = 10001101
C6_2 = 10101111 = C2
C6_5 = 10001101 = C0
C6_6 = 10001111 = C6
C6_7 = 10001101 = C0


![状态图.png](.\状态图.png)

##### (2)
计算平均启动距离

| Circle | Mean Start Distance |
| :-: |
| 2, 5 | 3.5 |
| 2, 6, 5| 4.333 |
| 6, 5| 5.5 |
| 6, 2, 5| 4.333 |
| 5| 5 |

采用(2,5)的间隔

最大吞吐率为 1/(3.5△t) = 0.29/△t

##### (3)

调度开始处分别为1,3,8,10,15,17，最后一个Task结束时刻为25
吞吐率为6/(25△t) = 0.24/△t

### 3.10

####(1)

F = {1, 3, 6}
C0 = 100101
C2 = 101101
C4 = 100111
C5 = 100101 = C0

C2_2 = 101111
C2_4 = 100111 = C4
C2_5 = 100101 = C0

C4_2 = 101101 = C2
C4_4 = 100111 = C4
C4_5 = 100101 = C0

C2_2_2 = 101111 = C2_2
C2_2_4 = 100111 = C4
C2_2_5 = 100101 = C0

![状态图2.png](.\状态图2.png)

#### (2)

如果允许不等时间间隔，那么选择2,2,5，最大吞吐率为0.333/△t
如果不允许不等时间间隔，那么选择4，最大吞吐率为0.25/△t

#### (3)

如果允许不等时间间隔，开始位置为1,3,5,10,12,14,19,21,23,28,结束位置34，吞吐率为0.29/△t，加速比为70/34=2.06
如果不允许不等时间间隔，开始位置为1,5,9,13,17,21,25,29,33,37，结束位置43，吞吐率为0.23/△t，加速比为70/43=1.63

### 3.11

#### (1)


| instruction\time | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11| 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20
| :-: |
| LW     | IF | ID | EX | ME | WB |    |    |    |    |    |    |    |    |    |    |    |    |    |    |    |
| DADDUI |    | IF | S  | S  | ID | EX | ME | WB |    |    |    |    |    |    |    |    |    |    |    |    |
| SW     |    |    |    |    |    | IF | S  | S  | ID | EX | ME | WB |    |    |    |    |    |    |    |    |
| DADDUI |    |    |    |    |    |    |    | IF | ID | EX | ME | WB |    |    |    |    |    |    |    |    |
| DSUB   |    |    |    |    |    |    |    |    | IF | S  | S  | ID | EX | ME | WB |    |    |    |    |    |
| BNEZ   |    |    |    |    |    |    |    |    |    |    |    | IF | S  | S  | ID | EX | ME | WB |    |    |
| LW(2nd loop)|    |    |    |    |    |    |    |    |    |    |    |    |    |    | S  | IF | ID | EX | ME | WB

需要一共99个loop，每个loop需要15个时钟周期，总计15*99+3 = 1488

#### (2)

| instruction\time | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11| 12 | 13 | 14 |
| :-: |
| LW     | IF | ID | EX | ME | WB |    |    |    |    |    |    |    |    |    |
| DADDUI |    | IF | ID | S  | EX | ME | WB |    |    |    |    |    |    |    |
| SW     |    |    | IF | S  | ID | EX | ME | WB |    |    |    |    |    |    |
| DADDUI |    |    |    |    | IF | ID | EX | ME | WB |    |    |    |    |    |
| DSUB   |    |    |    |    |    | IF | ID | EX | ME | WB |    |    |    |    |
| BNEZ   |    |    |    |    |    |    | IF | S  | ID | EX | ME | WB |    |    |
| LW(2nd loop)|    |    |    |    |    |    |    |    | S  | IF | ID | EX | ME | WB |

一共需要9 * 99 + 3 = 894个时钟周期

#### (3)

更改指令为

	LW R1,0(R2)
    DADDIU R2,R2,#4
    DSUB R4,R3,R2
    DADDIU R1,R1,#1
    BNEZ R4,LOOP
    SW R1,-4(R2)

| instruction\time | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11|
| :-: |
| LW     | IF | ID | EX | ME | WB |    |    |    |    |    |    |
| DADDUI |    | IF | ID | EX | ME | WB |    |    |    |    |    |
| DSUB   |    |    | IF | ID | EX | ME | WB |    |    |    |    |
| DADDUI |    |    |    | IF | ID | EX | ME | WB |    |    |    |
| BNEZ   |    |    |    |    | IF | ID | EX | ME | WB |    |    |
| SW     |    |    |    |    |    | IF | ID | EX | ME | WB |    |
| LW(2nd loop)|    |    |    |    |    |    | IF | ID | EX | ME | WB |

需要6 * 99 + 4 = 598个时钟周期

#### Q1

Q1：Write down the bypass condition for the path
between M (Memory) -> D (Decode) stages into register B. (The path is shown with a dotted line in the figure.)

	Bypass MEM->ID(B) = Case opcode M
    	LW  => rdata
        ... => addr

BSrc need to choose bypass by the rd2 and wd, if rd2 == rd E or rd M or rd W then choose bypass ALU->ID(B) or bypass Memory->ID(B) or bypass Writeback->ID(B)

#### Q2

Q2：Write down the stall condition in which stalls are only caused by data hazards.
Stall = (rsD=wsE). (opcodeE=LWE).(wsE≠0 ).re1D + (rtD=wsE). (opcodeE=LWE).(wsE≠0 ).re2D


#### Q3

	LW r2 r1 (r2 <- MEM[r1])
    NOP
    ADD r3 r1 r2 (r3 <- r1 + r2)
    NOP
    NOP

In the 3th instruction, the register B is r2 and r2 should use the data from instruct 'LW r2 r1'.


