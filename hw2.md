---
title: SEMANTYKA I WERYFIKACJA - Zadanie domowe nr 2
author: Witalis Domitrz
header-includes:
    - \usepackage{mathtools}
    - \usepackage{latexsym}
    - \usepackage{stmaryrd}
    - \usepackage{amssymb}
    - \newcommand{\Call}{\texttt{call }}
    - \newcommand{\proc}{\texttt{proc }}
    - \newcommand{\default}{\texttt{ default }}
    - \newcommand{\Z}{\mathbb{Z}}
    - \newcommand{\N}{\mathcal{N}}
    - \newcommand{\B}{\mathcal{B}}
    - \newcommand{\D}{\mathcal{D}}
    - \newcommand{\E}{\mathcal{E}}
    - \newcommand{\e}{\epsilon}
    - \renewcommand{\S}{\mathcal{S}}
    - \newcommand{\Where}{\textsf{where }}
    - \newcommand{\Alloc}{\textsf{alloc }}
    - \newcommand{\Fix}{\textsf{fix }}
    - \renewcommand{\t}{\qquad}
    - \newcommand{\rov}{\rho_{V}}
    - \newcommand{\rop}{\rho_{P}}
output:
    pdf_document
---


# Dziedziny syntaktyczne

Jak w treści.

# Dziedziny pomocnicze i semantyczne

Jedynie $\mathbf{Proc}$ jest niestandardowe.

- $\mathbf{Proc} = (\mathbf{Store} \to \Z) \times (\Z \to \mathbf{Store} \to \mathbf{Store})$

Reszta standardowo.

- $\Z$
- $\mathbf{Bool} = \{tt, ff\}$
- $\mathbf{VEnv} = Var \to \mathbf{Loc}$
- $\mathbf{PEnv} = PName \to \mathbf{Proc}$
- $\mathbf{Store} = \mathbf{Loc} \to \Z$
- $\mathbf{EXP} = \mathbf{VEnv} \to \mathbf{Store} \to \Z$
- $\mathbf{BEXP} = \mathbf{VEnv} \to \mathbf{Store} \to \mathbf{Bool}$
- $\mathbf{DECL} = \mathbf{VEnv} \to \mathbf{PEnv} \to \mathbf{Store} \to (\mathbf{VEnv} \times \mathbf{PEnv} \times \mathbf{Store})$
- $\mathbf{INSTR} = \mathbf{VEnv} \to \mathbf{PEnv} \to \mathbf{Store} \to \mathbf{Store}$

# Funkcje semantyczne

Standardowo.

- $\N : Num \to \Z$
- $\E : Expr \to \mathbf{EXP}$
- $\B : BExpr \to \mathbf{BEXP}$
- $\D : Decl \to \mathbf{DECL}$
- $\S : Instr \to \mathbf{INSTR}$

# Rozwiązanie

## Deklaracja

### $\proc p(x \default e)\ I$
$$
\begin{split}
& \D \llbracket \proc p(x \default e)\ I \rrbracket\ \rov\ \rop\ s =
    \left(
        \rov,
        \rop \left[p \mapsto \left(
            \E \llbracket e \rrbracket\ \rov,
            \Fix \Phi\right)\right],
        s\right) \\
& \t \Where \\
& \t \t \Phi =
    \lambda f. \lambda n.\lambda s'.\S \llbracket I \rrbracket\ \rov[x \mapsto l_x]\ \rop[p \mapsto \left(\E \llbracket e \rrbracket\ \rov, f\right)]\ s''[l_x \mapsto n] \\
& \t\t\t \Where (l_x, s'') = \Alloc s'
\end{split}
$$

## Wywołania

### $\Call p$
$$
\begin{split}
& \S \llbracket \Call p \rrbracket\ \rov\ \rop\ s = f\ (\e\ s)\ s \\
& \t \Where (\e, f) = \rop\ p
\end{split}
$$

### $\Call p(e)$
$$
\begin{split}
& \S \llbracket \Call p(e) \rrbracket\ \rov\ \rop\ s = f\ (\E \llbracket e \rrbracket\ \rov\ s)\ s \\
& \t \Where (\_, f) = \rop\ p
\end{split}
$$

## Reszta

Reszta nie różni się od standardowej semantyki języka z procedurami z parametrami przekazywanymi przez wartość.
