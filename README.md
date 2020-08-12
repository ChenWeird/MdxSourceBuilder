# MdxSourceBuilder

mdx图片词典制作工具：使用一个命令，实现从原始词条==> 标准化词条==> mdx源文件 ==> mdx词典文件

## 背景

### 需求背景

时常遇到一些好资料，怎奈只有纸质版或扫描版之类，希望将这些资料转换为可以检索的mdx词典，既方便使用，也提高利用率。

但是，常常在辛苦整理好词条（这是纯苦力活）之后，使用过往技术方案实现的成品却不够理想，不理想之处有两大方面：

* 导航不理想，极大降低了用户的使用体验
* 制作修订过程复杂，极大干扰了制作者的热情

这完全可以通过工具来解决。

### 程序设计背景

本来我只是提出痛点，希望有高人能出手解决，怎奈高人大都不屑于处理。

本非码农，可鉴于实在痛的厉害，只好自己用三脚猫功夫倒腾了人生第一个具有完整功能的程序。在此之前，从来没用过list、dict之类的，连这个github发布，都是现学现卖，还望高人不要耻笑，多提点才是。若有高人能够弄个更好的程序或是python版的或是GUI版的，那大家就有福了，我这纯粹抛砖引玉。

非码农的好处，或许是可以有更好的用户视角：既考虑词典终端用户的使用体验，也考虑普通的词典制作者的使用体验。虽不能解决所有问题，但至少已能解决我自己的大部分诉求，希望也能解决众多mdx词典用户的些许痛点。

## 解决方案

基本思路： 1.原始词条==> 2.标准化词条==> 3.mdx源文件 ==> 4.mdx词典文件

1. 原始词条：鉴于资料的多样性，原始词条的获取方式也是多种多样，有OCR来的，有手工输入的，也有从其他人的资料转编译来的，也有是因为制作人的喜好或用的工具不同，导致原始词条的格式完全不同。这个特点造就了解决方案必须：(1)兼容多样性，将最常见的词条样式纳入进来；(2)开放性，用户可以根据需要自定义更多个性化的原始词条样式。

    目前，本程序已经实现了对三种原始词条样式的兼容，用户也可以根据需要自定义添加。

2. 标准化词条：若能将多样化的原始词条转化为标准化的词条，那么后续就可以标准化处理了。因此如何定义标准化词条就变得很重要，它是实现后续程序的基础。

    目前，本程序已经提出了一个1.0版的最基本词条标准：一行页码，之后跟随多行关键词，每行一个关键词，如此往复。之所以说1.0版仅仅是最基本的标准，是因为这个标准还未能兼容如分栏、多层级词条等更复杂的情形，这些都有待后续有高人继续升级完善。

3. mdx源文件：这个txt文件与其他技术方案的最大区别是——包含了足够优良的页面导航、关键词导航以及用户自由定义的导航信息，极大提升用户对图片词典的使用体验。图片导航如何设计仁者见仁智者见智，因此，解决方案必须：(1)足够优良，不能太简陋，能用机器实现的定位，就不要浪费肉眼定位、繁琐操作定位等人类的精力；(2)兼容多样性，将最常见的导航样式纳入进来，比如封面附录等无需关键词导航、正文等需要关键词导航、拼音等则无需导航直接转链接到现有页面即可；(3)开放性，用户可以根据需要自定义CSS样式，或者添加更多个性化的导航样式。

    目前，本程序已经实现了三种导航样式，满足一本常见词典的基本需求，同时本程序会输出配套的精细CSS，方便用户个性化定制，此外用户也可以自由添加、改造导航样式。

4. mdx词典文件：这个步骤是可选项，但一步到位可以极大提升用户的体验，更重要的是使用这个工具可以实现跨平台制作mdx词典了，不必局限于Windows，Linux、Mac统统不在话下。当然要说明的是，这一环节用到了另一个开源工具， https://github.com/liuyug/mdict-utils ，功劳统统属于他！

## 使用方法

### 程序文件及安装

根本谈不上安装，因为整个程序就是3个Vim脚本文件而已，下载后，直接将这些脚本文件放在与词条文件同一个目录即可。

* MdxSourceBuilder.vim  这是入口文件：上半部分是配置文件，需要用户定义词典参数；下半部分是主程序，通常无需理会
* MdxSourceBuilderCore.vim  这是主程序调用的程序，仅当需要高级定制时修改，通常无需理会
* MdxSourceBuilderCSS.vim  这是CSS文件，样式文件可以在这里定义，通常无需理会

若有其他文件，都是附带的readme, demo之类，可以尽情删除。

### 极简使用说明

用 Vim 打开 MdxSourceBuilder.vim，新建文档，输入命令`:so MdxSourceBuilder.vim`，结束。

### 概要使用说明

1. 按格式要求准备好词条文件
2. 使用任意文本编辑器配置好 MdxSourceBuilder.vim 中的词典参数
3. 用 Vim 打开 MdxSourceBuilder.vim，新建文档，输入命令`:so MdxSourceBuilder.vim`

### 详细使用说明

直接打开查阅 MdxSourceBuilder.vim，其中“使用方法”及“词典参数配置”两个部分自带详细使用说明。

### 快速输入命令的Tip

输入`so mdx` 之后，按Tab键即可自动补全命令 `:so MdxSourceBuilder.vim`

### 相关FAQ

1. 关于Vim的使用：号称编辑器之神，确实上手不易，但也没宣传的那么夸张的难，我已把与这个程序有关的内容都写到文档中了。
2. 关于mdict-utils的使用：除了打包，还有很多其他解包、读取等功能，大家可以尽情挖掘改造。

## 社区讨论

* 讨论社区1: https://forum.freemdict.com/t/topic/2418
* 讨论社区2: https://www.pdawiki.com/forum/thread-40857-1-1.html

## LICENSE

[GPLv3](https://www.gnu.org/licenses/gpl-3.0.en.html)
