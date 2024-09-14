<H3>Enter Name:YUVARAJ V</H3>
<H3>Enter Register No:212223230252</H3>
<H3>Experiment-2</H3>
<H3>Date</H3>
<h1 align =center>Implementation of Exact Inference Method of Bayesian Network</h1>

## Program :
```
# Importing Library
from pgmpy.models import BayesianNetwork
from pgmpy.inference import VariableElimination
# Importing Library
from pgmpy.models import BayesianNetwork
from pgmpy.inference import VariableElimination
# Defining network structure

alarm_model = BayesianNetwork(
    [
        ("Burglary", "Alarm"),
        ("Earthquake", "Alarm"),
        ("Alarm", "JohnCalls"),
        ("Alarm", "MaryCalls"),
    ]
)

# Defining the parameters using CPT
from pgmpy.factors.discrete import TabularCPD

cpd_burglary = TabularCPD(
    variable="Burglary", variable_card=2, values=[[0.999], [0.001]]
)
cpd_earthquake = TabularCPD(
    variable="Earthquake", variable_card=2, values=[[0.998], [0.002]]
)
cpd_alarm = TabularCPD(
    variable="Alarm",
    variable_card=2,
    values=[[0.999, 0.71, 0.06, 0.05], [0.001, 0.29, 0.94, 0.95]],
    evidence=["Burglary", "Earthquake"],
    evidence_card=[2, 2],
)
cpd_johncalls = TabularCPD(
    variable="JohnCalls",
    variable_card=2,
    values=[[0.95, 0.1], [0.05, 0.9]],
    evidence=["Alarm"],
    evidence_card=[2],
)
cpd_marycalls = TabularCPD(
    variable="MaryCalls",
    variable_card=2,
    values=[[0.99, 0.3], [0.01, 0.7]],
    evidence=["Alarm"],
    evidence_card=[2],
)

# Associating the parameters with the model structure
alarm_model.add_cpds(
    cpd_burglary, cpd_earthquake, cpd_alarm, cpd_johncalls, cpd_marycalls
)
alarm_model.check_model()
inference=VariableElimination(alarm_model)
evidence={"JohnCalls":1,"MaryCalls":0}
query='Burglary'
res=inference.query(variables=[query],evidence=evidence)
print(res)
evidence2={"JohnCalls":1,"MaryCalls":1}
res2=inference.query(variables=[query],evidence=evidence2)
print(res2)
```
## Output :
### Res
![image](https://github.com/user-attachments/assets/bf0ad860-da47-472b-8c27-15f285ca3c24)
### Res 2
![image](https://github.com/user-attachments/assets/f1fba562-8fbe-46b4-bbdd-738c06b9dd4d)


## Result :
Thus, Bayesian Inference was successfully determined using Variable Elimination Method

