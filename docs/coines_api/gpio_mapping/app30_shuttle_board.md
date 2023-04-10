# GPIO mapping of APP3.0 shuttle board pins

The APP3.0 shuttle board has a total of 16 pins, 7 on the left and 9 on the right. (with shuttle board pins facing downwards)

Note:
\begin{itemize}
	\item In coinesAPI the pins are addressed as on the APP3.0 shuttle board. For example, the GPIO \#5 is addressed as \texttt{COINES\_MINI\_SHUTTLE\_PIN\_2\_6}.
	\item Supported VDD voltages on APP3.0 board are 0, 1.8V and 2.8V.
	\item Supported VDDIO voltage on APP3.0 board is 1.8V.
\end{itemize}

\begin{table}[H]
	\centering
	\begin{tabular}{|c|c|c|c|}
		\hline
		\textbf{Pin number on} & \textbf{Name /} & \textbf{Pin number on} & \textbf{Name /} \\
		\textbf{shuttle board} & \textbf{function} & \textbf{shuttle board} & \textbf{function} \\
		\hline\hline
		1\_1 & VDD (1.8/2.8V) & 2\_1 & SPI\_CS \\ \hline
		1\_2 & VDDIO (1.8) & 2\_2 & SPI: SCK / I\textsuperscript{2}C: SCL \\ \hline
		1\_3 & GND & 2\_3 & SPI: MISO / I\textsuperscript{2}C: SDO \\ \hline
		1\_4 & GPIO0 & 2\_4 & SPI: MOSI /  I\textsuperscript{2}C: SDA \\ \hline
		1\_5 & GPIO1 & 2\_5 & GPIO4 \\ \hline
		1\_6 & GPIO2 & 2\_6 & GPIO5 \\ \hline
		1\_7 & GPIO3 & 2\_7 & IOXP\_INT\\ \hline
		     &       & 2\_8 & PlugDet \\ \hline
		     &       & 2\_9 & EEPROM\_RW \\ \hline
	\end{tabular}
	\caption{Overview of APP3.0 shuttle board pins and their function}
	\label{tab:shtbrdpins}
\end{table}
