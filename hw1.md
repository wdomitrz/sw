---
title: SEMANTYKA I WERYFIKACJA - Zadanie domowe nr 1
author: Witalis Domitrz
header-includes:
    - \usepackage{bussproofs}
    - \usepackage{mathtools}
    - \usepackage{latexsym}
    - \newcommand{\If}{\texttt{if }}
    - \newcommand{\Then}{\texttt{ then }}
    - \newcommand{\Else}{\texttt{ else }}
    - \newcommand{\While}{\texttt{while }}
    - \newcommand{\Do}{\texttt{ do }}
    - \newcommand{\Protect}{\texttt{protect }}
    - \newcommand{\In}{\texttt{ in }}
output:
    pdf_document
---

<!---
\begin{prooftree}
\end{prooftree}
\AxiomC{}
\UnaryInfC{}
\BinaryInfC{}
\TrinaryInfC{}
\QuaternaryInfC{}
\QuinaryInfC{}
-->

# Oznaczenia

- $x \in Var$

    W przypadku przerwania potrzeba informacji o tym na jakiej zmiennej miało się wykonać przypisanie, dlatego będę utożsamiał taką przerywającą konfigurację z nazwą zmiennej na której rozpoczęło się przerwanie.

- $y \in Var \land y \neq x$

    Jest to nazwa zmiennej różna od $x$.

- $p \in P\left(Var\right)$

    Jest to zbiór zmiennych chronionych.

- $z \in State \cup Var$

    Używam $z$ tam, gdzie nie ma znaczenia jakiego typu jest to, co wyszło.

# Rozszerzenie konfiguracji
$\Gamma_{Expr} \Coloneqq Instr \times State \times P(Var) \cup State \cup Var$

# Uruchamianie programu
Programy zaczynają wykonanie w elemencie zbioru $Instr \times State \times P(Var)$ mającym pusty zbiór na trzeciej współrzędnej.

# Rozwiązanie

## $skip$
\begin{prooftree}
\AxiomC{$\left<skip, s, p\right> \leadsto s$}
\end{prooftree}

## $\coloneqq$

Przerwanie instrukcji ma nastąpić, gdy "w którejkolwiek chwili podczas wykonywania tej instrukcji nastąpi przypisanie, które zmienia wartość zmiennej $x$ (...)"

\begin{prooftree}
\AxiomC{$x \in p$}
\AxiomC{$\left<e, s\right> \leadsto n$}
\AxiomC{$s\ x \neq n$}
\TrinaryInfC{$\left<x \coloneqq e, s, p\right> \leadsto x$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$x \in p$}
\AxiomC{$\left<e, s\right> \leadsto n$}
\AxiomC{$s\ x = n$}
\TrinaryInfC{$\left<x \coloneqq e, s, p\right> \leadsto s$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$x \notin p$}
\AxiomC{$\left<e, s\right> \leadsto n$}
\BinaryInfC{$\left<x \coloneqq e, s, p\right> \leadsto s[x \mapsto n]$}
\end{prooftree}

## $;$
\begin{prooftree}
\AxiomC{$\left<I_1, s, p\right> \leadsto x$}
\UnaryInfC{$\left<I_1 ; I_2, s, p\right> \leadsto x$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$\left<I_1, s, p\right> \leadsto s'$}
\AxiomC{$\left<I_2, s', p\right> \leadsto z$}
\BinaryInfC{$\left<I_1 ; I_2, s, p\right> \leadsto z$}
\end{prooftree}

## $if$
\begin{prooftree}
\AxiomC{$\left<b, s\right> \leadsto tt$}
\AxiomC{$\left<I_1, s, p\right> \leadsto z$}
\BinaryInfC{$\left<\If b \Then I_1 \Else I_2, s, p\right> \leadsto z$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$\left<b, s\right> \leadsto ff$}
\AxiomC{$\left<I_2, s, p\right> \leadsto z$}
\BinaryInfC{$\left<\If b \Then I_1 \Else I_2, s, p\right> \leadsto z$}
\end{prooftree}

## $while$
\begin{prooftree}
\AxiomC{$\left<b, s\right> \leadsto ff$}
\UnaryInfC{$\left<\While b \Do I, s, p\right> \leadsto s$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$\left<b, s\right> \leadsto tt$}
\AxiomC{$\left<I, s, p\right> \leadsto x$}
\BinaryInfC{$\left<\While b \Do I, s, p\right> \leadsto x$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$\left<b, s\right> \leadsto tt$}
\AxiomC{$\left<I, s, p\right> \leadsto s'$}
\AxiomC{$\left<\While b \Do I, s', p\right> \leadsto z$}
\TrinaryInfC{$\left<\While b \Do I, s, p\right> \leadsto z$}
\end{prooftree}

## $protect$
\begin{prooftree}
\AxiomC{$\left<I, s, p \cup \{x\}\right> \leadsto s'$}
\UnaryInfC{$\left<\Protect x \In I, s, p\right> \leadsto s'$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$\left<I, s, p \cup \{x\}\right> \leadsto y$}
\UnaryInfC{$\left<\Protect x \In I, s, p\right> \leadsto y$}
\end{prooftree}

Przerwanie ma być propagowane do wszystkich \texttt{protect}ów tak, jak w odpowiedzi na trzecie pytanie z "[odpowiedzi na niektóre pytania dotyczące zadania domowego z semantyki operacyjnej](https://www.mimuw.edu.pl/~klin/teaching/sem19-20/praca-domowa-1.html)" opublikowanych na stronie wykładowcy.
\begin{prooftree}
\AxiomC{$\left<I, s, p \cup \{x\}\right> \leadsto x$}
\AxiomC{$x \in p$}
\BinaryInfC{$\left<\Protect x \In I, s, p\right> \leadsto x$}
\end{prooftree}

\begin{prooftree}
\AxiomC{$\left<I, s, p \cup \{x\}\right> \leadsto x$}
\AxiomC{$x \notin p$}
\BinaryInfC{$\left<\Protect x \In I, s, p\right> \leadsto s$}
\end{prooftree}
