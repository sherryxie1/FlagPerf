### 天数智芯 BI-V100 GPU配置与运行信息参考

#### 环境配置

- ##### 硬件环境
    - 机器、加速卡型号: Iluvatar BI-V100 32GB

- ##### 软件环境
   - OS版本：Ubuntu 20.04
   - OS kernel版本:  5.4.0-148-generic x86_64    
   - 加速卡驱动版本：3.1.0
   - Docker 版本：20.10.21
   - 训练框架版本：torch-1.13.1+corex.3.1.0
   - 依赖软件版本：无


### 运行情况

* 通用指标

| 指标名称       | 指标值                  | 特殊说明                                    |
| -------------- | ----------------------- | ------------------------------------------- |
| 任务类别       | 自然语言编码            |                                             |
| 模型           | bert-large-uncased      |                                             |
| 数据集         | Wikipedia               |                                             |
| 数据精度       | precision,见“性能指标”  | 可选fp32/amp/fp16                           |
| 超参修改       | fix_hp,见“性能指标”     | 跑满硬件设备评测吞吐量所需特殊超参          |
| 硬件设备简称   | BI-V100                 |                                             |
| 硬件存储使用   | mem,见“性能指标”        | 通常称为“显存”,单位为GiB                    |
| 端到端时间     | e2e_time,见“性能指标”   | 总时间+Perf初始化等时间                     |
| 总吞吐量       | p_whole,见“性能指标”    | 实际训练序列数除以总时间(performance_whole) |
| 训练吞吐量     | p_train,见“性能指标”    | 不包含每个epoch末尾的评估部分耗时           |
| **计算吞吐量** | **p_core,见“性能指标”** | 不包含数据IO部分的耗时                      |
| 训练结果       | acc,见“性能指标”        | masked_lm任务准确率(实际/目标)              |


* 性能指标

| 配置               | precision | fix_hp | e2e_time | p_whole | p_train | p_core | acc         | mem       |
| ------------------ | --------- | ------ | -------- | ------- | ------- | ------ | ----------- | --------- |
| BI-V100单机8卡（1x8） | fp32      | bs=12  | 11199.1   | 53.8   | 55.6   | 55.8  | 0.657/0.655 | 30.4/32.0 |
| BI-V100单机8卡（1x8） | amp      | bs=16  | 4860.2    | 84.0   | 88.5   | 89.1  | 0.655/0.655 | 30.3/32.0 |
| BI-V100单机单卡（1x1） | fp32      | bs=12,lr=4.7e-05  | /        |    /     |   /      | 10.1      | /           |  28.0/32.0         |
| BI-V100两机8卡（2x8） | fp32      | bs=12,lr=7e-05  | /        |    /     |   /      | 98.2       | /           | 30.5/32.0        |

