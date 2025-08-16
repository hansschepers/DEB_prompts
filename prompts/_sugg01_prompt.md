I am a PhD in mathematical biology, and would like to learn how the
Dynamic Energy Budget (DEB) modelling and parameter identification is done in this example.

look at this matlab code, start with the file starting with 'run_'.

Answer the following 6 questions (Question 2 in a mermaid artefact, Question 6 as in-stream markdown)
when this model is run and fitted:

1. Look up the latin species name for the organism, and give the English common name, as well as the genus, Family, Order, Class, Subphylum and Phylum), in a two column table.
2. Draw a function dependency graph in mermaid, of functions defined here (stop at the first matlab-native level) - mind the mermaid instructions above 
3. Explain what numerical schemes are used: ode integration method, analytic expressions for certain phases of animal development? integrals? root finding for certain steps?
4. Does the fit routine fit multiple data sets? Start answer with bare integer for "How many?", then elaborate a bit
5. Does this simulation run actually consists of multiple models (algebraic, ODEs) stitched together? 
are these in series or in a DAG? 
how are final states from one step translated into initial conditions for the next?
6. Please characterize this model fitting setup by filling out the following table. 
For each category, provide specific numbers and details, do not abbreviate counts to something like "10+"


| Characteristic | Count/Type | Details | Units/Examples |
|---|---|---|---|
| **Data Structure** |
| Total datasets | # | List dataset names/types | |
| Zero-variate responses | # | Single point measurements | |
| Uni-variate responses | # | Time series or curves | |
| Total response variables | # | All measured variables | |
| Distinct physical units | # | Different measurement scales | List units |
| **Temporal Structure** |
| Time points per uni-variate | # each | For each time series | |
| Time ranges | [min, max] | For each time series | |
| Total data points | # | Sum across all datasets | |
| **Optimization Structure** |
| Cost function outputs | scalar/vector | Single value or multiple objectives | |
| Optimization type | single/multi | Based on cost function structure | |
| **Weighting Scheme** |
| Default weights (≠1) | # | Non-unity baseline weights | |
| Modified weights | # | Explicitly adjusted weights | Factor applied |
| Pseudodata points | # | Regularization constraints | |
| **Parameter Structure** |
| Free parameters | # | Parameters being fitted | |
| Fixed parameters | # | Held constant during fitting | |
| Parameter bounds | # | Constrained parameters | |

---
