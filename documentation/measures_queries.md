# Measures Used in Healthcare Dashboard

## DateTable:
```
DateTable = 
ADDCOLUMNS(
 CALENDARAUTO(),
 "Year", YEAR([Date]),
 "Month", FORMAT([Date], "mmm"),
 "Monthnum", MONTH([Date]),
 "Weekday", FORMAT([Date], "ddd"),
 "Weeknum", WEEKDAY([Date]),
 "Qtr", "Q-"&FORMAT([Date], "Q"),
 "WeekType",IF(WEEKDAY([Date])=1 || WEEKDAY([Date])=7,
 "Weekend", "Weekday"

))
```

# DAX MEASURES:

## % Department:
```
% Department = 
DIVIDE(
    [Total Billing Amount],
    CALCULATE(
        [Total Billing Amount],
        ALL(departments[Department])
    )
)
```

## % Procedure:
```
% Procedure = 
DIVIDE(
    [Total Billing Amount],
    CALCULATE(
        [Total Billing Amount],
        ALL(procedures[Procedure])
    )
)
```

## Active Department:
```
Active Department = SELECTEDVALUE(departments[Department])
```

# AVERAGE MEASURES:

## Average Billing Amount per Visit
```
Average Billing Amount per Visit = 
DIVIDE(
    [Total Billing Amount], [Total Patients]
)
```

## Average Insurance Coverage
```
Average Insurance Coverage = AVERAGE(visits[Insurance Coverage])
```

## Average Length of Stay
```
Average Length of Stay = AVERAGE(visits[Length of Stay])
```

## Average Medication Cost
```
Average Medication Cost = AVERAGE (visits[Medication Cost])
```

## Average Out-of-Pocket
```
Average Out-of-Pocket = 
DIVIDE(
    [Out-of-Pocket], [Total Patients]
)
```

## Average Patient Satisfaction Score
```
Average Patient Satisfaction Score = AVERAGE(visits[Patient Satisfaction Score])
```

## Average Room Charge
```
Average Room Charge = 
    DIVIDE(
        [Total Room Charges], [Total Patients]
    )
```

## Average Treatment Cost
```
Average Treatment Cost = AVERAGE(visits[Treatment Cost])
```


# BASIC MEASURES:

## Out-of-Pocket
```
Out-of-Pocket = [Total Billing Amount] - [Total Insurance Coverage]
```

## Total Billing Amount
```
Total Billing Amount = 
    [Total Medication Cost] + 
    [Total Room Charges] +
    [Total Treatment Cost]
```

## Total Insurance Coverage
```
Total Insurance Coverage = SUM(visits[Insurance Coverage])
```

## Total Medication Cost
```
Total Medication Cost = sum(visits[Medication Cost])
```

## Total Patients
```
Total Patients = DISTINCTCOUNT(patients[Patient ID])
```

## Total Room Charges
```
Total Room Charges = 
SUMX(
    visits,
    visits[Room Charges(daily rate)] * 
    visits[Length of Stay]
)
```

## Total Treatment Cost
```
Total Treatment Cost = SUM(visits[Treatment Cost])
```