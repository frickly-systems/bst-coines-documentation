# coinesAPI calls: Other useful APIs

\subsubsection{coines\_get\_millis}
Returns the number of milliseconds passed since the program started

\begin{lstlisting}
uint32_t coines_get_millis();
\end{lstlisting}

\subsubsection{coines\_get\_micro\_sec}
Returns the number of microseconds passed since the program started

\begin{lstlisting}
uint64_t coines_get_micro_sec();
\end{lstlisting}

\subsubsection{coines\_attach\_interrupt}
Attaches an interrupt to a Multi-IO pin.Works only on MCU.

\begin{lstlisting}
void coines_attach_interrupt(enum coines_multi_io_pin pin_number,void (*callback)(uint32_t, uint32_t),enum coines_pin_interrupt_mode int_mode);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{pin\_number}:  Multi-IO pin
	\item \texttt{callback}: Name of the function to be called on detection of interrupt
	\item \texttt{int\_mode}: Trigger modes - change (\texttt{COINES\_PIN\_INTERRUPT\_CHANGE}), \\
	rising edge (\texttt{COINES\_PIN\_INTERRUPT\_RISING\_EDGE}), \\falling edge (\texttt{COINES\_PIN\_INTERRUPT\_FALLING\_EDGE})
\end{itemize}

\subsubsection{coines\_detach\_interrupt}
Detaches interrupt from a Multi-IO pin.Works only on MCU.

\begin{lstlisting}
void coines_detach_interrupt(enum coines_multi_io_pin pin_number);
\end{lstlisting}

\subsubsection{coines\_intf\_available}
Return the number of bytes available in the read buffer of the interface.Works only on APP3.0 MCU target.

\begin{lstlisting}
uint16_t coines_intf_available(enum coines_comm_intf intf);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{intf}: Type of interface (USB, COM, or BLE)
\end{itemize}

\subsubsection{coines\_intf\_connected}
Check if the interface is connected.Works only on APP3.0 MCU target.

\begin{lstlisting}
bool coines_intf_connected(enum coines_comm_intf intf);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{intf}: Type of interface (USB, COM, or BLE)
\end{itemize}

\subsubsection{coines\_flush\_intf}
Flush the write buffer.Works only on APP3.0 MCU target.

\begin{lstlisting}
void coines_flush_intf(enum coines_comm_intf intf);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{intf}: Type of interface (USB, COM, or BLE)
\end{itemize}

\subsubsection{coines\_read\_intf}
Read data over the specified interface.Works only on APP3.0 MCU target.

\begin{lstlisting}
uint16_t coines_read_intf(enum coines_comm_intf intf, void *buffer, uint16_t len);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{intf}: Type of interface (USB, COM, or BLE)
	\item \texttt{buffer}: Pointer to the buffer to store the data
	\item \texttt{len}: Length of the buffer
\end{itemize}

\subsubsection{coines\_write\_intf}
Write data over the specified interface.Works only on APP3.0 MCU target.

\begin{lstlisting}
uint16_t coines_write_intf(enum coines_comm_intf intf, void *buffer, uint16_t len);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{intf}: Type of interface (USB, COM, or BLE)
	\item \texttt{buffer}: Pointer to the buffer storing the data
	\item \texttt{len}: Length of the buffer
\end{itemize}

\subsubsection{coines\_get\_version}
Returns pointer to COINES version string

\begin{lstlisting}
char* coines_get_version(void);
\end{lstlisting}

\subsubsection{coines\_soft\_reset}
Resets the device. After reset device jumps to the address specified in makefile(APP\_START\_ADDRESS).

\begin{lstlisting}
void coines_soft_reset(void);
\end{lstlisting}

\subsubsection{coines\_read\_temp\_data}
This API is used to read the temperature sensor data.

\begin{lstlisting}
int16_t coines_read_temp_data(float *temp_data);
\end{lstlisting}
        
Arguments:
\begin{itemize}
	\item \texttt{temp\_conv\_data}: Buffer to retrieve the sensor data in degree Celsius.
\end{itemize}

\subsubsection{coines\_read\_bat\_status}
This API is used to read the battery status.

\begin{lstlisting}
int16_t coines_read_bat_status(uint16_t *bat_status_mv, uint8_t *bat_status_percent);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{bat\_status\_mv}: Buffer to retrieve the battery status in millivolt
	\item \texttt{bat\_status\_percent}: Buffer to retrieve the battery status in percentage
\end{itemize}

\subsubsection{coines\_ble\_config}
This API is used to configure BLE name and power. It should be called before calling coines\_open\_comm\_intf API.

\begin{lstlisting}
int16_t coines_ble_config(struct coines_ble_config *ble_config);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{ble\_config}: structure holding ble name and power details
\end{itemize}

\subsubsection{coines\_set\_led}
 This API is used to set led state(on or off).
 
\begin{lstlisting}
int16_t coines_set_led(enum coines_led led,enum coines_led_state led_state);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{led}: led to which the state has to be set.
	\item \texttt{led\_state}: state to be set to the given led.
\end{itemize}

\subsubsection{coines\_timer\_config}
 This API is used to configure the hardware timer.
 
\begin{lstlisting}
int16_t coines_timer_config(enum coines_timer_instance instance, void* handler);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{instance}: timer instance.
	\item \texttt{handler}: callback to be called when timer expires.
\end{itemize}

\subsubsection{coines\_timer\_start}
 This API is used to start the configured hardware timer.
 
\begin{lstlisting}
int16_t coines_timer_start(enum coines_timer_instance instance, uint32_t timeout);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{instance}: timer instance.
	\item \texttt{timeout}: timeout in microseconds.
\end{itemize}

\subsubsection{coines\_timer\_stop}
 This API is used to stop the  hardware timer.
 
\begin{lstlisting}
int16_t coines_timer_stop(enum coines_timer_instance instance);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{instance}: timer instance.
\end{itemize}

\subsubsection{coines\_get\_realtime\_usec}
This API is used to get the current counter(RTC) reference time in usec

\begin{lstlisting}
uint32_t coines_get_realtime_usec(void);
\end{lstlisting}

\subsubsection{coines\_delay\_realtime\_usec}
This API is used to introduce delay based on high precision RTC(LFCLK crystal) with the resolution of 30.517 usec.

\begin{lstlisting}
void coines_delay_realtime_usec(uint32_t period);
\end{lstlisting}

Arguments:
\begin{itemize}
	\item \texttt{period}: required delay in microseconds 
\end{itemize}

\newpage
\section{Extending the usage of the example files}

