\clearpage\section{Hyper-parameter Tuning of Neural Networks}\label{NE2}

\subsection{Model Configuration}
This section describes the methodology used and the evaluation of a neural network model trained with 22 controlpoint point coordinates as inputs and outputs of two sizes are mapped to the corresponding interpolated pressure $p$, $\tau_1$ and $\tau_2$. 
\\

\noindent Number of interpolation points are varied from 100 to 200 for each surface in order to study its effect against model's accuracy when tested under the unseen test dataset. The influence of number of training examples on the accuracy of the model is also explored using  pre-defined configuration details.
The following Table \ref{tab:model12} lists the model configuration that was kept constant during the evaluation phase:

\begin{table}[h!]
	\centering
	\begin{tabular}{@{}ll@{}}
		\toprule
		\textbf{Configuration Parameter} & \textbf{Value} \\
		\midrule
		Batch Size & 10\\
		Epochs & 100\\
		Optimizer & Adam\\
		Activation Function & ReLU\\
		Loss Function & Quadratic\\
		Stopping Criteria & Early Stopping\\
		Tolerance($\epsilon$) & $10^{-3}$\\
		Number of Inputs & 22 (Controlpoint coordinates) \\
		Number of Outputs & {200, 100} ($p$, $\tau_1$ \& $\tau_2$ values) \\
		\bottomrule
	\end{tabular}
	\caption{Constant Model Configuration Parameters}\label{tab:model12}	
\end{table}

\noindent Following Table \ref{tab:hyperparameters} summarizes the hyperparameters that were tuned, the range of values that they were tested with.

\begin{table}[h!]
	\centering
	\begin{tabular}{@{}lll@{}}
		\toprule
		\textbf{Hyperparameter} & \textbf{Tuned Values} & \textbf{Comments} \\
		\midrule
		Number of Layers & $\{1, 2, 3, 4, 5\}$ & Increasing complexity \\
		Neurons per Layer & $\{10, 20, 30, ..., 200\}$ & Increasing capacity \\			
		Dataset Size & $\{20, 40, 60, 80, 160, 320, ....2560 \}$ & Varying amounts of training data \\
		\bottomrule
	\end{tabular}
	\caption{Summary of Tuned Hyperparameters}\label{tab:hyperparameters}
\end{table}

\noindent Based on the above Hyper parameter tuning, $p$, $\tau_1$ \& $\tau_2$ were separately trained as the physics these quantities are not a like, hence would not give good results. A detailed analysis on the reason behind choosing this selected model architecture can be found at \cite{balla2021}, where the author has shown the decrement of the mean value of the error for the given architecture considered. Each of the trained model was saved and predictions were performed against the test set for evaluating the performance of the trained model. 
\\

\subsection{Model Performance}
 \noindent The performance of the trained NN is assessed by looking at the maximum relative error $R^2$ which is given by :

\begin{equation}
	R^2 = 1 - \dfrac{\sum_{i=1}^n (y_i - \hat{y}_i)^2}{\sum_{i=1}^n (y_i - \bar{y})^2}
\end{equation}

\noindent In terms of analysing the model accuracy when compared to the Target Data, computing relative L2 Norm Error keeping interpolated solver data as reference was providing better information on how the dataset size was in-fact a dependent hyperparameter for model accuracy. 
\\

\noindent It is because the R2 score of the models are scored very low till the dataset size were 640 for $\tau_2$ as it suffered to learn due to major nonlinearities involved in $\tau_2$. Below are the attached R2 Score contours Figures \ref{fig:r2plots} for models trained with dataset size of only 1280 and 2560 which is a full dataset size. Model performance for lean dataset size of just 20 cases  is compared against models trained with full dataset size in Figure ~\ref{fig:wrstcase1} and Figure ~\ref{fig:bstcase1} respectively. 
\\
