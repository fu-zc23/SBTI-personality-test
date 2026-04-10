# SBTI 人格测试

这是一个基于前端实现的 SBTI 人格测试网页复刻项目，原作者：[B站@蛆肉儿串儿](https://space.bilibili.com/417038183) 。

项目完全运行在浏览器中：

- 无后端服务
- 无接口请求
- 所有题目、规则与人格库均内置在前端

测试流程基于 15 个维度的评分模型，将结果映射为不同的人格类型。

## 使用方法

### 方式一：直接打开

直接使用浏览器打开 `index.html` 文件。

### 方式二：本地服务器运行

进入项目目录，运行以下命令启动本地服务器：

```bash
python -m http.server 8000
```

打开浏览器访问：

```
http://localhost:8000
```

## 测试解析

### 一、测试结构

测试 15 个 “性格维度”，每个维度 2 道题，共 30 道题。还有 2 道特殊题，用于触发隐藏人格 `DRUNK`。

15 个性格维度分成 5 组模型：

- 自我模型
  - S1 自尊自信
  - S2 自我清晰度
  - S3 核心价值
- 情感模型
  - E1 依恋安全感
  - E2 情感投入度
  - E3 边界与依赖
- 态度模型
  - A1 世界观倾向
  - A2 规则与灵活度
  - A3 人生意义感
- 行动驱力模型
  - Ac1 动机导向
  - Ac2 决策风格
  - Ac3 执行模式
- 社交模型
  - So1 社交主动性
  - So2 人际边界感
  - So3 表达与真实度

### 二、评分方式

每道题目 1-3 分，因此每个维度总共 2-6 分，分为低、中、高三种结果：

- 低（L）：2-3 分
- 中（M）：4 分
- 高（H）：5-6 分

得到一个 15 维 “人格向量”：

```
['S1','S2','S3','E1','E2','E3','A1','A2','A3','Ac1','Ac2','Ac3','So1','So2','So3']
```

例如某人的“人格向量”可能为：

```
[H, H, M, L, H, M, H, M, H, L, L, M, H, H, H]
```

最后匹配最相近的标准人格模板：

```
CTRL   → HHH-HMH-MHH-HHH-MHM 
ATM-er → HHH-HHM-HHH-HMH-MHL 
Dior-s → MHM-MMH-MHM-HMH-LHL 
BOSS   → HHH-HMH-MMH-HHH-LHL 
THAN-K → MHM-HMM-HHM-MMH-MHL 
OH-NO  → HHL-LMH-LHH-HHM-LHL 
GOGO   → HHM-HMH-MMH-HHH-MHM 
SEXY   → HMH-HHL-HMM-HMM-HLH 
LOVE-R → MLH-LHL-HLH-MLM-MLH 
MUM    → MMH-MHL-HMM-LMM-HLL 
FAKE   → HLM-MML-MLM-MLM-HLH 
OJBK   → MMH-MMM-HML-LMM-MML 
MALO   → MLH-MHM-MLH-MLH-LMH 
JOKE-R → LLH-LHL-LML-LLL-MLM 
WOC!   → HHL-HMH-MMH-HHM-LHH 
THIN-K → HHL-HMH-MLH-MHM-LHH 
SHIT   → HHL-HLH-LMM-HHM-LHH 
ZZZZ   → MHL-MLH-LML-MML-LHM 
POOR   → HHL-MLH-LMH-HHH-LHL 
MONK   → HHL-LLH-LLM-MML-LHM 
IMSB   → LLM-LMM-LLL-LLL-MLM 
SOLO   → LML-LLH-LHL-LML-LHM 
FUCK   → MLL-LHL-LLM-MLL-HLH 
DEAD   → LLL-LLM-LML-LLL-LHM 
IMFW   → LLH-LHL-LML-LLL-MLL 
```

### 三、特殊人格

#### 1. 隐藏人格 `DRUNK`

如果 “您平时有什么爱好？” 选择了 “饮酒”，会触发隐藏题目 “您对饮酒的态度是？”，如果隐藏题选择了 “我习惯将白酒灌在保温杯，当白开水喝，酒精令我信服。” 选项，就会触发隐藏人格 `DRUNK`，覆盖其他人格。

#### 2. 兜底人格 `HHHH`

如果 “人格向量” 与任何人格的模板相似度小于 60%，直接匹配 `HHHH` 人格。

### 四、总结

整体上看，这个测试可以概括为：

> 将人格拆解为 15 个维度 →
> 构造一个人格向量 →
> 在预设模板中寻找最相近的一类。

因此该测试并不是在判断 “你属于哪一类人”，而是在回答 “你最像哪一类人”，图一乐就好。