\subsection{Using the Bootloader via BLE}

\begin{itemize}
	\item PC (Windows/Linux and macOS)
	\newline Python script present in following path \path{COINES\v2.6.0\tools\app30-ble-dfu} can use the binary file directly.
	\begin{enumerate}[label=\roman*.]
		\item Scan for devices to find BLE MAC address using below command
		\begin{itemize}
			\item python app30-ble-dfu.py -l
		\end{itemize} 
		\item Update firmware by using MAC address obtained in the previous step and firmware BIN file
		\begin{itemize}
			\item python app30-ble-dfu.py -d D7:A3:CE:8E:36:14 -f firmware.bin
		\end{itemize}
	\end{enumerate}
	\item Android devices
	\begin{enumerate}[label=\roman*.]
		\item Generate ZIP package using \url{https://pypi.org/project/adafruit-nrfutil/} before using nRF ToolBox for BLE or nRF connect for mobile.
		\begin{itemize}
			\item adafruit-nrfutil dfu genpkg --dev-type 0x0052 --application firmware.bin dfu-package.zip
		\end{itemize} 
	\end{enumerate}
\end{itemize}

