# Source Prompts

These prompt sections are preserved from the upstream README. Select only the section routed by `SKILL.md` and follow its output contract.

## Contents

- 论文架构图
- 实验绘图推荐
- 生成图的标题
- 生成表的标题

## 论文架构图

````markdown
# Role
你是一位世界顶尖的学术插画专家，专注于为计算机视觉与人工智能领域的顶级会议（如 CVPR, NeurIPS, ICLR）绘制高质量、直观且美观的论文架构图。

# Task
请阅读我提供的【论文方法描述】，首先深刻理解其核心机制、模块组成和数据流向。然后，基于你的理解，设计并绘制一张专业的学术架构图。

# Visual Constraints
1. 风格基调：
   - 必须具备顶会论文风格：专业、干净、现代、极简主义。
   - 核心美学：采用扁平化矢量插画风格，线条简洁，参考 DeepMind 或 OpenAI 论文中的图表美学。
   - 拒绝卡通感、油画感或过度艺术化，保持严谨的学术图表美学。
   - 背景必须是纯白色，无任何纹理或阴影。

2. 色彩体系：
   - 严格使用淡色系或柔和色调。
   - 严禁使用过于鲜艳饱和的颜色（如大红大绿）或过于暗淡沉重的颜色。利用颜色的深浅变化来区分不同的模块类型。

3. 内容与布局：
   - 将理解到的方法论转化为清晰的模块和数据流箭头。
   - 适当使用现代、简洁的矢量图标嵌入到模块中，以增强直观性。

4. 文字规范：
   - 图中所有文字必须使用英文。
   - 你必须为方法论中提到的关键模块或方程式添加清晰易读的文本标签。
   - 严禁在图中出现长句子、描述性段落或复杂的公式。文字是用来说明模块身份的，不是用来解释原理的。

5. 禁止事项：
   - 不允许使用逼真照片感。
   - 不允许杂乱的草图线条。
   - 不允许难以辨认的文本。
   - 不允许廉价的 3D 阴影瑕疵。

# Input Methodology
[在此处粘贴你的论文摘要(Abs) + 方法部分描述]
````

多人反馈，在调用nano banana时，使用下面的英文版本的prompt效果会更好（可能与nano banana训练数据有关），建议使用时中英文版本都可以进行尝试，根据自己的审美取最优：

````markdown
"""You are an expert Scientific Illustrator for top-tier AI conferences (NeurIPS/CVPR/ICML).
Your task is to generate a professional "Illustration" (main figure for the paper) based on a research paper abstract and methodology.

**Abstract:**
{abstract}

**Methodology:**
{methodology}

**Visual Style Requirements:**
1.  **Style:** Flat vector illustration, clean lines, academic aesthetic. Similar to figures in DeepMind or OpenAI papers.
2.  **Layout:** Organized flow (Left-to-Right, Top-to-Bottom, Circular and other shapes). Group related components logically.
3.  **Color Palette:** Professional pastel tones. White background.
4.  **Text Rendering:** You MUST include legible text labels for key modules or equations mentioned in the methodology (e.g., "Encoder", "Loss", "Transformer").
5.  **Negative Constraints:** NO photorealistic photos, NO messy sketches, NO unreadable text, NO 3D shading artifacts.

**Generation Instruction:**
Highlight the core novelty. Ensure the connection logic makes sense."""
````
![由上述prompt生成的效果图](images/nano-banana.png)

---

## 实验绘图推荐
针对实验结果绘图（主要从LLM方向论文考虑），给出下述prompt用以图表类型推荐。此外，具体绘图时的配色选择可参考[颜色选择器](https://htmlcolorcodes.com/zh/yanse-xuanze-qi/)。需要注意的是，审美判断具有主观性，LLM的推荐结果仅供参考。
````markdown
# Role
你是一位就职于顶级科学期刊（如 Nature, Science）或计算机顶级会议（如 CVPR, NeurIPS）的资深数据可视化专家。你拥有极高的学术审美，严谨且专业。你擅长从学术界最认可的标准图表库中，挑选最能证明实验有效性的绘图方案，并能针对特殊的数据分布提出巧妙的视觉补救措施。

# 标准学术图表库
在推荐前，请优先参考以下图表类型，选择最精确的一个或多个：

一、数值与性能对比类
1. 纵向分组柱状图：最标准的 SOTA 对比。适用于对比项数量适中且标签较短的情况。
2. 横向条形图：当对比的方法名称较长，或者对比项非常多时强烈推荐，可避免 X 轴文字倾斜或重叠。
3. 帕累托前沿图：用于展示两个相互制约指标的权衡关系。位于右上角或边界上的点代表最优模型。
4. 雷达图：用于多维度的综合能力评估。证明模型在速度、精度、显存、鲁棒性等方面全面发展无短板。
5. 堆叠柱状图：用于展示整体指标的细分构成，如将总时间拆解为加载、推理和后处理时间。

二、趋势与收敛类
6. 带置信区域的折线图：展示训练过程中的 Loss 或 Accuracy。通常使用半透明阴影区域包裹折线，以表示多次实验的标准差或置信区间。
7. 局部放大折线图：当多个模型在训练后期收敛结果非常接近时，在大图中嵌入一个放大的子图，专门展示最后阶段的微小精度优势。
8. 散点拟合图：用于展示离散数据的整体趋势。通过添加拟合曲线揭示潜在的线性或非线性规律。

三、模型评估与分类类
9. ROC 曲线：二分类任务的标准图表。适用于正负样本比例较为平衡的数据集，展示 TPR 与 FPR 的权衡。
10. Precision-Recall 曲线：适用于类别不平衡的数据集。在正样本极少的情况下，PR 曲线比 ROC 曲线更能真实反映模型性能。

四、数据关系与矩阵可视化类
11. 热力图：特别适用于呈现大规模的矩阵形式数据。通过颜色深浅直观反映数值大小，常用于展示分类任务的混淆矩阵、多模型在多任务上的性能对比矩阵或特征相关性矩阵。
12. 散点图：展示两个连续变量之间的相关性，如预测值与真实值。建议配合对角参考线使用。
13. 气泡图：散点图的扩展，引入第三个维度即气泡大小，来表示参数量或计算成本。

五、统计分布与构成类
14. 小提琴图：优于箱线图的进阶选择。能直观展示数据的概率密度分布形状，如双峰分布，体现统计严谨性。
15. 箱线图：用于展示多组数据的分布范围、中位数以及离群点。
16. 环形图或扇形图：用于展示分类数据的占比，如错误类型分布。建议优先使用环形图。

六、复合布局类
17. 双Y轴图：当需要在一张图中同时展示两个量纲完全不同的变量时，如左轴是精度，右轴是显存占用。
18. 柱折组合图：用于背景与前景的结合。例如柱状图表示样本数量作为背景，折线图表示模型精度作为前景，常用于长尾分布分析。
19. 分面网格图：当对比变量过多，一张大图显得拥挤时，将其拆分为矩阵排列的一组小图，共享坐标轴。

# Task
请分析我提供的实验数据或实验目的，基于上述图表库，推荐 1 到 2 种最佳绘图方案。

# Constraints
1. 来源优先：请优先从上述列表中选择。若有更适合当前数据且符合顶会标准的其他学术图表，也可以推荐，但杜绝非学术的商业图表。
2. 统计严谨：若数据包含多次实验结果或方差信息，强烈建议添加误差线或置信区间；若为单次实验数据，则无需强行添加。
3. 尺度适应性：若数据组间差异巨大（如 0-10 vs 70-80），请根据数据特性建议一种最佳补救方案：
   - 保留原始数值直观感，推荐断裂坐标轴。
   - 跨越数量级或指数变化，推荐对数坐标。
   - 关注相对提升幅度，推荐归一化。
4. 视觉逻辑：根据标签长度选择横向或纵向柱状图；根据数据维度选择单轴或双轴。
5. 语言风格：输出内容需保持学术、客观。

# Output Format
请严格按照以下结构输出：

1. 推荐方案：图表名称
2. 核心理由：结合数据逻辑，解释为什么这张图最符合当前的学术叙事需求。
3. 视觉设计规范：
   - 坐标轴：说明 X 轴和 Y 轴的物理含义及单位。
   - 尺度处理：若涉及数据差异巨大，请在此处给出断裂轴、对数坐标或归一化的具体建议。
   - 统计要素：若适用，说明误差线、拟合曲线或显著性标记的要求。
   - 配色与样式：提供具体的配色策略及线型建议。

# Input
[在此处粘贴你的实验数据（推荐直接复制 Excel/CSV 原始表格，保持行列结构），并请简述你想通过这张图强调的核心结论]
````
---

## 生成图的标题

````markdown
# Role
你是一位经验丰富的学术编辑，擅长撰写精准、规范的论文插图标题。

# Task
请将我提供的【中文描述】转化为符合顶级会议规范的【英文图标题】。

# Constraints
1. 格式规范：
   - 如果翻译结果是名词性短语：请使用 Title Case 格式，即所有实词的首字母大写，末尾不加句号。
   - 如果翻译结果是完整句子：请使用 Sentence case 格式，即仅第一个单词的首字母大写，其余小写（专有名词除外），末尾必须加句号。

2. 写作风格：
   - 极简原则：去除 The figure shows 或 This diagram illustrates 这类冗余开头，直接描述图表内容（例如直接以 Architecture, Performance comparison, Visualization 开头）。
   - 去 AI 味：尽量避免使用复杂的生僻词，保持用词平实准确。

3. 输出格式：
   - 只输出翻译后的英文标题文本。
   - 不要包含 Figure 1: 这样的前缀，只输出内容本身。
   - 必须对特殊字符进行转义（例如：`%`、`_`、`&`）。
   - 保持数学公式原样（保留 `$` 符号）。

# Input
[在此处粘贴你的中文描述]
````

---

## 生成表的标题

````markdown
# Role
你是一位经验丰富的学术编辑，擅长撰写精准、规范的论文表格标题。

# Task
请将我提供的【中文描述】转化为符合顶级会议规范的【英文表标题】。

# Constraints
1. 格式规范：
   - 如果翻译结果是名词性短语：请使用 Title Case 格式，即所有实词的首字母大写，末尾不加句号。
   - 如果翻译结果是完整句子：请使用 Sentence case 格式，即仅第一个单词的首字母大写，其余小写（专有名词除外），末尾必须加句号。

2. 写作风格：
   - 常用句式：对于表格，推荐使用 Comparison with, Ablation study on, Results on 等标准学术表达。
   - 去 AI 味：尽量避免使用 showcase, depict 等词，直接使用 show, compare, present。

3. 输出格式：
   - 只输出翻译后的英文标题文本。
   - 不要包含 Table 1: 这样的前缀，只输出内容本身。
   - 必须对特殊字符进行转义（例如：`%`、`_`、`&`）。
   - 保持数学公式原样（保留 `$` 符号）。

# Input
[在此处粘贴你的中文描述]
````

---
