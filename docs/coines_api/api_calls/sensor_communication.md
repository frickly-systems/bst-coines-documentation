# coinesAPI calls: Sensor communication

\subsubsection{coines\_config\_i2c\_bus}
Configures the I\textsuperscript{2}C bus. 

\begin{lstlisting}
int16_t coines_config_i2c_bus(enum coines_i2c_bus bus, enum coines_i2c_mode i2c_mode);
\end{lstlisting}

The first argument refers to the bus on the board. Currently, on APP2.0, there is only one bus available, so the argument is always COINES\_I2C\_BUS\_0.

The following I\textsuperscript{2}C modes are available:
\begin{lstlisting}
COINES_I2C_STANDARD_MODE
COINES_I2C_FAST_MODE
COINES_I2C_SPEED_3_4_MHZ
COINES_I2C_SPEED_1_7_MHZ
\end{lstlisting}

\subsubsection{coines\_config\_spi\_bus}
Configures the SPI bus of the board. The argument coines\_spi\_bus refers to the bus on the board. On APP2.0, there is only one bus available, so the user should only use COINES\_SPI\_BUS\_0. The SPI speed can be chosen in various discrete steps, as defined in enum coines\_spi\_speed in coines.h. (For example, COINES\_SPI\_SPEED\_2\_MHZ sets the SPI speed to 2 MHz.)

\begin{lstlisting}
int16_t coines_config_spi_bus(enum coines_spi_bus bus, uint32_t spi_speed, enum coines_spi_mode spi_mode);
\end{lstlisting}

\subsubsection{coines\_config\_i2s\_bus}
This API is used to configure the I\textsuperscript{2}S bus to match the TDM configuration

\begin{lstlisting}
int16_t coines_config_i2s_bus(uint16_t data_words, coines_tdm_callback callback);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{data\_words}: number of words to use in the buffer. Max is set at COINES\_TDM\_BUFFER\_SIZE\_WORDS.
	\item \texttt{callback}: register a callback to be called to process and copy the data.
\end{itemize}

\subsubsection{coines\_deconfig\_spi\_bus}
This API is used to de-configure the SPI bus

\begin{lstlisting}
int16_t coines_deconfig_spi_bus(enum coines_spi_bus bus);
\end{lstlisting}

\subsubsection{coines\_deconfig\_i2c\_bus}
This API is used to de-configure the I\textsuperscript{2}C bus

\begin{lstlisting}
int16_t coines_deconfig_i2c_bus(enum coines_i2c_bus bus);
\end{lstlisting}

\subsubsection{coines\_deconfig\_i2s\_bus}
This API is used to stop the I\textsuperscript{2}S/TDM interface from reading data from the sensor

\begin{lstlisting}
void coines_deconfig_i2s_bus(void);
\end{lstlisting}

\subsubsection{coines\_write\_i2c}
Writes 8-bit register data to the I\textsuperscript{2}C device at \texttt{COINES\_I2C\_BUS\_0}.

\begin{lstlisting}
int8_t coines_write_i2c(enum coines_i2c_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{bus}: I\textsuperscript{2}C bus to be used
	\item \texttt{dev\_addr}: I\textsuperscript{2}C device address.
	\item \texttt{reg\_addr}: Starting address for writing the data.
	\item \texttt{reg\_data}: Data to be written.
	\item \texttt{count}: Number of bytes to write.
\end{itemize}

\subsubsection{coines\_read\_i2c}
Reads 8-bit register data from the I\textsuperscript{2}C device at \texttt{COINES\_I2C\_BUS\_0}.

\begin{lstlisting}
int8_t coines_read_i2c(enum coines_i2c_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{bus}: I\textsuperscript{2}C bus to be used
	\item \texttt{dev\_addr}: I\textsuperscript{2}C device address.
	\item \texttt{reg\_addr}: Starting address for reading the data.
	\item \texttt{reg\_data}: Buffer to take up the read data.
	\item \texttt{count}: Number of bytes to read.
\end{itemize}

\subsubsection{coines\_write\_spi}
Writes 8-bit register data to the SPI device at \texttt{COINES\_SPI\_BUS\_0}.

\begin{lstlisting}
int8_t coines_write_spi(enum coines_spi_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{bus}: SPI bus to be used.
	\item \texttt{dev\_addr}: Chip select pin number.
	\item \texttt{reg\_addr}: Starting address for writing the data.
	\item \texttt{reg\_data}: Data to be written.
	\item \texttt{count}: Number of bytes to write.
\end{itemize}

\subsubsection{coines\_read\_spi}
Reads 8-bit register data from the SPI device at \texttt{COINES\_SPI\_BUS\_0}.

\begin{lstlisting}
int8_t coines_read_spi(enum coines_spi_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{bus}: SPI bus to be used.
	\item \texttt{dev\_addr}: Chip select pin number.
	\item \texttt{reg\_addr}: Starting address for reading the data.
	\item \texttt{reg\_data}: Buffer to take up the read data.
	\item \texttt{count}: Number of bytes to read.
\end{itemize}

\subsubsection{coines\_config\_word\_spi\_bus}
Configures the SPI bus parameters speed, mode, 8-bit/16-bit transfer ( \texttt{COINES\_SPI\_TRANSFER\_8BIT / COINES\_SPI\_TRANSFER\_16BIT} ).

\begin{lstlisting}
int16_t coines_config_word_spi_bus(enum coines_spi_bus bus, enum coines_spi_speed spi_speed, enum coines_spi_mode spi_mode, enum coines_spi_transfer_bits spi_transfer_bits);
\end{lstlisting}


\subsubsection{coines\_write\_16bit\_spi}\label{16bitWrite}
Writes 16-bit register data to the SPI device at \texttt{COINES\_SPI\_BUS\_0}.

\begin{lstlisting}
int8_t coines_write_16bit_spi(enum coines_spi_bus bus, uint8_t cs, uint16_t reg_addr, void *reg_data, uint16_t count);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{bus}: SPI bus to be used.
	\item \texttt{cs}: Chip select pin number.
	\item \texttt{reg\_addr}: Starting address for writing the data.
	\item \texttt{reg\_data}: Data to be written.
	\item \texttt{count}: Number of bytes to write.
\end{itemize}

\subsubsection{coines\_read\_16bit\_spi}\label{16bitRead}
Reads 16-bit register data from the SPI device at \texttt{COINES\_SPI\_BUS\_0}.

\begin{lstlisting}
int8_t coines_read_16bit_spi(enum coines_spi_bus bus, uint8_t cs, uint16_t reg_addr, void *reg_data, uint16_t count);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{bus}: SPI bus to be used.
	\item \texttt{cs}: Chip select pin number.
	\item \texttt{reg\_addr}: Starting address for reading the data.
	\item \texttt{reg\_data}: Buffer to take up the read data.
	\item \texttt{count}: Number of bytes to read.
\end{itemize}

\subsubsection{coines\_delay\_msec}
Introduces delay in millisecond.

\begin{lstlisting}
void coines_delay_msec(uint32_t delay_ms);
\end{lstlisting}

\subsubsection{coines\_delay\_usec}
Introduces delay in microsecond.

\begin{lstlisting}
void coines_delay_usec(uint32_t delay_us);
\end{lstlisting}

