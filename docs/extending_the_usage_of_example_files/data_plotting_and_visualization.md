\subsection{Data plotting and visualization}

When compiling an example to run on MCU (for example TARGET=MCU\_APP20, see above), the obtained sensor data can easily be plotted in the serial plotter of the Arduino IDE.

The example application must print the sensor data to be plotted in a text string, with a terminating new line character. Multiple sensor values per axis are possible. The \texttt{printf} command will stream the sensor data in an ASCII string via (virtual) COM port. Once the user connects to the COM port and opens the Arduino serial plotter, the data will be displayed in a graphical way.

Notes and hints:
\begin{itemize}
	\item If the user wants to use an other plotting software, he must consider that the DTR signal line must be set, otherwise the flashed application on the application board will not start running. The serial plotter and serial monitor of Arduino IDE set this signal automatically, other software (like HTerm) have the option to do this manually.
	\item The plotting window offers automatic re-sizing. If the user does not want this and needs fixed limits, he could plot the limits as additional lines. \\
	Example: \texttt{printf("\%d \%d \%d\textbackslash n", lower\_limit, sensor\_data, upper\_limit);}
	\item In case of sensor data with a high offset, such as the output of a barometric pressure sensor, which is usually around 100000 Pa, the user may want to substract a certain offset, so see details of the signal. \\
	Example: \texttt{printf("\%d\textbackslash n", (pressure - 99000));}
\end{itemize}

\begin{figure}[H]
	\begin{center}
		\includegraphics[width=0.9\textwidth]{coinesAPI_images/arduino_serial_plotter.png}
		\caption{Accelerometer sensor data on Arduino Serial Plotter}
	\end{center}
\end{figure}

\newpage
\section{Media Transfer Protocol (MTP) firmware for Application Board 3.0}

The external memory chip W25M02/W25N02 on APP3.0 is based on NAND flash.

FAT filesystem on NAND flash memory results in a complicated solution which uses of lot of RAM. Moreover use of FAT without Flash Translation Layer (to save RAM) wears out NAND flash with frequent usage. Hence the choice of [FlogFS](https://github.com/conservify/FLogFS), a filesystem optimized for use with NAND flash.

But the use of `FlogFS`, presents a new problem 'Filesystem access from PC via USB'. Use of `FlogFS` with USB Mass Storage protocol is not possible because operating system can't recognize `FlogFS` as a valid filesystem.

Use of custom protocol to do filesystem operations would mean re-inventing the wheel and a lot of effort. User also would not have the same experience as with USB Mass Storage.

Solution was to go with the "Media Transfer Protocol" developed initially by Microsoft for Portable Devices like MP3 players. Starting from Android Kitkat (v4.4),MTP is the only way to access files on an Android device since the whole flash memory (included user storage space) uses filesystems like ext4, YAFFS, F2FS, etc.,

Files in APP3.0 board's NAND flash memory can be viewed using the USB MTP firmware.

Supported on Windows, Linux, Android (via USB OTG) and macOS

\begin{figure}[H]
	\begin{center}
		\includegraphics[width=0.7\textwidth]{coinesAPI_images/MTP_windows.png}
	\end{center}
\end{figure}

\begin{figure}[H]
	\begin{center}
		\includegraphics[width=0.7\textwidth]{coinesAPI_images/MTP_Ubuntu_Nautilus.png}
	\end{center}
\end{figure}

\begin{figure}[H]
	\begin{center}
		\includegraphics[width=0.7\textwidth]{coinesAPI_images/MTP_Android_2.png}
	\end{center}
\end{figure}

\begin{figure}[H]
	\begin{center}
		\includegraphics[width=0.7\textwidth]{coinesAPI_images/MTP_Android_3.png}
	\end{center}
\end{figure}
