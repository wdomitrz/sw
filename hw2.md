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
    - \newcommand{\Let}{\textsf{let }}
    - \newcommand{\In}{\textsf{in }}
    - \newcommand{\Alloc}{\textsf{alloc }}
    - \newcommand{\Fix}{\textsf{fix }}
    - \renewcommand{\t}{\qquad}
output:
    pdf_document
---


# Dziedziny pomocnicze

- $Proc = (State \to \Z) \times (\Z \to State \to State)$

# Rozwiązanie

## Deklaracja

### $\proc p(x \default e)\ I$
$$
\begin{split}
& \D \llbracket \proc p(x \default e)\ I \rrbracket\ \rho\ s = \left(\rho\left[p \mapsto \left(\E \llbracket e \rrbracket\ \rho, \Fix \Phi\right)\right], s\right) \\
& \t \Where \Phi\ f\ n\ s = \\
& \t\t \Let (l_x, s') = \Alloc s \\
& \t\t \In \S \llbracket I \rrbracket\ \rho[p \mapsto \left(\E \llbracket e \rrbracket\ \rho, f\right)][x \mapsto l_x]\ s'[l_x \mapsto n]
\end{split}
$$

## Wywołania

### $\Call p$
$$
\begin{split}
& \S \llbracket \Call p \rrbracket\ \rho\ s = f\ (\e\ s)\ s \\
& \t \Where (\e, f) = \rho\ p
\end{split}
$$

### $\Call p(e)$
$$
\begin{split}
& \S \llbracket \Call p(e) \rrbracket\ \rho\ s = f\ (\E \llbracket e \rrbracket\ \rho\ s)\ s \\
& \t \Where (\_, f) = \rho\ p
\end{split}
$$
