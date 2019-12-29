---
title: SEMANTYKA I WERYFIKACJA - Zadanie domowe nr 2
author: Witalis Domitrz
header-includes:
    - \usepackage{mathtools}
    - \usepackage{latexsym}
    - \usepackage{stmaryrd}
    - \newcommand{\Call}{\texttt{call }}
    - \newcommand{\proc}{\texttt{proc }}
    - \newcommand{\default}{\texttt{ default }}
    - \newcommand{\Z}{\mathbb{Z}}
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


# Dziedziny pomocnicze

- $Proc = (VEnv \to State \to \Z) \times (\Z \to State \to State)$
- $PEnv = PName \to Proc$

# Dziedziny semantyczne

- $\D : Decl \to VEnv \to PEnv \to State \to (VEnv \times PEnv \times State)$
- $\S : Instr \to VEnv \to PEnv \to State \to State$

# Rozwiązanie

## Deklaracja

### $\proc p(x \default e)\ I$
$$
\begin{split}
& \D \llbracket \proc p(x \default e)\ I \rrbracket\ \rov\ \rop\ s =
    \left(
        \rov,
        \rop \left[p \mapsto \left(
            \E \llbracket e \rrbracket,
            \Fix \Phi\right)\right],
        s\right) \\
& \t \Where \Phi\ P\ n\ s =
    \S \llbracket I \rrbracket\ \rov[x \mapsto l_x]\ \rop[p \mapsto \left(\E \llbracket e \rrbracket, P\right)]\ s'[l_x \mapsto n] \\
& \t\t \Where (l_x, s') = \Alloc s
\end{split}
$$

## Wywołania

### $\Call p$
$$
\begin{split}
& \S \llbracket \Call p \rrbracket\ \rov\ \rop\ s = P\ (\e\ \rov\ s)\ s \\
& \t \Where (\e, P) = \rop\ p
\end{split}
$$

### $\Call p(e)$
$$
\begin{split}
& \S \llbracket \Call p(e) \rrbracket\ \rov\ \rop\ s = P\ (\E \llbracket e \rrbracket\ \rov\ s)\ s \\
& \t \Where (\_, P) = \rop\ p
\end{split}
$$
