# **Hyper-Parameter Tuning of Neural Networks**

## **Overview**
This section describes the methodology used for evaluating a neural network model trained with **22 control point coordinates** as inputs. The outputs consist of interpolated pressure $p $, $\tau_1$, and $\tau_2$. The number of interpolation points varies between **100** and **200** for each surface to evaluate the effect of data size on model accuracy under unseen test data. The influence of the dataset size on model accuracy is also explored.

---

## **1. Model Configuration**

The following table lists the **constant model configuration parameters** during the evaluation phase:

| **Configuration Parameter** | **Value**                |
|-----------------------------|-------------------------|
| Batch Size                   | 10                      |
| Epochs                       | 100                     |
| Optimizer                    | Adam                    |
| Activation Function          | ReLU                    |
| Loss Function                | Quadratic               |
| Stopping Criteria            | Early Stopping          |
| Tolerance (\( \epsilon \))   | ![equation](https://latex.codecogs.com/svg.image?\color{White}10^{-3}) |
| Number of Inputs             | 22 (Control point coordinates) |
| Number of Outputs            | {200, 100} (\( p \), \(\tau_1\), and \(\tau_2\)) |

---

## **2. Hyperparameters and Tuning**

The following table summarizes the **hyperparameters** that were tuned and the corresponding ranges of values tested:

| **Hyperparameter** | **Tuned Values**                     | **Comments**                |
|--------------------|---------------------------------------|-----------------------------|
| Number of Layers   | ![equation](https://latex.codecogs.com/svg.image?\color{White}\{1,2,3,4,5\}) | Increasing model complexity |
| Neurons per Layer  | ![equation](https://latex.codecogs.com/svg.image?\color{White}\{10,20,30,...,200\}) | Increasing model capacity   |
| Dataset Size       | ![equation](https://latex.codecogs.com/svg.image?\color{White}\{20,40,60,...,2560\}) | Varying amounts of training data |

---

## **3. Model Training and Evaluation**

Based on the **hyperparameter tuning**, separate neural networks were trained for \( p \), \(\tau_1\), and \(\tau_2\) since these physical quantities differ in complexity and behavior. A detailed analysis of the chosen architecture can be found in [Balla et al., 2021], where the reduction in the mean error value for the given architecture is demonstrated.

Each trained model was saved, and predictions were performed on the **test set** to evaluate performance.

---

## **4. Model Performance**

The performance of the trained neural network is assessed using the **\( R^2 \) score**, defined as:

![equation](https://latex.codecogs.com/svg.image?\color{White}R^2%20=%201%20-%20\frac{\sum_{i=1}^n%20(y_i%20-%20\hat{y}_i)^2}{\sum_{i=1}^n%20(y_i%20-%20\bar{y})^2})

where:
- \( y_i \) represents the actual values.
- \( \hat{y}_i \) represents the predicted values.
- \( \bar{y} \) represents the mean of the actual values.

---

### **Key Observations:**
1. For the $ \tau_2$ model, the $R^2$ score remained low until the dataset size reached **640**, indicating that more data was required due to significant non-linearities in $\tau_2$.
2. **Relative $L2$ -Norm Error** was computed using solver-interpolated data as a reference, which provided better insights into the dependence of model accuracy on dataset size.

---

## **5. Results and Comparisons**

Below are visualizations comparing **$R^2$ contours** for models trained with dataset sizes of **1280** and **2560** (full dataset):

### **Model Comparisons:**
- **Figure 1:** Model performance for a dataset size of only **20 cases**.
- **Figure 2:** Comparison with models trained on the **full dataset**.

---

## **6. Conclusion**
- Neural networks trained for $p$, $\tau_1$, and $\tau_2$ require separate architectures due to differences in complexity.
- Increasing the **dataset size** significantly improves the performance, especially for complex quantities like \(\tau_2\).
- Tuning the number of layers and neurons improved the model’s ability to generalize, especially for **interpolation points ranging from 100 to 200**.

---

## **References**
- Balla et al. (2021): For detailed architecture analysis and error reduction strategies.
