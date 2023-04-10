# GPIO mapping of APP2.0 shuttle board pins


The APP2.0 shuttle board has total 28 pins, of which some have a predefined functionality and some can be used as GPIO by the user.

The shuttle board connector details are given in the table below.

\begin{table}[H]
	\centering
	\begin{tabular}{|c|c|c|c|}
		\hline
		\textbf{Pin number on} & \textbf{Name /} & \textbf{Pin number on} & \textbf{Name /} \\
		\textbf{shuttle board} & \textbf{function} & \textbf{shuttle board} & \textbf{function} \\
		\hline\hline
		1 & VDD (3.3V) & 28 & SHTLE\_COD \#4 \\ \hline
		2 & VDDIO (3.3V) & 27 & SHTLE\_COD \#3 \\ \hline
		3 & GND & 26 & SHTLE\_COD \#2 \\ \hline
		4 & SPI MISO & 25 & SHTLE\_COD \#1 \\ \hline
		5 & SPI: MOSI / I\textsuperscript{2}C: SDA & 24 & SHTLE\_COD \#0 \\ \hline
		6 & SPI: SCK / I\textsuperscript{2}C: SCL & 23 & SHTLE\_COD\_GND \\ \hline
		7 & SPI: CS & 22 & IO\_4 ( GPIO \#4 ) \\ \hline
		8 & IO\_5 ( GPIO \#5 ) & 21 & IO\_7 ( GPIO \#7 ) \\ \hline
		9 & IO\_0 ( GPIO \#0 ) & 20 & IO\_6 ( GPIO \#6 ) \\ \hline 
		10 & SHTLE\_COD \#5 & 19 & IO\_8 ( GPIO \#8 ) \\ \hline 
		11 & SHTLE\_COD \#6 & 18 & SCL (see note) \\ \hline 
		12 & SHTLE\_COD \#7 & 17 & SDA (see note)\\ \hline 
		13 & SHTLE\_COD \#8 & 16 & IO\_3 ( GPIO \#3 ) \\ \hline
		14 & IO\_1 ( GPIO \#1 ) & 15 & IO\_2 ( GPIO \#2 ) \\ \hline
	\end{tabular}
	\caption{Overview of shuttle board pins and their function}
	\label{tab:shtbrdpins}
\end{table}

Note:
\begin{itemize}
	\item In coinesAPI the pins are addressed using the same numbers as on the shuttle board. For example, the GPIO \#5 has the pin number 8.
	\item In some cases (depending on the sensor), the I\textsuperscript{2}C lines are shuttle board pin 6 for the clock signal SCL and shuttle board pin 5 for the data line SDA. In such cases pins 17 and 18 may not be connected. Please carefully read the shuttle board documentation.
\end{itemize}