\subsection{Key Features}

\subsubsection{USB DFU}

\begin{itemize}
	\item Code download to RAM or FLASH
	\item Code read back (upload) from  RAM or FLASH (Useful for taking firmware backups)
	\item Works with Windows, Linux, macOS and Android.
\end{itemize}

\subsubsection{BLE DFU}

\begin{itemize}
	\item Code download to FLASH.
	\item Works with PC and mobile devices with iOS/Android.
\end{itemize}

Bootloader was written taking into account the following aspects

\begin{itemize}
	\item Usability.
	\begin{enumerate}[label=\roman*.]
		\item No special driver installation or admin rights should be required.
		\item The update process should be straight forward.
	\end{enumerate}
	\item Maintainability
	\begin{enumerate}[label=\roman*.]
		\item Open source community takes care of PC side tools. For eg: dfu-util is a cross platform tool.
		\item Use Google Chrome's WebUSB to update firmware. Sample implementation \url{https://devanlai.github.io/webdfu/dfu-util/}
	\end{enumerate}
	\item Size
	\item COINES on MCU.
\end{itemize}
