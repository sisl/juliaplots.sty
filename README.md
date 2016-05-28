# juliaplots.sty

This package makes it easy to integrate Julia code and plots into latex documents. It sits on top of [pythontex](https://www.ctan.org/pkg/pythontex?lang=en), which comes bundled with TexLive and MikTeX. Python must be installed along with the other dependencies of pythontex (e.g., pygments).

To install this package, just download [juliaplots.sty](https://github.com/sisl/juliaplots.sty/raw/master/juliaplots.sty) file and place it in the directory of your document.

The package currently supports the following Julia plotting packages:

1. [PGFPlots.jl](https://github.com/sisl/PGFPlots.jl)
2. [PyPlot.jl](https://github.com/stevengj/PyPlot.jl)
3. [Gadfly.jl](https://github.com/dcjones/Gadfly.jl)

Before using any of these packages, they must be installed and usable from Julia. In the case of Gadfly, you must also have [Cairo.jl](https://github.com/JuliaGraphics/Cairo.jl)  installed.

Only one plotting package is permitted. You specify the package you want as a package option to `juliaplots`. For example:
* `\usepackage[pgfplots]{juliaplots}`
* `\usepackage[pyplot]{juliaplots}`
* `\usepackage[gadfly]{juliaplots}`

As with pythontex, you can run code using `jlcode`:
```latex
\begin{jlcode}
	x = [1,2,3]
	y = [2,4,1]
	plot(x, y)
\end{jlcode}
```

You can run and typeset code using `jlblock`
```latex
\begin{jlblock}
	x = [1,2,3]
	y = [2,4,1]
	plot(x, y)
\end{jlblock}
```

You can run a command with, for example, `\jlc{x=2}`. You can typeset code without running it with `\jlv{x=2}`. You can run a command and typeset it using `\jlb{x=2}`.

The functionality that is added by juliaplots.jl is the `\plot` command, which will generate the plot and inject it into the document. The number of arguments depends on which plotting package you are using. Here are examples:
* PGFPlots: `\plot{myfile}`, where the sole argument is the name of the file (do not include the file extension) that will be used in the background for including the plot.
* PyPlot: `\plot{myfile}{width=3in}`, where the first argument is the name of the PDF file (without file extension) to store the image, and the second argument are the options to be passed to `\includegraphics` when the PDF is included.
* Gadfly: `\plot{myfile}{3inch}{3inch}{width=3in}`, where the first argument is the name of the PDF file (without file extension) to store the image, the second is the width of the image to be exported by Gadfly, the third is the height of the image to be exported by Gadfly, and the fourth argument contains the options to be passed to `\includegraphics` when the PDF is included.

To create your document, run `lualatex mytexfile.tex` (or similar command), then `pythontex mytexfile.tex`, and then `lualatex mytexfile.tex`. If you have trouble with the generation of your plot, see the error output from pythontex.

This repository contains example tex files and their associated PDF files.

### Future work

In the future, we would like to support [Plots.jl](https://github.com/tbreloff/Plots.jl).
