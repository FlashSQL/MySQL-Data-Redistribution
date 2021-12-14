# MySQL Data Redistribution

## Motivation
While B-Tree is a ubiquitous index structure used in managing data, it is well known for its low space utilization in nodes. Such space under-utilization is detrimental to flash storage in terms of cost and performance. In particular, the logical space waste in B-tree will amplify physical writes inside flash storage, worsening the transaction throughput.

## Contribution
Our evaluation results from running OLTP benchmarks using the optimized MySQL/InnoDB prototype clearly show that those optimizations improve transaction throughput (i.e., more than 50%) with less space and cost (i.e., less than 40%) in flash storage.

### Experiment Result
- TPCC-Result
![image](https://user-images.githubusercontent.com/55489991/145993724-fc77122f-f276-4b74-81bb-e98004c64339.png)
- Index Space Utilization
![image](https://user-images.githubusercontent.com/55489991/145993926-a14f3b45-36a9-45f7-b4f7-4275c6f46a6f.png)


## Prerequisites & Installation Guide

1. Install prerequisites of mysql-5.6.26. Follow the instructions in the [site](https://github.com/LeeBohyun/mysql-tpcc/blob/master/installation_guide/multi-mysql-tpcc.md).
2. Clone this repository.
```bash
$ git clone https://github.com/FlashSQL/MySQL-Data-Redistribution.git
```
3. Run ``mysqld`` server to run MySQL.
