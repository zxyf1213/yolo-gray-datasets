SVG-EAR 最理想的是直接选择让最终 Softmax Attention 误差最小的 block，但这个目标实际不可用于 routing：一方面，计算真实误差需要先得到 Full Attention，本身就要付出完整 QK
T
 的代价；另一方面，Softmax 的分母会把同一 query 下所有 block 耦合起来，改一个 block 的计算方式会改变整行所有 attention 权重，因此无法给每个 block 独立计算一个固定误差。作者因此放弃直接优化 Softmax 后的误差，转而比较 Softmax 之前的指数权重误差，使每个 block 可以独立打分和选择。
<img width="899" height="422" alt="image" src="https://github.com/user-attachments/assets/2e125c3f-e283-4bff-8191-47bd514272d0" />
