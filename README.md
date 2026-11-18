# 边缘 MoE 文献总索引

**A = 边缘×MoE 交集（直接核心）**；

**B = 可迁移层**（非边缘的 MoE 技术，或非 MoE 的边缘技术）；

**C = 背景参照**（数据中心上限、benchmark、方向外分支）。

⭐ = 用户重点标记；⚠ = arXiv 预印本（文件名无会议/期刊前缀）

## 一、覆盖度诊断（v3，85 文件统计）

| 视角 | 覆盖情况 |
|---|---|
| 相关度 | **A 层 19 篇**（开题直接相关工作名单）／B 层 ~50／C 层 6 |
| 约束维度 | 容量 ~25 篇（拥挤）；带宽 ~12；**能耗与热仍 0 篇** |
| 系统层次 | 算法 ~10、硬件 1、**系统 ~55 → 开题定位系统方向** |
| 协同拓扑 | 单设备 ~40、多边缘 ~12、端云 1（CORE，应用层）、联邦 1（FLUX，微调侧） |
| 机制簇 | 预取已破零（ProMoE⚠、PRED-MoE）；**专家合并 4 篇成簇**（03.4）；理论 2 篇 + 基准 1 |
| 主方向格子 | 04.3 联合族 8 篇：**A 层竞争 2 篇（MoEZip✅ 正式发表 + Unified GPU Memory⚠ workshop）**；04.2 KV 族 8 篇全部非 MoE（B 层）→ **MoE×KV 正式文献仍为零，空白在但窗口收窄** |

## 二、⚠ 竞争预警（读表最重要的一节）

1. **NeurIPS26研讨会-Unified GPU Memory**（04.3）：KV Cache 与 Expert Weights 的**在线重分配**——与你的 KVE-MoE 设想几乎同题。虽是 workshop 论文，但说明该题已有人抢跑。
2. **NeurIPS26-MoEZip**（04.3）：路由感知的 MoE KV 压缩，**已正式发表**——从路由侧切入 MoE×KV。
3. 行动：尽快精读这两篇重新校准创新边界；开题时间表往前压；你的差异化落点仍是"KV 增长 × 专家工作集 × 在线请求调度"的**跨层闭环**（单一内存划分已被 VAMP/Unified GPU Memory 占位）。

## 三、文件夹树

```
D:\论文\边缘推理\
├── 文献总索引.md
├── 00-综述与笔记\                     (4)
├── 01-特性、理论与基准\                (3) 
├── 02-路由与门控\                     (5)
├── 03-专家结构与参数\                 (16)
│   ├── 03.1-剪枝\  ├── 03.2-压缩与量化\  ├── 03.3-分解与拆分\
│   └── 03.4-合并\  └── 03.5-新结构\
├── 04-内存与存储管理\ ★               (27)
│   ├── 04.1-权重驻留族\  ├── 04.2-KV族\  └── 04.3-联合族\
├── 05-调度与执行\                     (17)
│   ├── 05.1-请求级调度\  └── 05.2-执行级编排\
├── 06-跨节点协同（多边缘·端云·联邦）\    (12)
└── 07-硬件架构\                       (1)
```



## 四、清单

### 00-综述与笔记
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| CSUR-Network Edge Inference 综述 | ✅ | C | 边缘推理全景；分层框架来源 |
| 相关方向.md/.pdf | — | — | 开题推演：KVE-MoE、四周计划 |
| 子问题分类方案对比.md | — | — | 四套分类方案对比与决策记录 |

### 01-特性、理论与基准
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| INFOCOM25-Theory of MoE for MEC | ✅ | **A** | 边缘 MoE 理论建模——开题理论支点 |
| NeurIPS25-MoE-CAP | ✅ | C | MoE 系统成本/精度/性能基准 |
| ICLR26-Unveiling Super Experts | ✅ | B | 超级专家现象分析（剪枝/卸载依据） |
| The qs Inequality（双重惩罚） | ⚠ | B |  |

### 02-路由与门控
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| ICLR26-本地路由一致性 | ✅ | **A** | 哪些模型适合卸载——模型筛选依据 |
| MOBICOM26-CFMoE | ✅ | **A** | 路由局部性+差异化缓存布局（次04.1） |
| MOBICOM25-D2MoE | ✅ | **A** | 双路由+动态位宽（次03.2） |
| TriRoute | ⚠ | B | 学习型注意力/专家/KV 预算分配（次04.3） |
| AAAI26-AdaFuse (LoRA-Switch) | ✅ | B | token 级预门控选 adapter——预门控思想可迁移至专家预取（次05.2） |

### 03-专家结构与参数 · 03.1-剪枝
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| MOBICOM26-CRISP | ✅ | **A** | 边缘服务器组合感知剪枝+调度 |
| NeurIPS25-DiEP | ✅ | B | 可微专家剪枝 |
| NeurIPS25-Discovering Important Experts | ✅ | B | 重要专家发现的理论视角 |
| ICLR-Quantifying Expert Specialization | ⚠ | B | 专业化量化→剪枝（⚠无年份需查） |
| NeurIPS26-Modality-Aware Pruning | ✅ | C | 多模态 MoE 剪枝（方向外） |

### 03.2-压缩与量化
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| ICML26-ZipMoE | ✅ | **A** | 无损专家压缩+缓存亲和调度 |
| ICLR26-Global Expert-Level Mixed-Precision | ✅ | B | 专家级全局混合精度 |
| ICLR26-Efficient Quantization w/ Guarantees | ✅ | B | 带泛化保证的 MoE 量化 |

### 03.3-分解与拆分
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| ICLR26-TD-MoE | ✅ | B | 专家张量低秩分解 |
| Accelerating MoE…Adaptive Expert Split | ⚠ | B | 专家拆分（次04.1）；疑 EdgeMoE 系期刊版待确认 |

### 03.4-合并（新簇）
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| INFOCOM26-任务感知专家合并 | ✅ | **A** | 疑 ISCA24 期刊扩展版，需查重 |
| TON26-Adaptive Expert Merging | ✅ | **A** | 边缘场景专家合并 |
| ISCA24-Task-Aware Expert Merging | ✅ | B | 合并簇源头 |
| ⭐ICLR24-Merge, Then Compress | ✅ | B | 先合并后压缩 |

### 03.5-新结构
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| ICLR25-MoE++ | ✅ | B | 零计算专家 |
| NeurIPS26-dMoE | ✅ | C | 扩散 LLM 块专家（方向外） |

### 04-内存与存储管理 ★ · 04.1-权重驻留族
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| TMC25-EdgeMoE | ✅ | **A** | 开山作：移动端卸载+专家分割 |
| ⭐ASPLOS25-CoServe | ✅ | **A** | 受限内存 CoE 推理（CoE 定义待读） |
| WiSP（工作集视角） | ⚠ | **A** | 极低资源硬件工作集管理 |
| ASPLOS26-MoE-APEX | ✅ | **A** | 自适应精度×专家卸载（次03.2） |
| DAC26-SAEM | ✅ | **A** | CoT 阶段感知专家管理——工作集时变性，与你方向相关 |
| FluxMoE（驻留解耦） | ⚠ | B | 专家驻留与执行解耦 |
| NeurIPS26-Fewer Expert Transfers | ✅ | B | 不改路由的专家逐出策略 |
| NeurIPS26-Temporal MoE Serving | ✅ | B | 内存随活跃参数伸缩 |
| ProMoE | ⚠ | B | 预取代表作：主动缓存（次05.2） |
| SIGCOM26-POSTER-PRED-MoE | ✅ | B | 预测预取+逐出（poster） |
| NeurIPS24-Toward Efficient MoE | ⚠ | B | 泛 MoE 推理效率——**暂放此，待读定夹** |

### 04.2-KV 族（全部非 MoE → 全 B；MoE×KV 正式文献为零即你的空白）
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| ⭐INFOCOM26-Memory-Efficient KV at Edge | ✅ | B | 边缘 KV 优化——**主打方向直接对照** |
| MOBICOM26-mzCache | ✅ | B | 设备内多任务内存管理 |
| INFOCOM25-Mell | ✅ | B | 多 GPU KV 管理 |
| ICML24-KIVI | ✅ | B | KV 2bit 非对称量化 |
| ICLR25-KVTuner | ✅ | B | 分层敏感度 KV 混合精度量化 |
| NeurIPS25-Ada-KV | ✅ | B | KV 逐出自适应预算分配 |
| OSDI2026-Sereno | ✅ | B | 移动端内存带宽争用——"带宽干扰"论点弹药（B 中价值最高） |
| ⭐NeurIPS25-MoBA | ✅ | B | 块注意力长上下文（非 MoE；支撑"长上下文假设"论点） |

### 04.3-联合族 ★
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| NeurIPS26-MoEZip | ✅ | **A ⚠竞争** | 路由感知 MoE KV 压缩——正式发表 |
| NeurIPS26研讨会-Unified GPU Memory | ⚠ | **A ⚠同题预警** | KV×Expert 在线重分配 |
| Dynamic HBM Repartitioning（VAMP） | ⚠ | B ⚠竞争 | KV×Expert 动态显存划分（多轮） |
| Physically Partitioned KVCache（WriteScope） | ⚠ | B ⚠竞争 | CPU-GPU KV 物理分区负载均衡 |
| ICLR25-Mixture Compressor | ✅ | B | MoE 的 KV+权重联合压缩 |
| PiKV（两个版本） | ⚠ | B | MoE 分布式 KV 管理（双版本待比对删旧） |
| MOBICOM25-Elastic On-Device LLM | ✅ | B | 设备端弹性 LLM 服务（待读确认） |

### 05-调度与执行 · 05.1-请求级调度
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| MOBICOM26-Saber（⭐母论文） | ✅ | **A** | 专家路径分组；"KV 不是瓶颈"假设=切入点 |
| ICLR26-Semantic Parallelism | ✅ | B | MoE 模型-数据协同调度 |
| IEEE TPDS2026-ALPS | ✅ | B | 边缘长度预测调度（非 MoE） |
| MobiSys2025-EdgeLoRA | ✅ | B | 边缘多租户 LoRA |
| INFOCOM26-Semantic Caching | ✅ | B | 语义响应缓存 |
| INFOCOM26-SemCache | ✅ | B | 多用户 LoRA 语义缓存共享 |

### 05.2-执行级编排
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| ASPLOS25-Klotski ⭐ | ✅ | B | 多批流水（驻留次属04.1） |
| ASPLOS25-MoE-Lightning ⭐ | ✅ | B | CPU-GPU-I/O 流水+Roofline |
| ICLR25-Fiddler ⭐ | ✅ | B | CPU/GPU 动态执行位 |
| SOSP25-KTransformers ⭐ | ✅ | B | CPU-GPU 混合推理框架 |
| Accelerating Offloading…Interleaving（Bevy） | ⚠ | B | 并发请求交错 |
| NeurIPS25-MoESD | ✅ | B | 推测解码×稀疏 MoE |
| MOBICOM26-NPUGen | ✅ | B | NPU 代生成 KV 稳长上下文 |
| AAAI26-DIAA | ✅ | B | 设备内解码加速 |
| Efficient CPU-GPU collaborative MoE…（Apex） | ⚠ | **A**（场景待确认） | CPU-GPU 自适应专家分配——**与 ASPLOS26-MoE-APEX 重名待区分** |
| ICS26-LayerScope | ✅ | B | 跨层预测多批调度 |
| PACT26-HiNa-MoE | ✅ | B | CPU 矩阵引擎非侵入 MoE 推理 |

### 06-跨节点协同（多边缘·端云·联邦）
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| OrderMoE | ⚠ | **A** | 专家相似性驱动分布式边缘 MoE |
| TopoCompress | ⚠ | **A** | 拓扑感知 token 压缩降通信 |
| TrimMoE | ⚠ | **A** | 通信感知自适应深度 |
| INFOCOM26-Director ⭐ | ✅ | B | 分布式专家在线放置迁移（备选方向1对照） |
| SIGCOM25-MegaScale-Infer | ✅ | C | 数据中心分离式专家并行（上限参照） |
| INFOCOM2025-Jupiter | ✅ | B | 边缘设备间协同推理 |
| INFOCOM2026-HALO | ✅ | B | 有损边缘网络语义感知 |
| IEEE TC2026-张量并行 | ✅ | B | 异构边缘设备张量并行 |
| IEEE TMC2026-E2LLM | ✅ | B | 边-IoT 结构引导推理 |
| Sigcomm2026-Connex | ✅ | B | 终端移动性原语 |
| NeurIPS25-CORE | ✅ | C | 云-本地协作移动 agent（应用层） |
| EUROSYS26-FLUX | ✅ | B | 受限设备联邦微调稀疏 LLM |

### 07-硬件架构
| 文献 | 状态 | 相关度 | 定位 |
|---|---|---|---|
| ICCAD25-HD-MoE | ✅ | B | 3D 近存混合动态并行 |

## 五、待补文献清单（按优先级）

1. **Gimbal**（arXiv 2606.15177）——KV 压力+Expert 压力联合信号调度，主方向创新边界检查项。
2. **vLLM / PagedAttention**（SOSP'23）——KV 分页事实基线。
3. **SGLang / RadixAttention**——前缀缓存与调度。
4. **MoE-Infinity**——卸载式 MoE 引擎（实验底座候选）。
5. **Pre-gated MoE**（ICML'24）——路由预测/预取经典（ProMoE/PRED-MoE 可暂顶）。
