# B36 SOCBench（Detection）— 数据表格与分析

> 来源：DeepTempo SOCBench（socbench.org/detection），**没有对应论文**，因此本文件只有数据集统计，没有模型成绩。  
> 表格：[analysis/tables](../B36-socbench-detection/analysis/tables/)

## 1. 数据集概况（`data_overview.csv`）

benchmark-v0.parquet：757,641 条 NetFlow 风格的网络流记录，16 列（源/目的 IP 与端口、协议、收发字节与包数、TCP 标志、持续时间、采样率、标签）。恶意 282,595 条（37.3%）、正常 475,046 条；15,857 个源 IP、662,845 个目的 IP。另附 72 行 CIC-IDS2018 小样例。

## 2. 来源构成（`data_by_source.csv`）

| 来源 | 流数 | 恶意比例 | 包含的攻击标签 |
| --- | --- | --- | --- |
| malware_1_1 | 632,787 | 30.2% | C&C、水平端口扫描 |
| malware_3_1 | 85,884 | **97.7%** | Attack、C&C、水平端口扫描 |
| normal-xdsl-linux | 9,907 | 0 | 正常 |
| normal-at-home-linux | 9,797 | 0 | 正常 |
| normal-university-linux | 7,769 | 0 | 正常 |
| malware_34_1 | 7,209 | 73.8% | C&C、DDoS、端口扫描 |
| malware_8_1 | 4,237 | 48.5% | C&C |
| normal-https-website | 51 | 0 | 正常 |

8 个来源看起来出自 Stratosphere IoT-23 类的恶意软件捕获（各约 24 小时）与几段正常主机流量。一个来源（malware_1_1）就占全部数据的 83.5%，基准结果会被它主导。

## 3. 标签与特征（`data_by_attack.csv` 等）

- 攻击标签：水平端口扫描 202,940（26.8%）、“Attack” 70,495（9.3%）、C&C 8,843（1.2%）、DDoS 211。注意存在大小写不一致的重复标签（PartOfAHorizontalPortScan / PartOfAHorizontalPortscan，106 条），展示或评测时应合并。
- 协议（`data_protocol_x_label.csv`）：恶意流量几乎全部是 TCP（协议号 6，282,559 条），UDP（17）基本都是正常流量——仅凭协议就能分开大部分样本，说明该数据集对检测模型偏“容易”，有捷径特征。
- 恶意流量的目的端口集中在 Telnet 23（96,560）、SSH 22（70,487）、8080、2323——典型的 IoT 僵尸网络（Mirai 类）扫描特征。
- 数值特征中位数（`data_numeric_medians_by_label.csv`）：恶意流平均发出 370 字节/5 个包，正常流 60 字节/1 个包；pkts 字段有 3.63% 缺失。

## 4. 展示建议

在展示系统中作为“SOC 检测数据集”说明页：来源构成饼图、攻击类型条形图、目的端口 Top 10。由于没有论文与官方模型成绩，不宜放入模型排行榜。
