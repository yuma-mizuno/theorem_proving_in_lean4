<!-- Introduction -->
導入
============

<!-- Computers and Theorem Proving -->
計算機と定理証明
-----------------------------

*Formal verification* involves the use of logical and computational methods to establish claims that are expressed in precise mathematical terms.
These can include ordinary mathematical theorems, as well as claims that pieces of hardware or software, network protocols, and mechanical and hybrid systems meet their specifications.
In practice, there is not a sharp distinction between verifying a piece of mathematics and verifying the correctness of a system:
formal verification requires describing hardware and software systems in mathematical terms, at which point establishing claims as to their correctness becomes a form of theorem proving. Conversely, the proof of a mathematical theorem may require a lengthy computation, in which case verifying the truth of the theorem requires verifying that the computation does what it is supposed to do.

*形式的検証（formal verification）*とは、論理的・計算論的方法を用いて、厳密な数学用語で表現された主張を証明することです。これには、通常の数学定理のほか、ハードウェアやソフトウェアの一部、ネットワーク・プロトコル、機械システムやハイブリッドシステムがその仕様を満たしているという主張も含まれます。実際には、数学の一部を検証することと、システムの正しさを検証することの間には、明確な区別はありません。形式的検証では、ハードウェアやソフトウェアのシステムを数学的な言葉で記述する必要があり、その時点で、その正しさを証明することは定理証明の一種となります。逆に、数学定理の証明には長い計算を要することがあり、その場合、定理の真偽を検証するためには、計算が想定通りに実行されていることを検証する必要があります。

The gold standard for supporting a mathematical claim is to provide a proof,
and twentieth-century developments in logic show most if not all conventional proof methods can be reduced to a small set of axioms and rules in any of a number of foundational systems. With this reduction, there are two ways that a computer can help establish a claim: it can help find a proof in the first place, and it can help verify that a purported proof is correct.

数学的主張を裏付ける究極的な水準は、証明を示すことです。
20世紀における論理学の発展により、ほとんどの従来の証明方法は、全てではないにせよ、いくつかの基礎的な体系における少数の公理と規則の集合に還元できることが分かりました。この還元を踏まえて、計算機が証明を手助けする方法は2つあります。つまり、まず証明を発見することと、証明だとされるものの正しさを検証することです。

*Automated theorem proving* focuses on the "finding" aspect. 
Resolution theorem provers, tableau theorem provers, fast satisfiability solvers, and so on 
provide means of establishing the validity of formulas in propositional and first-order logic.
Other systems provide search procedures and decision procedures for specific languages and domains, such as linear or nonlinear expressions over the integers or the real numbers.
Architectures like SMT ("satisfiability modulo theories") combine domain-general search methods with domain-specific procedures.
Computer algebra systems and specialized mathematical software packages provide means of carrying out mathematical computations, establishing mathematical bounds, or finding mathematical objects.
A calculation can be viewed as a proof as well, and these systems, too, help establish mathematical claims.

*自動定理証明（automated theorem proving）*は、「発見」の側面に焦点を当てています。
導出原理（resolution theorem provers）や、タブロー法（tableau theorem provers）、SATソルバー（fast satisfiability solvers）などは、命題論理や一階述語論理における式の妥当性を検証（validate）する手段です。
また、整数や実数に対する線形式や非線形式など、特定の言語やドメインに対する探索手続きや決定手続きを提供するシステムもあります。
SMT（satisfiability modulo theories, 充足可能性モジュロ理論）のようなアーキテクチャーは、ドメイン固有の手続きに汎用的な検索手法と組み合わせたものです。数式処理システム（computer algebra systems, CAS）や特化型の数学ソフトウェア・パッケージは、数学的な計算（computation）を実行したり、不等式を示したり、数学的対象を発見したりする手段です。計算（calculation）は証明と見なすこともできるため、これらのシステムもまた数学的主張の証明の手助けとなります。

Automated reasoning systems strive for power and efficiency, often at the expense of guaranteed soundness.
Such systems can have bugs, and it can be difficult to ensure that the results they deliver are correct.
In contrast, *interactive theorem proving* focuses on the "verification" aspect of theorem proving, requiring that every claim is supported by a proof in a suitable axiomatic foundation.
This sets a very high standard: every rule of inference and every step of a calculation has to be justified by appealing to prior definitions and theorems, all the way down to basic axioms and rules. In fact, most such systems provide fully elaborated "proof objects" that can be communicated to other systems and checked independently. Constructing such proofs typically requires much more input and interaction from users, but it allows you to obtain deeper and more complex proofs.

自動推論システム（ausomated reasoning systems）は、しばしば健全性の保証を犠牲にして、パワーと効率性を追求しています。このようなシステムにはバグがあることもあり、その結果が正しいことを確めるのは難しいです。
対照的に、*対話型定理証明（interactive theorem proving）*は、定理証明の「検証」の側面に焦点を当て、すべての主張が適切な公理系における証明によって裏付けられていることを要求します。これは非常に高い水準を設定するもので、すべての推論規則とすべての計算ステップは、基本的な公理や推論規則に至るまで、事前に示された定義や定理に照らして正当化されなければならなりません。実際、このようなシステムのほとんどは、他のシステムに伝達して独立にチェックできるように完全に精密化された「証明オブジェクト」を提供しています。このような証明を構築すると、一般にはユーザーからの入力や対話をより多く必要となりますが、より深く複雑な証明が得られるようになります。

The *Lean Theorem Prover* aims to bridge the gap between interactive and automated theorem proving, by situating automated tools and methods in a framework that supports user interaction and the construction of fully specified axiomatic proofs. The goal is to support both mathematical reasoning and reasoning about complex systems, and to verify claims in both domains.

*Lean Theorem Prover* は、ユーザー対話と完全に仕様化された公理的証明の構築の両方をサポートするフレームワークに自動化ツールと方法を据える[^1]ことで、対話型定理証明と自動定理証明のギャップを埋めることを目指しています。
そのゴールは、数学的推論と複雑なシステムに纏わる推論の両方をサポートし、それぞれのドメインにおける主張を検証することです。

[^1]: 原文の係り受け不明瞭

Lean's underlying logic has a computational interpretation, and Lean can be viewed equally well as a programming language.
More to the point, it can be viewed as a system for writing programs with a precise semantics,
as well as reasoning about the functions that the programs compute.
Lean also has mechanisms to serve as its own *metaprogramming language*,
which means that you can implement automation and extend the functionality of Lean using Lean itself. These aspects of Lean are explored in a companion tutorial to this one, [Programming in Lean 4](TBD), though computational aspects of the system will make an appearance here.

Lean を基礎付けている論理は計算論的な解釈を持ち、Lean はプログラミング言語と同一視できます。さらに言えば、Lean は精密な意味論（precise semantics）を持つプログラムを記述するためのシステムであり、プログラムが計算する関数について推論するためのシステムでもあります。Lean はまた、独自の*メタプログラミング言語*として機能する仕組みを持っています。つまり、Lean そのものを使って、Lean の自動化を実装したり、機能を拡張したりできるのです。Leanのこのような側面は、関連チュートリアルである [Programming in Lean 4](TBD) で探求されますが、システムの計算的側面はここでも登場します。

<!-- About Lean -->
Lean について
----------

The *Lean* project was launched by Leonardo de Moura at Microsoft Research Redmond in 2013. It is an ongoing, long-term effort, and much of the potential for automation will be realized only gradually over time. Lean is released under the [Apache 2.0 license](LICENSE), a permissive open source license that permits others to use and extend the code and mathematical libraries freely.

*Lean* プロジェクトは、Microsoft Research Redmond の Leonardo de Moura によって2013年に立ち上げられました。このプロジェクトは現在進行中の長期的な取り組みであり、可能な自動化の多くは時間の経過とともに徐々にしか実現されないでしょう。Lean は [Apache 2.0 ライセンス](LICENSE)に基づいてリリースされています。これは自由にコードと数学ライブラリを使用したり拡張したりすることを許可する寛容なオープンソースライセンスです。

To install Lean in your computer consider using the [Quickstart](https://github.com/leanprover/lean4/blob/master/doc/quickstart.md) instructions. The Lean source code, and instructions for building Lean, are available at [https://github.com/leanprover/lean4/](https://github.com/leanprover/lean4/). 

Lean をインストールするには、[Quickstart](https://github.com/leanprover/lean4/blob/master/doc/quickstart.md) を参照してください。Lean のソースコードとビルド方法は [https://github.com/leanprover/lean4/](https://github.com/leanprover/lean4/) にあります。

This tutorial describes the current version of Lean, known as Lean 4.

このチュートリアルでは、Lean 4 と呼ばれる最新バージョンの Lean について説明します。

<!-- About this Book -->
本書について
---------------

This book is designed to teach you to develop and verify proofs in Lean.
Much of the background information you will need in order to do this is not specific to Lean at all.
To start with, you will learn the logical system that Lean is based on, a version of *dependent type theory* that is powerful enough to prove almost any conventional mathematical theorem, and expressive enough to do it in a natural way.
More specifically, Lean is based on a version of a system known as the Calculus of Constructions with inductive types.
Lean can not only define mathematical objects and express mathematical assertions in dependent type theory, but it also can be used as a language for writing proofs.

本書は、Lean で証明を記述し検証する方法を学ぶためのものです。そのために必要な背景情報の多くは Lean 特有のものではありません。まず最初に、Lean が根拠としている論理システムを学びます。これは*依存型理論（dependent type theory）*の一種で、従来の数学定理のほとんどを証明するのに十分強力であり、それを自然な方法で行うのに十分な表現力を持っています。より具体的には、Lean は帰納的型（inductive types）を用いた Calculus of Constructions [^2] として知られる論理システムの一種に基づいています。Lean は数学的対象を定義したり依存型理論で数学的主張を表現したりできるだけでなく、証明を書くための言語としても利用できます。

[^2]: Calculus of Inductive Constructions (CIC)

Because fully detailed axiomatic proofs are so complicated, the challenge of theorem proving is to have the computer fill in as many of the details as possible.
You will learn various methods to support this in [dependent type theory](dependent_type_theory.md). 
For example, term rewriting, and Lean's automated methods for simplifying terms and expressions automatically.
Similarly, methods of *elaboration* and *type inference*, which can be used to support flexible forms of algebraic reasoning.

完全に詳細な公理論的証明は非常に複雑であるため、定理証明の課題は、できるだけ多くの詳細をコンピュータに埋めさせることです。[依存型理論](dependent_type_theory.md)では、これをサポートする様々な方法を学びます。例えば、項の書き換えや、項や式を自動的に簡略化するためのLeanの自動化手法などである。同様に、*精緻化（elaboration）*[^3]や*型推論（type inference）*といったメソッドも、柔軟な代数的推論に使えます。

[^3]: 定訳なし？エラボレーション

Finally, you will learn about features that are specific to Lean, including the language you use to communicate with the system, and the mechanisms Lean offers for managing complex theories and data.

最後に、システムと対話するために使う言語や、複雑な理論やデータを管理するための Lean の仕組みなど、Lean 特有の機能について学びます。

Throughout the text you will find examples of Lean code like the one below:

本文中には、以下のような Lean コードの例があります：

```lean
theorem and_commutative (p q : Prop) : p ∧ q → q ∧ p :=
  fun hpq : p ∧ q =>
  have hp : p := And.left hpq
  have hq : q := And.right hpq
  show q ∧ p from And.intro hq hp
```

If you are reading the book inside of [VS Code](https://code.visualstudio.com/), you will see a button that reads "try it!"
Pressing the button copies the example to your editor with enough surrounding context to make the code compile correctly.
You can type things into the editor and modify the examples, and Lean will check the results and provide feedback continuously as you type.
We recommend running the examples and experimenting with the code on your own as you work through the chapters that follow. You can open this book on VS Code by using the command "Lean 4: Open Documentation View".

この本を [VS Code](https://code.visualstudio.com/) で読んでいるなら、"try it!" というボタンが表示されます。このボタンを押すと、コードを正しくコンパイルするのに十分な周辺コンテキストとともに、エディタに例がコピーされます。エディタに入力し、例を修正することもできます。Leanはあなたが入力した結果をチェックし、継続的にフィードバックを提供します。この後の章を読み進めながら、自分でサンプルを実行し、コードを試してみることをお勧めします。本書は、「Lean 4: Open Documentation View」コマンドを使って VS Code 上で開くことができます。

<!-- Acknowledgments -->
謝辞
---------------

This tutorial is an open access project maintained on Github.
Many people have contributed to the effort, providing corrections, suggestions, examples, and text. 
We are grateful to Ulrik Buchholz, Kevin Buzzard, Mario Carneiro, Nathan Carter, Eduardo Cavazos, Amine Chaieb, Joe Corneli, William DeMeo, Marcus Klaas de Vries, Ben Dyer, Gabriel Ebner, Anthony Hart, Simon Hudon, Sean Leather, Assia Mahboubi, Gihan Marasingha, Patrick Massot, Christopher John Mazey, Sebastian Ullrich, Floris van Doorn, Daniel Velleman, Théo Zimmerman, Paul Chisholm, Chris Lovett, and Siddhartha Gadgil for their contributions.
Please see [lean prover](https://github.com/leanprover/) and [lean community](https://github.com/leanprover-community/) for an up to date list of our amazing contributors.

このチュートリアルは Github 上で管理されているオープンアクセスプロジェクトです。多くの人々が修正案・提案・例示・文章を提供してこの取り組みに貢献して下さいました。
Ulrik Buchholz, Kevin Buzzard, Mario Carneiro, Nathan Carter, Eduardo Cavazos, Amine Chaieb, Joe Corneli, William DeMeo, Marcus Klaas de Vries, Ben Dyer, Gabriel Ebner, Anthony Hart, Simon Hudon, Sean Leather, Assia Mahboubi, Gihan Marasingha, Patrick Massot, Christopher John Mazey, Sebastian Ullrich, Floris van Doorn, Daniel Velleman, Théo Zimmerman, Paul Chisholm, Chris Lovett, and Siddhartha Gadgil の貢献に感謝いたします。
素晴らしい貢献者達の最新リストについては [Lean prover](https://github.com/leanprover/) と [Lean community](https://github.com/leanprover-community/) をご覧ください。

