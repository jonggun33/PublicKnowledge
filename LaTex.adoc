= LaTex
:toc: left
:sectnums:

== Environment Setting
=== Mac
. Installl Skim
. For Skim Preference>Sync... 'Check for file Changes', 'Reload automatically'
. Install MacTex (xelatex, latex)
. Edit ~/.vimrc

[source, bash]
autocmd FileType tex nmap <buffer><C-T>: !xelatex %<CR>
autocmd FileType tex nmap <buffer> T : !open -a Skim %:r.pdf<CR><CR>

https://tex.stackexchange.com/questions/353593/setting-up-a-latex-environment-for-vim[vim+latex on mac]

=== Windows

== Document Structure
[source, latex]
\documentclass{article}
\title{Cartesian closed categories and the price of eggs}
\author{Jane Doe}
\date{September 1994}
\begin{document}
   \maketitle
   Hello world!
\end{document}

=== Skeleton for a Cheatsheet
[source, latex]
\documentclass [a3paper]{article}
\usepackage{milticol}
\usepackage{blindtext}
\usepackage[margin=0.5in, landscape]{geometry}
\title{SKELETON for a Cheetsheet}
%\setcounter{secnumdepth}{0}
%\setcounter{partnumdepth}{0}
\begin{document}
%\maketitle
%\raggedright
\begin{multicols}{4}
\part{Data Scientist Cheetsheet}
\section{numpy}
np.arount(p, decimals=4)\\
np.sqrt(df)\\
\section{Dataframe Creation}
\begin{verbatim}
pd.read_csv('abc.csv', sep='\t', encoding='CP949');
df = sr.to_frame()
\end{verbatim}
\begin{center}
    \Large{Happy Happy}
\end{center}
\begin{tabular}{ll}
abc & def \\
\end{tabular}
\begin{tabular{{@@{}||@{}}
\verb!name! & ming zi \\
\verb!age! & na i \\
\end{tabular}
\blindtext
\blindtext
\blindtext
\blidtext
\section{bbb}
\blindtext
\blindtext
\end{multicols}
\end{document}

== Mathematics

== Drawing