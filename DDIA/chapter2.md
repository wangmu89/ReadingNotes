# 数据模型与查询语言

分层系统的基本思想：每层都通过提供一个简洁的数据模型来隐藏下层的复杂性。



**数据模型**

关系模型（SQL）：数据被组织成关系（relations，SQL中的表（table）），每个关系都是元组（tuples）的无序集合（SQL中的行（row））。

NOSQL（Not Only SQL）的采用：

- 比关系数据库更好的扩展性需求，包括支持超大数据集或超高写入吞吐量
- 普遍偏爱免费和开源软件而不是商业数据库产品
- 关系模型不能很好地支持一些特定的查询操作
- 对关系模式一些限制性感到沮丧，渴望更具动态和表达力的数据模型

SQL+NOSQL：混合持久化（Polyglot persistence）



impedance mismatch：阻抗失谐，对象和关系不匹配，对象-关系映射框架（Objet-relational mapping，ORM，如：ActiveRecord、Hibernate）可以降低样板代码量，但是无法完全隐藏两个模型之间的差异。

一些开发人员认为JSON模型减少了应用程序代码和存储层之间的阻抗失配，但是JSON作为数据编码格式也存在问题。

缺乏模式常常被认为是一个优势。

