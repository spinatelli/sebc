# YARN and Resource Management

Inserted numbers into 0_YarnCalcs.xlsx:

```
Worker vcores   20
Worker spindles 12
Worker RAM  128
Workload factor 2
Worker nodes    10
```

The workload factor represents the number of mappers and reducers to run for every worker node. This means that 1 will run 1 map task for every worker node, 2 will run 2, 4 will run 4. Same thing for reduce tasks. In the calculator tool, the number is actually used only if it's lower than the number computed dividing available memory by the minimum memory allocation per task, and lower than the number computed dividing the available vcores by the minimum vcore allocation per task. E.g., by setting it to 2, it means 20 mapper tasks should be used, but since there are 15 vcores available and 1 vcore is used for each task, only 15 mappers should be used.