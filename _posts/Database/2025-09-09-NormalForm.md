---
layout: post
title: "NormalForm"
date: 2025-09-09
categories: database
tags: [database, sql]
---
## 数据库范式 Normal Form

| Normal Forms | Definition                             |      |
| ------------ | -------------------------------------- | ---- |
| 1NF          | 属性都是atomic                         |      |
| 2NF          | 非主属性对候选键不存在部分函数依赖     |      |
| 3NF          | 非主属性对候选键不存在传递依赖         |      |
| BCNF         | 主属性对候选键不存在部分和传递函数依赖 |      |

#### 判断范式

1. 确定候选键
2. 是否存在非主属性对主属性的部分依赖(仅当主属性为组合键的情况下，有可能不满足2NF)
   1. 存在->1NF
3. 非主属性是否传递依赖于候选键
   1. 存在->2NF
4. 判断所有依赖项的左边是否全为候选键
   1. 是->BCNF
   2. 否->3NF

#### 第一范式 （1NF）

数据库表中的任何属性都是atomic的。

实体中的某个属性不能有多个值，或者不能有重复的属性。

#### 第二范式 （2NF）

定义：非主属性**完全依赖**于主键。（不能存在依赖主关键字的一部分的属性 no partial）

A relation schema R is in second normal form (2NF) if nonprime attributes A in R are not partially dependent on any key of R.

**所有候选键为单关键字的关系都符合第二范式。**

**不符合2NF的情况，只存在于候选键为组合关键字的情况下。**

例题：

如果存在局部依赖（不为2NF），则应该把这部分分离出来作为新的实体。

{学号，课程名称}  ---> {姓名，年龄，成绩，学分}

学号 ---> 姓名，年龄

课程名称 ---> 学分

(1) 数据冗余：

同一门课程由n个学生选修，"学分"就重复n-1次；同一个学生选修了m门课程，姓名和年龄就重复了m-1次。

 (2) 更新异常：

若调整了某门课程的学分，数据表中所有行的"学分"值都要更新，否则会出现同一门课程学分不同的情况。

(3) 插入异常：

假设要开设一门新的课程，暂时还没有人选修。这样，由于还没有"学号"关键字，课程名称和学分也无法记录入数据库。 

(4) 删除异常：

假设一批学生已经完成课程的选修，这些选修记录就应该从数据库表中删除。但是，与此同时，课程名称和学分信息也被删除了。很显然，这也会导致插入异常。

#### 第三范式（3NF）

定义：在第二范式的基础上，数据表中如果**不存在非关键字段对任一候选关键字段的传递函数依赖**则符合第三范式。

A relation schema R is in third normal form (3NF) if, whenever a nontrivial functional dependency X → A holds in R, either X is a superkey of R, or A is a prime attribute of R.

**第三范式就是属性不依赖于其它非主属性**。

所谓传递函数依赖（Transitive functional dependency)，指的是如果存在"A → B → C"的决定关系，则C传递函数依赖于A。

将有函数依赖的表，拆分为多个表。

#### Boyce-Codd Normal Form（BCNF是3NF的改进形式）

定义：在第三范式的基础上，数据库表中如果**不存在任何字段对任一候选关键字段的传递函数依赖**则符合鲍依斯-科得范式。

A relation schema R is in Boyce-Codd Normal Form (BCNF) if whenever a nontrivial FD X → A holds in R, then X is a superkey of R.

另一种判断方式是，**对每个函数依赖X→Y的左侧求闭包，如果对于每一个函数依赖，左侧的闭包都包含关系R中的所有属性，那么这个关系R是BCNF范式的**。 反之，用以上方法判断时，如果出现函数依赖不满足以上条件，那么就存在违背BCNF范式的情况， 这个关系R就不是BCNF范式的。

假设仓库管理关系表为StorehouseManage(仓库ID, 存储物品ID, 管理员ID, 数量)，且有一个管理员只在一个仓库工作；一个仓库可以存储多种物品。这个数据库表中存在如下决定关系：

(仓库ID, 存储物品ID) →(管理员ID, 数量)

(管理员ID, 存储物品ID) → (仓库ID, 数量)

所以，(仓库ID, 存储物品ID)和(管理员ID, 存储物品ID)都是StorehouseManage的候选关键字，表中的唯一非关键字段为数量，它是符合第三范式的。但是，由于存在如下决定关系：

(仓库ID) → (管理员ID)

(管理员ID) → (仓库ID)

即存在关键字段决定关键字段的情况，所以其不符合BCNF范式。

#### 范式之间的关系

Each normal form is strictly stronger than the previous one

Every 2NF relation is in 1NF

Every 3NF relation is in 2NF

Every BCNF relation is in 3NF

There exist relations that are in 3NF but not in BCNF

BCNF is considered a stronger form of 3NF

The goal is to have each relation in BCNF (or 3NF)



#### Inferred Functional Dependencies

##### Armstrong's inference rules

IR1. (Reflexive) If Y ⊆ X, then X → Y

IR2. (Augmentation) If X → Y , then XZ → YZ

IR3. (Transitive) If X → Y and Y → Z, then X → Z

##### Other Inference Rules

+ Decomposition: If X → YZ,then X → Y andX → Z
+ Union: If X → Y and X → Z,then X → YZ
+ Pseudotransitivity: If X → Y and WY → Z, then WX → Z

The last three inference rules, as well as any other inference rules, can be deduced from IR1, IR2, and IR3 (completeness property)

##### Closure 闭包

一个集合F的函数依赖的闭包，是所有能从F推导出来的所有函数依赖。

F+ can be calculated by repeatedly applying IR1, IR2, IR3 using the FDs in F.

求集合F的闭包：

1. 闭包中包括所有集合F中的属性
2. 找这些属性存在的依赖
3. 将依赖的对应的属性写入到闭包中，重复步骤2



#### Lossless Join (无损连接) (Nonadditive Join)

Let R1 and R2 form a decomposition of R.

The decomposition is a lossless decomposition if there is no loss of information by replacing R with two relation schemas R1 and R2.

#### Cover

F covers G if every FD in G can be inferred from F(so G ⊆ F+)

#### Equivalence

F and G are equivalence if F covers G and G covers F.

#### Minimal Cover

A set F of FDs is **minimal** if it satisfies the following conditions

Every dependency in F has a single attribute as RHS.

We cannot remove any dependency from F and have a set of dependencies that is equivalent to F .

We cannot replace any FD X → A in F with a dependency Y → A,whereY ⊂X andstillhaveasetofFDsthatis equivalent to F.



##### 平凡函数依赖

定义：若X->Y，且Y是X的子集（对任一关系模式，平凡函数依赖必然成立），就是平凡函数依赖。

举例：

在学生表(学号,姓名,年级)中,(学号,姓名)可以推导学号和姓名其中的任何一个,就是所谓的平凡函数依赖。

简单来说，就是只要Y是X的子集，Y就依赖于X。

##### 非平凡函数依赖

定义：若X->Y，但Y不是X的子集，就是非平凡函数依赖。

举例：学生表(学号,姓名,年级，性别)中,通过(学号,姓名)可以推出这个学生所在的年级,但年级不是（学号，姓名）的子集，这是非平凡函数依赖.((学号,姓名)就是一个x,学号或者姓名就是一个x')。

