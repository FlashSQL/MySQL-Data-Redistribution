# MySQL Data Redistribution

## Motivation
While B-Tree is a ubiquitous index structure used in managing data, it is well known for its low space utilization in nodes. Such space under-utilization is detrimental to flash storage in terms of cost and performance. In particular, the logical space waste in B-tree will amplify physical writes inside flash storage, worsening the transaction throughput. 

## Contribution
Our evaluation results from running OLTP benchmarks(TPC-C) using the data redistribution MySQL clearly show that those optimizations improve transaction throughput (i.e., more than 50%) with less space and cost (i.e., less than 40%) in flash storage. Also the overall index space utilization is improved.

### Experiment Result
- TPCC-Result
![image](https://user-images.githubusercontent.com/55489991/145993724-fc77122f-f276-4b74-81bb-e98004c64339.png)

- Index Space Utilization

![image](https://user-images.githubusercontent.com/55489991/145994040-af8c83d5-0dab-4e35-b329-53c66dbe7b6b.png)


## Prerequisites & Installation Guide

1. Install prerequisites of mysql-5.6.26. Follow the instructions in the [site](https://github.com/LeeBohyun/mysql-tpcc/blob/master/installation_guide/multi-mysql-tpcc.md).
2. Clone this repository.
```bash
$ git clone https://github.com/FlashSQL/MySQL-Data-Redistribution.git
```
3. Run ``mysqld`` server to run MySQL.
4. Compare with Vanilla MySQL and see how table size changes

## Modified files compared to Vanilla MySQL
- storage/innobase/btr/btr0btr.cc
- storage/innobase/fil/fil0fil.cc
- storage/innobase/srv/srv0srv.cc
- storage/innobase/include/btr0btr.h
- storage/innobase/include/srv0srv.h
- storage/innobase/include/fil0fil.h

## Implementation Details about Data Redistritbution
- added a new function in btr0btr.cc: btr_page_redistribute_before_split()
- returns the inserted record
- btr_page_redistribute_before_split() is called during btr_page_split_and_insert()(btr0btr.cc) before split is performed
- modifications in srv0srv and fil0fil are for adding table id and table name

## References
- https://dev.mysql.com/
