# Unity 风格指南

本文包含了在 Unity 中设置项目结构、脚本和资源命名规范的建议。

<a name="toc"></a>
## 目录

> 1. [简介](#introduction)
> 1. [项目结构](#structure)
> 1. [脚本](#scripts)
> 1. [资源命名规范](#anc)
> 1. [资源工作流程](#asset-workflows)

<a name="introduction"></a>
## 1. 简介

### 章节

> 1.1 [风格](#style)

> 1.2 [重要术语](#importantterminology)

<a name="style"></a>
### 1.1 风格

#### 如果你的项目已经有风格指南，应当遵循它。
如果你正在参与一个已有风格指南的项目或团队，应当尊重该指南。若本指南与现有指南有冲突，应以现有指南为准。

风格指南应当是动态更新的文档，如果你认为某项更改对所有人都有益，应当向现有风格指南和本指南提出修改建议。

> ##### *关于风格的争论毫无意义。应该有风格指南，并且你应该遵循它。*
> [_Rebecca Murphey_](https://rmurphey.com)

#### 项目的所有结构、资源和代码都应当像是由一个人创建的，无论有多少人参与。
在不同项目间切换时，不应当需要重新学习风格和结构。遵循风格指南可以消除不必要的猜测和歧义。

这也让开发和维护更加高效，因为无需思考风格，只需遵循指引。本指南以最佳实践为基础，遵循本指南也能最大程度减少难以追踪的问题。

#### 朋友不要让朋友有糟糕的风格。
如果你发现有人没有遵循风格指南，或没有风格指南，请尝试纠正他们。

在团队或社区中协作时，大家风格一致更容易互相帮助和沟通。没人愿意帮忙理清别人的“意大利面条代码”或处理难以理解命名的资源。

如果你在帮助一个遵循不同但一致且合理风格指南的人，你应当能够适应。如果他们没有任何风格指南，请引导他们阅读本指南。

<a name="importantterminology"></a>
### 1.2 重要术语

<a name="terms-prefab"></a>
#### 预制体（Prefab）
Unity 中的预制体是一种可以创建、配置并存储完整 GameObject（包括其所有组件、属性值和子 GameObject）为可复用资源的系统。

<a name="terms-level-map"></a>
#### 关卡/地图/场景
关卡指的是有些人称为地图（map），Unity 称为场景（Scene）的内容。一个关卡包含一组对象。

<a name="terms-serializable"></a>
#### 可序列化（Serializable）
可序列化的变量会显示在 Unity 的 Inspector 窗口中。更多信息请参见 Unity 关于 [Serializable](https://docs.unity3d.com/Manual/script-Serialization.html) 的文档。

<a name="terms-cases"></a>
#### 命名方式
有几种常见的命名方式：

> ##### PascalCase
> 每个单词首字母大写并去除空格，例如 `DesertEagle`、`StyleGuide`、`ASeriesOfWords`。
> 
> ##### camelCase
> 第一个字母小写，后续每个单词首字母大写，例如 `desertEagle`、`styleGuide`、`aSeriesOfWords`。
>  ##### 全小写（lowercase）
> 所有字母小写，例如 `deserteagle`。
>
> ##### 蛇形命名（Snake_case）
> 单词之间用下划线分隔，单词首字母可大写或小写，例如 `desert_Eagle`、`Style_Guide`、`a_Series_of_Words`。

**[⬆ 返回顶部](#table-of-contents)**

<a name="structure"></a>
## 2. 项目结构
项目的内容结构风格应当被视为法律。资源命名规范和内容目录结构相辅相成，违反任何一项都会造成混乱。

在本风格中，我们将使用一种更依赖于项目窗口过滤和搜索功能的结构，而不是另一种常见的将资源类型分组到文件夹中的结构。

> 使用 [资源命名规范](#anc) 中的前缀命名约定，使用文件夹来包含类似类型的资源，如 `Meshes`、`Textures` 和 `Materials` 是多余的，因为资源类型已经同时按前缀排序，并且可以在内容浏览器中过滤。

> 重要提示：开发资源（工作进行中或测试资源包含在 `_Dev` 中）应始终以 `_` 为前缀，以便在检查器中配置时易于查找。
<pre>
Assets
    <a name="#structure-developers">_Dev</a>(Use a `_`to keep this folder at the top)
        DeveloperName
            (Work in progress assets)
    <a name="structure-top-level">ProjectName</a>
	    Characters
            	Anakin
            FX
	    	Particles
                Vehicles
                    Abilities
                        IonCannon
                            (Particle Systems, Textures)
                Weapons
            Gameplay
                Characters
                Equipment
                Input
		Triggers
		Quests
		Scene
                Vehicles
                    Abilities
                    Air
                        TieFighter
                            (Models, Textures, Materials, Prefabs)
            <a name="#structure-levels">_Levels</a>
                Frontend
                Act1
                    Level1
            Lighting
                HDRI
                Lut
                Textures
            MaterialLibrary
            	Debug
            	Shaders
            Objects
                Architecture (Single use big objects)
                    DeathStar
                Props (Repeating objects to fill a level)
                    ObjectSets
                        DeathStar
            Scripts
                AI
                Gameplay
		    Triggers
		    Quests
                    Input
                Tools
            Sound
                Characters
                Vehicles
                    TieFighter
                        Abilities
                            Afterburners
                Weapons
            UI
                Art
                    Buttons
                Resources
                    Fonts
    ExpansionPack (DLC)
    Plugins
    ThirdPartySDK  
</pre>




本结构的原因在以下子节中列出。

### 章节

> 2.1 [文件夹名称](#structure-folder-names)

> 2.2 [顶级文件夹](#structure-top-level)

> 2.3 [开发者文件夹](#structure-developers)

> 2.4 [关卡](#levels)

> 2.5 [定义所有权](#structure-ownership)

> 2.6 [`Assets` 和 `AssetTypes`](#structure-assettypes)

> 2.7 [大型资源集](#structure-large-sets)

> 2.8 [材质库](#structure-material-library)

> 2.9 [场景结构](#scene-structure)


<a name="2.1"></a>
<a name="structure-folder-names"><a>
### 2.1 文件夹名称
这些是内容结构中任何文件夹的常见规则。

<a name="2.1.1"></a>
#### 始终使用 [PascalCase](#terms-cases)
PascalCase 指的是以大写字母开头，然后每个后续单词也以大写字母开头，例如 `DesertEagle`、`RocketPistol` 和 `ASeriesOfWords`。

<a name="2.1.2"></a>
#### 永远不要使用空格
重申 [2.1.1](#2.1.1)，永远不要使用空格。空格可能会导致各种工程工具和批处理过程失败。理想情况下，你的项目根目录也不应包含空格，例如 `D:\Project` 而不是 `C:\Users\My Name\My Documents\Unity Projects`。

<a name="2.1.3"></a>
#### 永远不要使用 Unicode 字符和符号
如果你的游戏角色名为 'Zoë'，其文件夹名称应为 `Zoe`。Unicode 字符在工程工具和某些应用程序中可能比空格更糟糕，而且某些应用程序不支持 Unicode 字符路径。

与此相关，如果你的项目有且你的计算机用户名有 Unicode 字符（例如你的名字是 `Zoë`），任何位于你的 `My Documents` 文件夹中的项目都会受到此问题的影响。通常只需将项目移动到 `D:\Project` 即可解决这些神秘问题。

使用 `a-z`、`A-Z` 和 `0-9` 以外的其他字符（如 `@`、`-`、`_`、`,`、`*` 和 `#`）也可能在其他平台、源代码控制和较弱的工程工具中导致意外且难以追踪的问题。 

<a name="structure-no-empty-folders"></a>
#### 没有空文件夹
内容浏览器中不应存在空文件夹。它们会污染内容浏览器。

如果你发现内容浏览器中有一个你无法删除的空文件夹，你应该执行以下操作：
1. 确保你正在使用源代码控制。
1. 导航到磁盘上的文件夹并删除其中的资源。
1. 关闭编辑器。
1. 确保你的源代码控制状态同步（例如，如果你使用 Perforce，请在内容目录上运行 Reconcile Offline Work）
1. 打开编辑器。确认一切正常。如果出现问题，请回滚，找出问题所在，然后重试。
1. 确保文件夹已消失。
1. 提交源代码控制更改。

<a name="2.2"></a>
<a name="structure-top-level"><a>
### 2.2 使用顶级文件夹存储项目特定资源
项目的所有资源都应存在于一个以项目名称命名的文件夹中。例如，如果你的项目名为“Generic Shooter”，其所有内容都应存在于 `Assets/GenericShooter` 中。

> `Developers` 文件夹不是项目依赖的资源，因此不是项目特定的。有关此的详细信息，请参见 [开发者文件夹](#2.3)。

有多个原因支持这种方法。

<a name="2.2.1"></a>
#### 没有全局资源
在代码风格指南中通常会写到你不应该污染全局命名空间，这与本指南遵循相同的原则。当允许资源存在于项目文件夹之外时，通常很难强制执行严格的结构布局，因为不在文件夹中的资源会鼓励不良行为，即不组织资源。

每个资源都应有其目的，否则它不应属于项目。如果资源是实验性的测试，不应属于项目，则应将其放入 [`Developer`](#2.3) 文件夹中。

<a name="2.2.2"></a>
#### 减少迁移冲突
在多个项目中工作时，团队通常会从项目复制资源到另一个项目，如果他们为两个项目都做了一些有用的事情。 

通过将所有项目特定资源放置在顶级文件夹中，可以减少导入这些资源时发生迁移冲突的可能性。

<a name="2.2.2e1"></a>
##### 主材质示例
例如，假设你在某个项目中创建了一个主材质，你希望在另一个项目中使用它，你迁移了该资源。如果此资源不在顶级文件夹中，其名称可能类似于 `Assets/MaterialLibrary/M_Master`。如果目标项目没有主材质，这应该没有问题。

随着一个或两个项目的发展，它们各自的 Master 材质可能会根据正常开发过程进行调整，以适应其特定项目。

当出现这种情况时，例如，一个项目中的艺术家创建了一个漂亮的通用静态网格集，另一个人希望将该静态网格集包含在第二个项目中。如果艺术家创建的资源使用了基于 `Assets/MaterialLibrary/M_Master` 的材质实例，当执行迁移时，以前迁移的 `Assets/MaterialLibrary/M_Master` 资源有很大几率发生冲突。

这个问题很难预测且难以处理。迁移静态网格的人可能不是熟悉两个项目 Master 材质开发的人，他们可能甚至不知道这些静态网格依赖于材质实例，而这些材质实例又依赖于主材质。迁移工具需要整个依赖链才能正常工作，因此它将被迫在复制这些资源到另一个项目时抓取 `Assets/MaterialLibrary/M_Master`，并覆盖现有资源。

如果两个项目的 Master 材质在 _任何_ 方面不兼容，你都有可能破坏项目中所有依赖项，以及可能已经迁移的依赖项，仅仅因为资源没有存储在顶级文件夹中。简单的静态网格迁移现在变得非常困难。

<a name="2.2.3"></a>
#### 样本、模板和第三方内容是风险零
[2.2.2](#2.2.2) 的扩展，如果团队成员决定添加样本内容、模板文件或从第三方购买的资产，则可以保证这些新资产不会以任何方式干扰项目，除非你的项目顶级文件夹未被唯一命名。

你不能信任第三方内容完全符合 [顶级文件夹规则](#2.2)。存在许多资源，其大部分内容位于顶级文件夹，但也可能包含可能修改的 Unity 样本内容以及污染全局 `Assets` 文件夹的关卡文件。

在遵循 [2.2](#2.2) 时，你遇到的最糟糕的第三方冲突是，如果两个第三方资产都具有相同的样本内容。如果你的所有资源都在项目特定文件夹中，包括你移动到文件夹中的样本内容，你的项目将永远不会崩溃。

#### DLC、子项目和补丁易于维护
如果你的项目计划发布 DLC 或与多个子项目相关联，这些项目可能需要迁移或简单地不进行烹饪，与项目相关的资源应具有其自己的顶级内容文件夹。这使得烹饪 DLC 与主项目内容分离变得更容易。子项目可以轻松迁移。如果你需要更改资产的材质或添加一些非常特定的资产覆盖行为，你可以轻松地将这些更改放入补丁文件夹中，并安全地工作，而不会破坏核心项目。

<a name="2.3"></a>
<a name="structure-developers"></a>
### 2.3 使用开发者文件夹进行本地测试
在项目开发过程中，团队成员通常会有一个“沙盒”，他们可以自由地进行实验，而不会影响核心项目。由于这项工作可能正在进行中，这些团队成员可能希望将其资产放在项目源代码控制服务器上。并非所有团队都需要使用开发者文件夹，但使用它们通常会遇到一个常见问题，即团队成员意外使用了尚未准备好的资源，这将在这些资源被移除时导致问题。例如，艺术家可能正在迭代一个模块化的静态网格集，并且仍在调整其尺寸和网格对齐。如果世界构建者看到这些资源在主项目文件夹中，他们可能会在整个关卡中使用它们，而不知道它们可能会经历巨大的变化或被移除。这导致团队中的每个人都必须重新处理，以解决这个问题。

如果这些模块化资源被放置在开发者文件夹中，世界构建者将永远没有理由使用它们，整个问题将永远不会发生。

一旦资源准备就绪，艺术家只需将资源移动到项目特定文件夹中。这本质上就是将资源从实验性提升到生产性。


<a name="levels"></a>
### 2.4 所有 [场景](#terms-level-map) 文件都应包含在名为 Levels 的文件夹中
关卡文件非常特殊，几乎每个项目都有自己的地图命名系统，特别是当它们处理子关卡或流式关卡时。无论特定项目使用哪种地图组织系统，所有关卡都应位于 `Assets/ProjectNameName/Levels` 中。

能够告诉某人打开一个特定的地图而不必解释它在哪，是一个很好的时间节省和一般“质量生活”改进。关卡通常位于 `Levels` 的子文件夹中，例如 `Levels/Campaign1/` 或 `Levels/Arenas`，但这里最重要的是它们都存在于 `Assets/ProjectNameName/Levels` 中。

这也简化了工程师的烹饪工作。整理关卡进行构建过程可能非常令人沮丧，如果他们必须从任意文件夹中挖掘它们。如果一个团队的所有关卡都在一个地方，则更容易在构建过程中意外地不烹饪地图。它也简化了照明构建脚本和 QA 过程。

<a name="2.5"></a>
<a name="structure-ownership"></a>
### 2.5 定义所有权
在多于一个人的团队中，定义区域/资源/功能的所有权。一些资源（如场景或预制体）在多个同时更改时不太好，导致冲突。拥有一个可以更改（或授予更改权限）给定资源的单个人有助于避免这个问题。

<a name="2.6"></a>
<a name="structure-assettypes"></a>
### 2.6 不要创建名为 `Assets` 或 `AssetTypes` 的文件夹

<a name="2.6.1"></a>
#### 创建名为 `Assets` 的文件夹是多余的。
所有资源都是资源。

<a name="2.6.2"></a>
#### 创建名为 `Meshes`、`Textures` 或 `Materials` 的文件夹是多余的。
所有资源名称都考虑了其资源类型。这些文件夹只提供冗余信息，并且可以使用内容浏览器提供的强大且易于使用的过滤系统来替换。

想要只查看 `Environment/Rocks/` 中的静态网格？只需打开静态网格过滤器。如果所有资源名称正确，它们也将按字母顺序排序，无论前缀如何。想要同时查看静态网格和骨骼网格？只需打开两个过滤器。这消除了在内容浏览器树视图中选择两个文件夹的必要性。

> 这也大大减少了资产的完整路径名。静态网格的 `SM_` 前缀只有三个字符，而 `Meshes/` 有七个字符。

不这样做也阻止了不可避免地有人将静态网格或纹理放入 `Materials` 文件夹中。

<a name="2.7"></a>
<a name="structure-large-sets"></a>
### 2.7 大型资源集拥有自己的文件夹布局

这可以看作是 [2.6](#2.6) 的伪例外。

某些资源类型具有大量相关文件，其中每个资源都有其独特目的。最常见的是动画和音频资源。如果你发现自己有 15 个或更多这些资源，它们应该在一起。

例如，跨多个角色的动画应位于 `Characters/Common/Animations` 中，可能包含子文件夹，如 `Locomotion` 或 `Cinematic`。

> 这不适用于纹理和材质。通常，如果 `Rocks` 文件夹中有大量纹理，如果有很多岩石，这些纹理通常只与少量特定岩石相关，并且应该有适当的名称。即使这些纹理是 [材质库](#2.8) 的一部分。

<a name="2.8"></a>
<a name="structure-material-library"></a>
### 2.8 `MaterialLibrary`

如果你的项目使用主材质、分层材质或任何形式的可重用材质或纹理，这些资源应位于 `Assets/ProjectName/MaterialLibrary` 中。

这样所有“全局”材质都有一个栖息地，并且易于定位。

> 这也使得在项目中强制执行“仅使用材质实例”策略变得非常容易。如果所有艺术家和资源都应使用材质实例，那么该文件夹中唯一应存在的常规材质资源。你可以轻松验证这一点，只需在任何不是 `MaterialLibrary` 的文件夹中搜索基础材质。

材质库不一定要由纯材质组成。共享实用纹理、材质函数和此类事物也应存储在此，并包含在指定其用途的文件夹中。例如，通用噪声纹理应位于 `MaterialLibrary/Utility` 中。

任何测试或调试材料都应位于 `MaterialLibrary/Debug` 中。这使得调试材料可以轻松从项目中移除，并使其非常明显，如果生产资产在使用它们时出现引用错误。

<a name="2.9"></a>
<a name="scene-structure"></a>
## 2.9 场景结构
在项目层次结构旁边，还有场景层次结构。与之前一样，我们将为你提供一个模板。你可以根据需要调整它。使用命名空游戏对象作为场景文件夹。

<pre>
@System
@Debug
@Management
@UI
    Layouts
Cameras
Lights
    Volumes
Particles
Sound
World
    Global
    Room1
        Architecture
        Terrain
        Props
Gameplay
	Actors
	Items
	Triggers
	Quests
_Dynamic
</pre>

 - 所有空对象都应位于 0,0,0 处，并带有默认旋转和缩放。
 - 对于仅包含脚本的空对象，请使用“@”作为前缀 – 例如 @Cheats
 - 当你在运行时实例化对象时，请确保将其放入 _Dynamic – 不要污染你的层次结构或你将发现难以导航。

**[⬆ 返回顶部](#table-of-contents)**

<a name="scripts"></a>

## 3. 脚本

本节将重点介绍 C# 类及其内部结构。在可能的情况下，样式规则遵循 Microsoft 的 C# 标准。

### 章节
> 3.1 [类组织](#classorganization)

> 3.2 [编译](#compiling)

> 3.3 [变量](#variables)

> 3.4 [函数](#functions)

<a name="classorganization"></a>
### 3.1 类组织
源文件应只包含一个公共类型，尽管允许内部类。

源文件应使用公共类的名称命名。

组织命名空间，

类成员应按字母顺序分组，并分为以下部分：
* 常量字段
* 静态字段
* 字段
* 构造函数
* 属性
* 事件 / 委托
* 生命周期方法 (Awake, OnEnable, OnDisable, OnDestroy)
* 公共方法
* 私有方法
* 嵌套类型

在每个组中按访问权限排序：
* public
* internal
* protected
* private
```
namespace ProjectName
{
	/// <summary>  
	/// 类的主要功能概述
	/// </summary>
    public class Account
    {
      #region Fields
      
      [Tooltip("在检查器中设置的公共变量，应带有 Tooltip")]
      public static string BankName;
      
	  /// <summary>  
	  /// 它们也应该有总结
	  /// </summary>
      public static decimal Reserves;
 
	  public string BankName;
	  public const string ShippingType = "DropShip";
	  
	  private float _timeToDie;
	  
	  #endregion
	  
	  #region Properties
	  
      public string Number {get; set;}
      public DateTime DateOpened {get; set;}
      public DateTime DateClosed {get; set;}
      public decimal Balance {get; set;}
            
	  #endregion
	 
	  #region LifeCycle
	  
      public Awake()
      {
        // ...
      }
      
      #endregion
	  #region Public Methods
	  
      public AddObjectToBank()
      {
        // ...
      }
      
      #endregion
    }
}
```

#### 脚本模板
为了节省时间，你可以覆盖 Unity 的默认脚本模板，以自动设置命名空间和区域等。请参阅此 Unity [支持](https://support.unity3d.com/hc/en-us/articles/210223733-How-to-customize-Unity-script-templates) 文章，了解如何。

<a name="namespace"></a>
#### 命名空间
使用命名空间确保你的类/枚举/接口/等不会与来自其他命名空间或全局命名空间的现有命名空间冲突。项目至少应使用项目名称作为命名空间，以防止与任何导入的第三方资产发生冲突。

#### 所有公共函数都应有总结

简单来说，任何具有公共访问修饰符的函数都应有其总结。 

```
/// <summary>
/// 开枪
/// </summary>
public void Fire()
{
// 开枪。
}
```

#### 折叠组
如果一个类只有少量变量，则不需要折叠组。

如果一个类有中等数量的变量（5-10），所有 [可序列化](#serializable) 变量都应分配一个非默认的折叠组。一个常见的类别是 `Config`。

要创建折叠组，Unity 有两种选择。 

* 第一种是在主类中定义一个 `[Serializable] public Class`，但这可能会影响性能。这允许使用相同的变量名共享。
* 第二种是使用 [Odin Inspector](https://odininspector.com/) 提供的折叠组属性。

```
[[Serializable](https://docs.unity3d.com/ScriptReference/Serializable.html)]
public struct PlayerStats
	{
        public int MovementSpeed;
    }
    
[FoldoutGroup("Interactable")]
public int MovementSpeed = 1;
```

#### 注释
注释应用于描述意图、算法概述和/或逻辑流程。
理想情况下，从阅读注释中，除了作者之外，其他人也能理解函数的目的和一般操作。

虽然没有最小注释要求，确实一些非常小的例程不需要注释，但希望大多数例程都有注释，反映程序员的意图和方法。

##### 注释风格
将注释放在单独的行上，而不是代码行末尾。

注释文本以大写字母开头。

注释文本以句号结尾。

在注释分隔符（//）和注释文本之间插入一个空格，如以下示例所示。

注释标签 // (两个斜杠) 样式应尽可能使用。在可能的情况下，将注释放在代码上方，而不是旁边。以下是一些示例：
```
        // 示例变量注释。
        private int _myInt = 5;
```

#### 区域
`#region` 指令使你能够折叠和隐藏 C# 文件中的代码段。选择性隐藏代码使你的文件更易于管理和阅读。 
```
#region "这是要折叠的代码"
    Private components As System.ComponentModel.Container
#endregion
```

#### 间距
使用逗号后跟一个空格在函数参数之间。

示例：`Console.In.Read(myChar, 0, 1);`
* 不要在括号和函数参数之间使用空格。
* 不要在函数名和括号之间使用空格。
* 不要在括号内使用空格。
<a name="3.1"></a>
<a name="compiling"></a>
### 3.2 编译
所有脚本都应零警告和零错误编译。你应该立即修复脚本警告和错误，因为它们可以快速级联到非常可怕的意外行为。

不要提交损坏的脚本到源代码控制。如果你必须将它们存储在源代码控制中，请搁置它们。

### 3.3 变量
`variable` 和 `property` 这两个词可以互换使用。

#### 变量命名

##### 名词
所有非布尔变量名称必须清晰、明确、描述性。 

##### 大小写
所有变量都使用 PascalCase，除非标记为 [private](#privatevariables)，否则使用 camelCase。 

使用 PascalCase 缩写 4 个字符或更多（3 个字符都是大写）。

##### 考虑上下文
所有变量名称都不得与其上下文冗余。

###### 考虑上下文示例：
考虑一个名为 `PlayerCharacter` 的类。

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

所有这些变量名称都是冗余的。它暗示变量代表它所属的 `PlayerCharacter`，因为 `PlayerCharacter` 定义了这些变量。

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

#### 变量访问级别
在 C# 中，变量具有访问级别概念。公共意味着任何代码都可以访问变量。受保护意味着只有类及其子类可以访问此变量。私有意味着只有此变量及其子类无法访问。
变量应仅在必要时公开。

建议使用 `[SerializeField]` 属性而不是公开变量。

##### 局部变量
局部变量应使用 camelCase。

###### 隐式类型局部变量
当变量类型从赋值的右侧明显可见，或者当精确类型不重要时，使用隐式类型。
```
var var1 = "This is clearly a string.";
var var2 = 27;
var var3 = Convert.ToInt32(Console.ReadLine());
// 也用于 for 循环
for (var i = 0; i < bountyHunterFleets.Length; ++i) {};
```

不要在变量类型不明显时使用 var。
示例
```
int var4 = ExampleClass.ResultSoFar();
```

<a name="privatevariables"></a>
##### 私有变量
私有变量应以 `_` 为前缀，并使用 camelCase。

除非已知变量应在定义它的类中访问，而不能是子类，否则不要将变量标记为私有。直到变量能够被标记 `protected`，请保留私有，以确保你知道你想要限制子类使用。

##### 不要使用匈牙利符号
不要在标识符中使用匈牙利符号或任何其他类型标识。
```
// Correct
int counter;
string name;
 
// Avoid
int iCounter;
string strName;
```

#### 可在编辑器中访问的变量

##### 工具提示 
所有 [可序列化](#serializable) 变量都应在 `[Tooltip]` 字段中有一个描述，解释更改此值如何影响脚本的行为。

##### 变量滑块和值范围
所有 [可序列化](#serializable) 变量都应使用滑块和值范围，如果变量不应设置为某个值，则应使用 `[Range(min, max)]` 标记。

示例：一个生成围栏柱的脚本可能有一个可编辑变量 `PostsCount` 和一个值 -1 没有意义。使用 `[Range(min, max)]` 标记 0 作为最小值。

如果一个可编辑变量在构造脚本中使用，它应该有一个合理的滑块范围定义，以便某人不能意外地为其分配一个非常大的值，这可能会崩溃编辑器。

值范围仅在知道值的边界时定义。虽然滑块范围防止意外的大量输入，但未定义的值范围允许用户指定超出滑块范围的值，这可能被认为是“危险”但仍然有效。

#### 变量类型

##### 布尔值

###### 布尔前缀
所有布尔值都应以 PascalCase 开头，并带有一个动词。

示例：使用 `isDead` 和 `hasItem`，**不** 使用 `Dead` 和 `Item`。

###### 布尔名称
所有布尔值都应尽可能描述性地命名，如果表示一般信息。

尝试不使用像 `isRunning` 这样的动词。动词往往会导致复杂的状态。

###### 布尔复杂状态
不要使用布尔值来表示复杂和/或依赖的状态。这使得添加和删除状态变得复杂，并且不再易于阅读。使用枚举代替。

示例：定义武器时，**不** 使用 `isReloading` 和 `isEquipping`，如果武器不能同时重新加载和装备。定义一个名为 `WeaponState` 的枚举，并使用一个名为 `WeaponState` 的变量，而不是这个类型。这使得添加新武器状态变得容易得多。

##### 枚举
枚举使用 PascalCase 并使用单数名称作为枚举和它们的值。例外：位字段枚举应为复数。枚举可以放置在类空间之外，以提供全局访问。

示例： 
```
public enum WeaponType
{
    Knife,
    Gun
}

// 枚举可以有多个值
[Flags]
public enum Dockings
{
	None = 0,
	Top = 1,
}

public WeaponType Weapon
```

##### 数组
数组遵循与上述相同的命名规则，但应为复数名词。

示例：使用 `Targets`、`Hats` 和 `EnemyPlayers`，**不** 使用 `TargetList`、`HatArray`、`EnemyPlayerArray`。

##### 接口
接口以大写字母 `I` 开头，然后是 PascalCase。

示例：```public interface ICanEat { }```

<a name="functions"></a>
### 3.4 函数、事件和事件调度器
本节描述了如何编写函数、事件和事件调度器。所有适用于函数的内容也适用于事件，除非另有说明。

#### 函数命名
函数、事件和事件调度器的命名至关重要。仅根据名称，某些假设可以做出关于函数。例如：

* 它是一个纯函数吗？
* 它是否获取状态信息？
* 它是一个处理程序吗？
* 它的目的是什么？

这些问题和更多问题都可以通过适当的函数命名来回答。

<a name="function-verbrule"></a>
#### 所有函数都应为动词
所有函数和事件执行某种动作，无论是获取信息、计算数据还是导致某些东西爆炸。因此，所有函数都应以动词开头。它们应该尽可能使用现在时。它们还应该有一些上下文来解释它们在做什么。

好的例子：

* `Fire` - 好的例子，如果在一个 Character / Weapon 类中，因为它有上下文。不好的例子，如果在一个 Barrel / Grass / 任何模糊的类中。
* `Jump` - 好的例子，如果在一个 Character 类中，否则需要上下文。
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" 是一个动词。](http://writingexplained.org/is-is-a-verb)

坏的例子：

* `Dead` - 是死的？会死吗？
* `Rock`
* `ProcessData` - 含糊不清，这些词没有意义。
* `PlayerState` - 名词含糊不清。
* `Color` - 动词没有上下文，或模糊名词。

#### 返回布尔值的函数应提问
在编写一个不改变状态或修改任何对象且纯粹用于获取信息、状态或计算是/否值的函数时，它应该提问。这也应遵循 [动词规则](#function-verbrule)。

这极其重要，因为如果问题没有被问到，它可能会被认为函数执行了一个动作并返回了该动作是否成功。

好的例子：

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" 是一个动词。](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" 是 "be" 的过去时。](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) 当引用“上一帧”或“上一状态”时使用“was”。
* `CanReload` - ["Can" 是一个动词。](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

坏的例子：

* `Fire` - 是着火吗？会开火吗？做火？
* `OnFire` - 可能与事件调度器混淆。
* `Dead` - 是死的？会死吗？
* `Visibility` - 是可见的？设置可见性？飞行条件描述？

#### 事件处理程序和调度器应以 `On` 开头
任何处理事件或调度事件的函数都应以 `On` 开头，并继续遵循 [动词规则](#function-verbrule)。

好的例子：

* `OnDeath` - 游戏中的常见搭配
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

坏的例子：

* `OnData`
* `OnTarget`

**[⬆ 返回顶部](#table-of-contents)**
<a name="anc"></a>
<a name="4"></a>

## 4. 资源命名规范
资源命名规范应被视为法律。遵循命名规范的项目可以轻松管理其资源、搜索、解析和维护。

大多数事物都以前缀开头，通常是资产类型缩写后跟下划线。

**资源使用 [PascalCase](#cases)**

<a name="base-asset-name"></a>
<a name="4.1"></a>
### 4.1 基础资产名称 - `Prefix_BaseAssetName_Variant_Suffix`
所有资源都应有 _基础资产名称_。基础资产名称代表一组相关资源的逻辑分组。任何属于此逻辑组的资源 
都应遵循 `Prefix_BaseAssetName_Variant_Suffix` 的标准。

牢记 `Prefix_BaseAssetName_Variant_Suffix` 的规律，并使用常识通常足以保证良好的资产名称。以下是一些关于每个元素的详细规则。

`Prefix` 和 `Suffix` 由 [资源命名修饰符](#asset-name-modifiers) 表决定。

`BaseAssetName` 应由简短且易于识别的名称决定，该名称与该组资源的相关上下文有关。例如，如果你有一个名为 Bob 的角色，所有 Bob 的资源都应有 `BaseAssetName` 为 `Bob`。

对于独特的特定变体资源，`Variant` 是短且易于识别的名称，表示逻辑上属于一组资源的子集。例如，如果 Bob 有多个皮肤，这些皮肤应仍使用 `Bob` 作为 `BaseAssetName`，但应包含一个可识别的 `Variant`。一个“邪恶”皮肤应称为 `Bob_Evil`，一个“复古”皮肤应称为 `Bob_Retro`。

对于独特的通用变体资源，`Variant` 是一个两位数字，从 `01` 开始。例如，如果你有一个环境艺术家生成非描述性岩石，它们应命名为 `Rock_01`、`Rock_02`、`Rock_03` 等。除了极少数例外，你不应该要求三位数的变体编号。如果你有超过 100 个资源，你应该考虑使用不同的基础名称或多个变体名称。

根据你的资源变体生成方式，你可以将变体名称串联起来。例如，如果你正在为 Arch Viz 项目创建地板资产，你应该使用基础名称 `Flooring` 和链式变体，如 `Flooring_Marble_01`、`Flooring_Maple_01`、`Flooring_Tile_Squares_01`。

<a name="1.1-examples"></a>
#### 示例

##### 角色

| 资产类型               | 资产名称   |
| ------------------------ | ------------ |
| 骨骼网格（Skeletal Mesh）            | SK_Bob       |
| 材质（Material）                 | M_Bob        |
| 纹理（Texture）（漫反射/Albedo） | T_Bob_D      |
| 纹理（Texture）（法线）         | T_Bob_N      |
| 纹理（Texture）（邪恶漫反射）   | T_Bob_Evil_D |

##### 道具

| 资产类型               | 资产名称   |
| ------------------------ | ------------ |
| 静态网格（01）         | SM_Rock_01   |
| 静态网格（02）         | SM_Rock_02   |
| 静态网格（03）         | SM_Rock_03   |
| 材质（Material）                 | M_Rock       |
| 材质实例（雪）（Material Instance） | MI_Rock_Snow |

<a name="asset-name-modifiers"></a>
### 4.2 资源命名修饰符

命名资源时使用这些表来确定资源的前缀和后缀。

#### 章节

> 4.2.1 [最常见](#anc-common)

> 4.2.2 [动画](#anc-animations)

> 4.2.3 [人工智能](#anc-ai)

> 4.2.4 [预制体](#anc-prefab)

> 4.2.5 [材质](#anc-materials)

> 4.2.6 [纹理](#anc-textures)

> 4.2.7 [杂项](#anc-misc)

> 4.2.8 [物理](#anc-physics)

> 4.2.9 [音频](#anc-audio)

> 4.2.10 [用户界面](#anc-ui)

> 4.2.11 [效果](#anc-effects)

<a name="anc-common"></a>
#### 最常见

| 资产类型              | 前缀     | 后缀     | 备注                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| 关卡/场景           |  *          |            | [应包含在名为 Levels 的文件夹中。](#levels) 例如 `Levels/A4_C17_Parking_Garage.unity` |
| 关卡（持久化）      |            | _P         |                                  |
| 关卡（音频）           |            | _Audio     |                                  |
| 关卡（照明）        |            | _Lighting  |                                  |
| 关卡（几何）        |            | _Geo       |                                  |
| 关卡（游戏玩法）        |            | _Gameplay  |                                  |
| 预制体                  |        |            |                                  |
| 探针（反射）      | RP_        |            |                                  |
| 探针（灯光）           | LP_        |            |                                  |
| 体积                  | V_         |            |                                  |
| 触发区域            |            | _Trigger   |                                  |
| 材质                | M_         |            |                                  |
| 静态网格             | SM_       |            |                                  |
| 骨骼网格           | SK_       |            |                                  |
| 纹理                 | T_         | _?         | 参见 [纹理](#anc-textures)    |
| 视觉特效          | VFX_       |            |                                  |
| 粒子系统         | PS_       |            |                                  |
| 灯光                   | L_         |            |                                  |
| 相机（Cinemachine）    | CM_         |            | 虚拟相机                   |

<a name="anc-models"></a>

#### 4.2.1a 3D 模型 (FBX 文件)

PascalCase

| 资产类型    | 前缀 | 后缀 | 备注 |
| ------------- | ------ | ------ | ----- |
| 角色    | CH_    |        |       |
| 载具      | VH_    |        |       |
| 武器       | WP_    |        |       |
| 静态网格   | SM_    |        |       |
| 骨骼网格 | SK_    |        |       |
| 骨骼      | SKEL_  |        |       |
| 绑定      | RIG_   |        |       |

#### 4.2.1b 3d 模型 (3ds Max)

3ds Max 中的所有网格都是小写的，以区分它们与 FBX 导出。

| 资产类型    | 前缀 | 后缀      | 备注                                   |
| ------------- | ------ | ----------- | --------------------------------------- |
| 网格          |        | _mesh_lod0* | 仅当模型使用 LOD 时使用 LOD 后缀 |
| 网格碰撞器 |        | _collider   |                                         |

<a name="anc-animations"></a>

#### 4.2.2 动画 
| 资产类型           | 前缀 | 后缀 | 备注 |
| -------------------- | ------ | ------ | ----- |
| 动画剪辑       | A_     |        |       |
| 动画控制器 | AC_    |        |       |
| 头像遮罩          | AM_    |        |       |
| 变形目标         | MT_    |        |       |

<a name="anc-ai"></a>
#### 4.2.3 人工智能

| 资产类型              | 前缀     | 后缀     | 备注                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| AI / NPC                | AI_        |  _NPC          |   *Npc 可能是 CH_ !AI_ 的 pawn                          |
| 行为树           | BT_      |            |                                  |
| 黑板              | BB_       |            |                                  |
| 装饰器               | BTDecorator_ |          |                                  |
| 服务                 | BTService_ |            |                                  |
| 任务                    | BTTask_  |            |                                  |
| 环境查询       | EQS_     |            |                                  |
| 环境查询上下文         | EQS_     | Context    |                                  |

<a name="anc-prefab"></a>
#### 4.2.4 预制体

| 资产类型              | 前缀     | 后缀     | 备注                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| 预制体         |        |            |                                  |
| 预制体实例         | I       |            |                                  |
| 可脚本对象       |     |        | 在编辑器中分配 "蓝图" 标签 |

<a name="anc-materials"></a>

#### 4.2.5 材质
| 资产类型        | 前缀 | 后缀 | 备注 |
| ----------------- | ------ | ------ | ----- |
| 材质          | M_     |        |       |
| 材质实例 | MI_    |        |       |
| 物理材质 | PM_    |        |       |
| 材质着色器图 | MSG_    |        |       |

<a name="anc-textures"></a>

#### 4.2.6 纹理
| 资产类型              | 前缀     | 后缀     | 备注                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| 纹理                 | T_         |            |                                  |
| 纹理（基础色）    | T_         | _BC         | 漫反射 / Albedo     	       |
| 纹理（金属/光滑度）| T_  | _MS        |                                  |
| 纹理（法线）        | T_         | _N         |                                  |
| 纹理（Alpha）         | T_         | _A         |                                  |
| 纹理（高度）          | T_         | _H         |                                  |
| 纹理（环境光遮蔽） | T_     | _AO      |                                  |
| 纹理（自发光）      | T_         | _E         |                                  |
| 纹理（遮罩）          | T_         | _M         |                                  |
| 纹理（打包）        | T_         | _*         | 参见 [纹理打包](#anc-textures-packing) 关于 [打包](#anc-textures-packing) 的说明。 |
| 纹理立方体            | TC_       |            |                                  |
| 媒体纹理           | MT_       |            |                                  |
| 渲染目标           | RT_       |            |                                  |
| 立方渲染目标      | RTC_     |            |                                  |
| 纹理光照配置文件   | TLP_     |            |                                  |

<a name="anc-textures-packing"></a>

#### 4.2.6.1 纹理打包
打包多个纹理数据层到一张纹理中是一种常见做法。例如，将 Emissive、Roughness、Ambient Occlusion 打包到纹理的红色、绿色和蓝色通道中。要确定后缀，只需将上述后缀字母堆叠在一起，例如 `_ERO`。

> 通常可以接受在漫反射/Albedo 的 Alpha 通道中包含 Alpha/Opacity 层，因为这是常见做法，添加 `A` 到 `_D` 后缀是可选的。

将 4 个通道的数据打包到纹理中（RGBA）不推荐，除非漫反射/Albedo 的 Alpha 通道中有一个 Alpha/Opacity 遮罩，因为带有 Alpha 通道的纹理比不带 Alpha 通道的纹理开销更大。
<a name="anc-misc"></a>

#### 4.2.7 杂项

| 资产类型                      | 前缀 | 后缀 | 备注 |
| ------------------------------- | ------ | ------ | ----- |
| 通用渲染管线资源 | URP_   |        |       |
| HD 渲染管线资源        | HDRP_  |        |       |
| 后期处理体积配置文件     | PP_    |        |       |
| 用户界面                  | UI_    |        |       |

<a name="anc-physics"></a>
#### 4.2.8 物理

| 资产类型        | 前缀 | 后缀 | 备注 |
| ----------------- | ------ | ------ | ----- |
| 物理材质 | PM_    |        |       |

<a name="anc-audio"></a>

#### 4.2.9 音频

| 资产类型     | 前缀 | 后缀 | 备注                                                        |
| -------------- | ------ | ------ | ------------------------------------------------------------ |
| 音频剪辑     | A_     |        |                                                              |
| 音频混音器    | MIX_   |        |                                                              |
| 对话语音 | DV_    |        |                                                              |
| 音频类    |        |        | 无前缀/后缀。应放入名为 AudioClasses 的文件夹中 |

<a name="anc-ui"></a>
#### 4.2.10 用户界面
| 资产类型       | 前缀 | 后缀 | 备注 |
| ---------------- | ------ | ------ | ----- |
| 字体             | Font_  |        |       |
| 纹理（精灵） | T_     | _GUI   |       |

<a name="anc-effects"></a>
#### 4.2.11 效果
| 资产类型      | 前缀 | 后缀 | 备注 |
| --------------- | ------ | ------ | ----- |
| 粒子系统 | PS_    |        |       |
**[⬆ 返回顶部](#table-of-contents)**

<a name="asset-workflows"></a>

## 5. 资源工作流程

本节描述了创建和导入可在 Unity 中使用的资源的最佳实践。

<a name="toc"></a>
### 章节

> 5.1 [Unity 资源导入设置](#unityimport)
>
> 5.2 [3ds Max](#3dsmax)
>
> 5.3 [纹理](#textures)
>
> 5.4 [音频](#audio)

<a name="unityimport"></a>

### 5.1 Unity 资源导入设置

Unity 的 [AssetPostprocessor](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) 允许你挂钩导入管道并运行脚本，在资源首次导入项目之前或之后。这使你能够在资源首次导入项目时强制执行导入设置。例如，纹理以 `_N` 结尾的可以标记为法线贴图。

示例导入设置指南：

https://github.com/justinwasilenko/Unity-AssetPostProcessor

<a name="3dsmax"></a>
### 5.2 3ds Max

Unity 从 3ds Max 导入指南：

https://docs.unity3d.com/2017.4/Documentation/Manual/HOWTO-ImportObjectMax.html

Unity 教程 FBX 导出包的 FBX 往返：

https://learn.unity.com/project/3ds-max-to-unity-pipeline

#### 设置 3ds Max

Unity 使用 1 单位 = 1 米。设置 3ds Max 以使用米，方法是转到 ```Customize/Units Setup/System Unit Setup``` 并将其设置为 1 单位 = 1 米。使用正确的缩放非常重要，以确保正确的物理 / GI / 和 VR 交互。

3ds Max 中的动画帧率应设置为 30fps。```Time Configuration``` 对话框有 3ds Max 的 FPS 设置

##### 处理小物体

* 将 ```Customize > Customize User Interface > Mouse Wheel Zoom Increment``` 设置为 0.1m 以停止过度缩放

* 打开视口裁剪并设置视口侧面的滑块，以便能够放大查看小网格。(https://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/sfdcarticles/sfdcarticles/Viewport-Clipping.html)

#### 在 3ds Max 中建模

* 遵循 [资源命名规范](#anc-models)
* 避免超长细三角形（加速平铺渲染器和帮助 GI 烘焙）
* 使用面积和角度加权网格法线（Unity 导入设置或创建于 3ds Max）

#### 从 3ds Max 导出到 Unity

##### 导出设置：

- 三角化 On
- 切线与副切线 Off
- 平滑组 On
- 保留边缘方向 On
- 单位 - 自动 Off / 场景单位转换为米
- 轴转换 Z 向上

3ds Max 中创建的模型使用与 Unity 不同的坐标系。模型需要在其 X 轴上旋转 +90 度才能正确导入到 Unity。

要快速完成，请打开 MaxScript 编辑器，粘贴此代码，选择并拖动此代码到 3ds Max 工具栏以创建一个按钮，该按钮将运行此脚本。它应用 Xform 修改器来旋转枢轴。

```
fn RotateCreationPivot obj rot =
(
select obj
modPanel.addModToSelection (XForm ()) ui:on
obj.modifiers[#XForm].gizmo.rotation += rot as quat
rotate obj (inverse rot as quat)
)
RotateCreationPivot $ (eulerToQuat(eulerAngles 90 0 0))
```


批量导出器 3ds Max (http://www.strichnet.com/improving-the-fbx-workflow-between-3ds-max-and-unity3d/)

##### 导出 CAT 动画到 FBX

绑定正常骨骼到 CAT 骨架以用于蒙皮和导出

###### 绑定姿势

将 Motion Panel/Layer Manager/"Setup/Animation Mode" 切换到 ```Red```
仅选择骨骼和网格，你想导出
导出命名：ModelName.FBX

###### 动画

将 Motion Panel/Layer Manager/"Setup/Animation Mode" 设置为 ```Green```
仅选择层次结构中需要的骨骼（这些应与绑定姿势完全相同的骨骼），不要包含网格。
导出命名：ModelName@AnimationName.FBX
@ 符号是 Unity 命名约定的一个特殊符号，允许动画绑定到 Unity 编辑器中的 Human.fbx

#### 从 3ds Max 导入到 Unity

如果仅导入动画或骨骼从 FBX： 

* 设置 ```Preserve Hierarchy Model``` 导入选项为 ```True```
* 设置 ```Rig > Avatar Definition``` 为 ```Copy From Other Avatar```

MaxListener 窗口，设置选定骨骼的宽度和高度，可能也设置对象？
$.width = 0.01
$.height = 0.01

**[⬆ 返回顶部](#table-of-contents)**

<a name="textures"></a>
### 5.3 纹理

* 纹理遵循上面找到的 [资源命名规范](#anc-textures)。 
* 它们是 2 的幂（例如，512 x 512 或 256 x 1024）。
* 尽可能使用纹理集。
* 3D 软件应指向 Unity 项目纹理以保持一致性，当你保存或导出时。
* 如果游戏纹理分辨率已知，最好在 Photoshop 中调整纹理大小，而不是使用 Unity 的压缩选项。这可以减少文件大小和纹理导入时间。
* 当在高分辨率 PSD 外部你的 Unity 项目中工作时，请为高分辨率纹理和导入的 Unity 文件使用相同的名称。这允许在两个纹理之间快速迭代。

更多关于导入纹理的信息可以在这里找到：[https://docs.unity3d.com/Manual/ImportingTextures.html](https://docs.unity3d.com/Manual/ImportingTextures.html)

需要使用 Alpha 通道的纹理应遵循此指南：[https://docs.unity3d.com/Manual/HOWTO-alphamaps.html](https://docs.unity3d.com/Manual/HOWTO-alphamaps.html)

##### 纹理文件格式

所有纹理都应为 .PSD 格式。导入文件中不应包含图层，并且只能有一个 Alpha 通道。

**[⬆ 返回顶部](#table-of-contents)**

<a name="audio"></a>
### 5.4 音频

仅导入未压缩的音频文件到 Unity，使用 WAV 或 AIFF 格式。

关于 [Unity 音频导入优化](https://www.gamedeveloper.com/audio/unity-audio-import-optimisation---getting-more-bam-for-your-ram) 的优秀指南

**[⬆ 返回顶部](#table-of-contents)**



#### 文章参考：
https://unity3d.com/learn/tutorials/topics/tips/large-project-organisation
https://github.com/Allar/ue4-style-guide
http://www.arreverie.com/blogs/unity3d-best-practices-folder-structure-source-control/
