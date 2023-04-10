# coinesAPI calls: GPIO oriented calls

\subsubsection{coines\_set\_pin\_config}
Sets the pin direction and the state.

\begin{lstlisting}
int16_t coines_set_pin_config(enum coines_multi_io_pin pin_number, enum coines_pin_direction direction, enum coines_pin_value pin_value);  
\end{lstlisting}

\subsubsection{coines\_get\_pin\_config}
Gets the pin configuration.

\begin{lstlisting}
int16_t coines_get_pin_config(enum coines_multi_io_pin pin_number, enum coines_pin_direction *pin_direction, enum coines_pin_value *pin_value);
\end{lstlisting}

\subsubsection{coines\_set\_shuttleboard\_vdd\_vddio\_config}
Configures the VDD and VDDIO of the sensor. For APP2.0, a voltage level of 0 or 3300 mV is supported. Any values above 0 will default to 3300 mV.

\begin{lstlisting}
int16_t coines_set_shuttleboard_vdd_vddio_config(uint16_t vdd_millivolt, uint16_t vddio_millivolt);
\end{lstlisting}

