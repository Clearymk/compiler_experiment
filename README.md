### compiler_experiment
项目共分为三个模块

1. 词法分析器
2. 递归下降分析
3. SLR(1)分析法

----

## 使用方法
其中2和3可以对于输入的算术表达式进行语法分析并计算出结果，其中的case文件有输入的样例，三个样例分别对应三个模块的输入。

---

## 计算原理简要概述

在递归下降语法分析中，先将文法转换成SDD,将其转换为SDT，再去除左递归.每个文法符号有value属性或者syn和inh属性。在边语法分析时同时计算出结果。

下面给出SDT:

E -> T {E'.inh = T.val} E' {E.val = E'.syn}

E' -> \+T {E<sub>1</sub>'.inh = E'.inh \+ T.val} E<sub>1</sub>' {E'.syn = E<sub>1</sub>'.syn}

E' -> \-T {E<sub>1</sub>'.inh = E'.inh \- T.val} E<sub>1</sub>' {E'.syn = E<sub>1</sub>'.syn}

E' -> ε {E'.syn = E'.inh}

T -> F{T.inh = F.val} T' {T.syn = T.syn}

T' -> \*F{T<sub>1</sub>'.inh = T'.inh \* F.val} T<sub>1</sub>' {T'.syn = T<sub>1</sub>'.syn}

T' -> \F{T<sub>1</sub>'.inh = T'.inh \ F.val} T<sub>1</sub>' {T'.syn = T<sub>1</sub>'.syn}

T' -> ε {T'.syn = T'.inh}

F -> num {F.val = num.val}

F -> (E) {F.val = E.val}

在SLR(1)语法分析中通过一个计算栈来储存数据，在每次进行规约的时候进行计算工作。
原理:S属性的SDD在进行计算可以按照语法分析树的节点来后序遍历的来计算属性值，而规约的过程恰好就是一次后续遍历，所以不必特地构建语法分析树，直接在规约时计算属性值

---

本代码用于实验课，距离具体应用还有很长一段距离

---

- [ ] 支持小数运算

- [ ] 支持变量计算,如:i+i 
