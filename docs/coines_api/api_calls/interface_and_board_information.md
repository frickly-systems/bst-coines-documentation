# coinesAPI calls: Interface and board information

\subsubsection{coines\_open\_comm\_intf}
Opens the communication interface.Currently only \texttt{COINES\_COMM\_INTF\_USB} (USB Connection) interface is available. \texttt{COINES\_COMM\_INTF\_BLE} is available for \texttt{MCU\_APP30} target.

In case of MCU Target, API waits indefinitely for serial port or BLE connection (\texttt{MCU\_APP30} target only).

In order to use \texttt{fprintf} and \texttt{fscanf} with BLE, \texttt{intf\_type} should be \texttt{COINES\_COMM\_INTF\_BLE}


\begin{lstlisting}
int16_t coines_open_comm_intf(enum coines_comm_intf intf_type,void *arg); 
\end{lstlisting}

\subsubsection{coines\_close\_comm\_intf}
Closes the communication interface.

\begin{lstlisting}
int16_t coines_close_comm_intf(enum coines_comm_intf intf_type,void *arg); 
\end{lstlisting}

\subsubsection{coines\_get\_board\_info}
Gets the board information.

\begin{lstlisting}
int16_t coines_get_board_info(struct coines_board_info *data);
\end{lstlisting}

The data structure contains the following items 

\begin{lstlisting}
struct coines_board_info {
	/*!Board hardware ID */
	uint16_t hardware_id;
	/*!Board software ID */
	uint16_t software_id;
	/*!Type of the board like APP2.0, Arduino Due*/
	uint8_t board;
	/*!Shuttle ID of the sensor connected*/
	uint16_t shuttle_id;
};
\end{lstlisting}
