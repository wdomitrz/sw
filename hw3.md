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
    - \usepackage{a4wide}
    - \usepackage{amsmath}
    - \usepackage{amssymb}
    - \usepackage{latexsym}
    - \usepackage[english]{babel}
    - \usepackage[T1]{fontenc}
    - \usepackage[utf8]{inputenc}
    - \usepackage[pdftex]{color}
    - \usepackage[final]{listings}

output:
    pdf_document
---

\lstdefinelanguage{whileprograms}{morekeywords={while,do,if,then,else,),(,decr,in,wrt},%
   sensitive,%
   morecomment=[l]//,%
   morecomment=[s]{\{}{\}},%
   morecomment=[s]{[}{]},%
    basicstyle=\small\tt,
    keywordstyle=\normalfont\bfseries\color{black},
    commentstyle=\color{blue},
    mathescape=true,
}

\lstset{language=whileprograms,flexiblecolumns=true,mathescape=true,frame=none}
\lstset{commentstyle=\it,basicstyle=\tt}
\lstset{literate={<=}{{$\leq$}}2
                {>=}{{$\geq$}}2
                 {^}{{$\land$}}2
                 {&}{{$\land$}}2}


\begin{lstlisting}
{x>0, y>0}
xx:=x; yy:=y;
wx:=x; wy:=y;
{                                                                                      }
while {                                                                                }
   wx<>wy do
      {                                                                                }
      if wx<wy then
            while {                                                                    }
               wx+2*xx<=wy do
                  {                                                                    }
                  xx:=2*xx;
            {                                                                          }
            wx:=wx+xx;
            xx:=x
      else
            while {                                                                    }
               wy+2*yy<=wx do
                  {                                                                    }
                  yy:=2*yy;
            {                                                                          }
            wy:=wy+yy;
            yy:=y
{                                                                                      }
{wx=NWW(x,y)}
\end{lstlisting}
