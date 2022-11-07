一种针对 MUS 求解问题的加强剪枝策略
========================
本文提出了一种新策略ABC，应用于MARCO算法与MARCO-MAM算法中。
文件夹《MARCO-ABC》对应MARCO算法中加入ABC策略的代码。
文件夹《MARCO-MAM-ABC》对应MARCO-MAM算法中加入ABC策略的代码。

1.实验中的数据集在子目录test2中（两个子目录中均有）
2.此代码的MARCO算法是其改进版本
3.代码与论文的对应情况
###MARCO原版论文：
Liffiton MH, Malik A. Enumerating infeasibility: Finding multiple MUSes quickly. In Proceedings of the 10th International Conference on Integration of AI and OR Techniques in Constraint Programming (CPAIOR 2013),2013,160–175.
###MARCO改进版论文：
Liffiton M H，Previti A，Malik A. Fast，flexible MUS enumeration. Constraints,2016,21(2):223–250.
###MARCO-MAM论文：
欧阳丹彤,高菡,田乃予,等.基于双模型的MUS求解方法.计算机研究与发展,2019,56(12):2623−2631. https://crad.ict.ac.cn/CN/10.7544/issn1000-1239.2019.20180852 [doi: 10.7544/issn1000-1239.2019.20180852]
4.实验环境配置与代码运行方式（与MARCO算法一致）
MARCO算法的readme文档在上述两个子文件夹中，内容同下：

MARCO: an efficient MUS and MSS/MCS enumeration tool
====================================================

This is a Python implementation of the MARCO/MARCOs algorithm [1,2] for
enumerating MUSes and MSS/MCSes of infeasible constraint systems (currently:
CNF, GCNF, and SMT).  This implementation makes use of MUSer2 [3,4] for MUS
extraction and MiniSAT 2.2 [5] for satisfiability testing and the generation of
SAT models.

   Website: http://www.iwu.edu/~mliffito/marco/

Please contact Mark Liffiton (mliffito@iwu.edu) in case of any errors or
questions.

[1] MARCO
   M. Liffiton, A. Previti, A. Malik, and J. Marques-Silva (2016)
   "Fast, Flexible MUS Enumeration." In: Constraints 21(2):223-250.

[2] MARCOs (parallel MARCO)
   W. Zhao and M. Liffiton (2016) "Parallelizing Partial MUS Enumeration."
   In: Proc. ICTAI 2016.

[3] MUSer2
   A. Belov and J. Marques-Silva (2012) "MUSer2: An efficient MUS extractor."
   In: Journal on Satisfiability, Boolean Modeling and Computation 8, 123-128.

[4] MUSer2 (parallel)
   A. Belov, N. Manthey, and J. Marques-Silva (2013) "Parallel MUS extraction."
   In: Proc. SAT 2013.

[5] Minisat 2.2
   N. Een and N. Sörensson (2003) "An Extensible SAT-solver." In: Proc. SAT 2003.
   N. Een and A. Biere (2005) "Effective Preprocessing in SAT through Variable
   and Clause Elimination." In: Proc. SAT 2005. 


## Setup

This implementation makes use of Python bindings for MiniSAT that must be built
before running MARCO.

Tested Platforms:

 - Linux
 - Cygwin
 - OS X

Requirements:

 - Python 2.7 or 3.x
 - A standard build environment (make, gcc or clang, etc.)
 - zlib development libraries (e.g., `zlib1g-dev` or `zlib-devel` packages)

To build and test the Python bindings:

    $ cd pyminisolvers
    $ make
    $ python test_minisolvers.py

Additionally, the following are recommended, depending on your needs:

 - Z3 Python interface for analyzing SMT instances.

     Available as part of the Z3 distribution: https://github.com/Z3Prover/z3

 - A MUSer2 binary for analyzing CNF/GCNF.  The included `muser2-para` binary
   is compiled for x86-64 Linux.  For other platforms, download and compile
   from the source (license: GPL).

     Available from: https://bitbucket.org/anton_belov/muser2-para

   Without a working MUSer2 binary, you can still run MARCO on CNF/GCNF in a
   fall-back mode that uses a basic, *much less efficient* deletion-based MUS
   extractor using Minisat directly (see the `--force-minisat` option).


## Usage

Example: `./marco.py tests/test1.cnf`

Run `./marco.py --help` for a list of available options.

Input files may be in CNF, GCNF (group oriented CNF), or SMT2 format.  Input
files may be gzipped.

The supported GCNF format is specified in:
  http://www.satcompetition.org/2011/rules.pdf

The output lists MUSes ("U") and MSSes ("S"), one per line.  In 'verbose' mode
(-v), each line also lists the indexes of the constraints included in each set
(with 1-based counting).  MCSes are the complements of the MSSes w.r.t. the
original set of input constraints (e.g., if MARCO reports an MSS "1 3 4" for a
5-constraint input, the corresponding MCS is constraints 2 and 5).  If you want
the MCSes printed directly, use the '--print-mcses' command line option; MCSes
will be printed on lines starting with "C" (in place of the "S" lines for their
MSSes).


## Authors
- MARCO: Mark Liffiton and Wenting Zhao

### Included solvers
- MUSer2: Anton Belov, Norbert Manthey, and Joao Marques-Silva
- MiniSAT: Niklas Een and Niklas Sörensson
- MiniCARD: Mark Liffiton and Jordyn Maglalang
