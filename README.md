# SASDN
 **用于超分辨率重建的逐步对抗式稳定扩散网络**
1.  网络将两种当前较为成熟的图像生成式网络模型：生成对抗式网络和稳定扩散网络结构相融合
2.  网络主要创新点在于：
    1.  原始高分辨率图像分成两条线路提供目标图像
        1.  下采样+引入噪声
        2.  下采样
    2. 从纯噪声图像开始，每一个去噪时间步中引入两个判别器，指导每一步去噪和上采样
       1. 噪声判别器：负责指导模型的噪声抑制能力，以**下采样+引入噪声**为目标图像
       2. 纹理判别器：负责指导模型的纹理增强能力，以**下采样**为目标图像
    3. 给两个判别器一定权重，根据需求自行调整噪声抑制和纹理增强的重要程度
    4. 引入多注意力头结构，最大化利用图像中原有信息。
3. 网络详细信息：
   1. 前向扩散：
      1. 特征图从 512->448->384->320->256->192->128
      2. backbone 中每个层级特征图分 4 次上采样，每次提升 16