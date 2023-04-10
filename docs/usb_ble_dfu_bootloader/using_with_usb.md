\subsection{Using the Bootloader via USB}

Write firmware to Flash memory using following command
\begin{itemize}
	\item dfu-util -a FLASH -D fw.bin -R
\end{itemize}

Write firmware to RAM memory using following command
\begin{itemize}
	\item dfu-util -a RAM -D fw.bin -R
\end{itemize}

Read firmware from Flash memory using following command
\begin{itemize}
	\item dfu-util -a FLASH -U fw\_bkup.bin
\end{itemize}

Read firmware from RAM memory using following command
\begin{itemize}
	\item dfu-util -a RAM -U fw\_bkup.bin
\end{itemize}

Read device serial number/ BLE MAC address
\begin{itemize}
	\item dfu-util -l
\end{itemize}

