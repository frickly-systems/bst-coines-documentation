# coinesAPI calls: Streaming feature

Note :
\begin{enumerate}
\item The below APIs are supported only on PC Target.
\item A simpler approach of using \texttt{coines\_attach\_interrupt()} API for is available for MCU.
\end{enumerate}


\subsubsection{coines\_config\_streaming}
Sets the configuration for streaming sensor data.

\begin{lstlisting}
int16_t coines_config_streaming(uint8_t channel_id, struct coines_streaming_config *stream_config, struct coines_streaming_blocks *data_blocks); 
\end{lstlisting}

Arguments:
\begin{itemize}
\item \texttt{channel\_id}: An integer number that can be used as identifier/index to the sensor data that will be streamed for this setting

\item \texttt{stream\_config}: Contains information regarding interface settings and streaming configuration.
\item  \texttt{coines\_streaming\_blocks}: Contains information regarding numbers of register blocks, range and size of  each block.
\end{itemize}
Note:\newline
The below parameters should always be set:
	\begin{itemize}
		\item \texttt{data\_block.no\_of\_blocks}: number of blocks to stream (must at least be one)
		\item For each block b:
		\begin{itemize}
			\item \texttt{data\_block.reg\_start\_addr[b]}: start address of the block in the register map
			\item \texttt{stream\_block.no\_of\_data\_bytes[b]}: number of addresses to read, starting from the start address
		\end{itemize}
	\end{itemize}

For reading data from I\textsuperscript{2}C bus,then set the below parameters:
	
	\begin{itemize}
		\item \texttt{stream\_config.intf = COINES\_SENSOR\_INTF\_I2C;}
		\item \texttt{stream\_config.i2c\_bus}: I\textsuperscript{2}C bus (in case of APP2.0, this is always \texttt{COINES\_I2C\_BUS\_0})
		\item \texttt{stream\_config.dev\_addr}: I\textsuperscript{2}C address of the sensor
	\end{itemize}
For reading data from SPI bus, then set the below parameters:
	\begin{itemize}
		\item \texttt{stream\_config.intf = COINES\_SENSOR\_INTF\_SPI;}
		\item \texttt{stream\_config.spi\_bus}: SPI bus (in case of APP2.0, this is always \texttt{COINES\_SPI\_BUS\_0})
		\item \texttt{stream\_config.cs\_pin}: CS pin of the sensor, information can be obtained from the shuttle board documentation for the sensor. 
	\end{itemize}
When polling mode is requested, set the below parameters:
	\begin{itemize}
		\item \texttt{stream\_config.sampling\_units}: \\ either milliseconds (\texttt{COINES\_SAMPLING\_TIME\_IN\_MILLI\_SEC}) \\ or microseconds (\texttt{COINES\_SAMPLING\_TIME\_IN\_MICRO\_SEC})
		\item \texttt{stream\_config.sampling\_time}: sampling period in the unit as defined in \\ \texttt{stream\_config.sampling\_units}
	\end{itemize}
When interrupt mode is requested, set the below parameters:
	\begin{itemize}
		\item \texttt{stream\_config.int\_pin}: pin of the interrupt which shall trigger the sensor read-out. If the interrupt output of the sensor is used, the required information about the pin number can be obtained from the shuttle board documentation for the sensor.
		\item \texttt{stream\_config.int\_timestamp}:  it can be configured if the sensor data is tagged with a timestamp (\texttt{COINES\_TIMESTAMP\_ENABLE}) or not (\texttt{COINES\_TIMESTAMP\_DISABLE}).
	\end{itemize}

\subsubsection{coines\_start\_stop\_streaming}
Starts or stops sensor data streaming.

\begin{lstlisting}
int16_t coines_start_stop_streaming(enum coines_streaming_mode stream_mode, uint8_t start_stop);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{stream\_mode}: streaming mode (either \texttt{COINES\_STREAMING\_MODE\_POLLING} or \\ \texttt{COINES\_STREAMING\_MODE\_INTERRUPT})
	\item \texttt{start\_stop}: flag to either start (\texttt{COINES\_STREAMING\_START}) or stop (\texttt{COINES\_STREAMING\_STOP}) the streaming
\end{itemize}

\subsubsection{coines\_read\_stream\_sensor\_data}
Reads the data streamed from the sensor.

\begin{lstlisting}
int16_t coines_read_stream_sensor_data(uint8_t sensor_id, uint32_t number_of_samples, uint8_t *data, uint32_t *valid_samples_count);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{sensor\_id}: id of the sensor 
	\item \texttt{number\_of\_samples}: number of samples the user wishes to read (not implemented)
	\item \texttt{data}: data buffer
	\begin{itemize} 
	   \item Interrupt streaming - Packet counter + Register data + Timestamp
	   \item Polling streaming - Register data
	\end{itemize}
	\item \texttt{valid\_samples\_count}: number of samples the user has actually received (may be less than \texttt{number\_of\_samples})
\end{itemize}

Example of a packet:

\begin{figure}[h]
	\includegraphics[width=\textwidth]{coinesAPI_images/COINES_streamingSample}
	\caption{Format of streaming packages}
\end{figure}

In the above figure, the following meaning apply to the mentioned abreviations:
\begin{itemize}
	\item r\textsubscript{p}: Value at register address p
	\item a: Size of register block–0
	\item r\textsubscript{p+a}: Value at register address p
\end{itemize}

Similarly is the case for r\textsubscript{q}, j and r\textsubscript{q+j}. See the \texttt{coines\_streaming\_blocks} structure for information regarding register blocks.

The packet counter and the timestamp can be obtained as follows:

\begin{itemize}
	\item[] \texttt{packet\_counter = (byte3\_c << 24) | (byte2\_c << 16) | (byte1\_c << 8) | (byte0\_c)}
	\item[] \texttt{timestamp = (byte5\_t << 40) | (byte4\_t << 32) | (byte3\_t << 24) | (byte2\_t << 16) | (byte1\_t << 8) | (byte0\_t)}
\end{itemize}

The 48-bit timestamp is enabled by using \\ \texttt{coines\_trigger\_timer(COINES\_TIMER\_START,  COINES\_TIMESTAMP\_ENABLE);}

Timestamp in microseconds can be obtained using below formula:
\begin{itemize}
	\item[] $\displaystyle Timestamp\ (\mu s) = \frac{48bit\_timestamp}{30}$
\end{itemize}

\subsubsection{coines\_trigger\_timer}
Triggers the timer in firmware and also enables or disables the time stamp feature.

\begin{lstlisting}
int16_t coines_trigger_timer(enum coines_timer_config tmr_cfg,enum coines_time_stamp_config ts_cfg);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{tmr\_cfg}: start, stop or reset the timer (\texttt{COINES\_TIMER\_START}, \texttt{COINES\_TIMER\_STOP} or \\ \texttt{COINES\_TIMER\_RESET}) 
	\item \texttt{ts\_cfg}: Enables/disables microcontroller timestamp  (\texttt{COINES\_TIMESTAMP\_ENABLE} or \\ \texttt{COINES\_TIMESTAMP\_DISABLE}) 
\end{itemize}

