# Driving Declinometer and Vehicle Weight Estimation
Knowing the weight of a vehicle and the slope of the road would be beneficial for many 
driver assistance systems. For example, the information could be used to improve power 
management or plan routes based on weight restrictions. 

Unfortunately, installing additional sensors to measure weight and slope directly is 
expensive. However, vehicles already track properties like engine power and speed that 
depend strongly on the unknown quantities. These could be used as input for a software 
"sensor" that is much cheaper than a hardware solution.

**- Can you accurately predict weight and slope using signals that already exist on a 
vehicle?**

## Data description

The data contains eleven signals from the vehicle. The first nine signals can be used as input for the prediction, the last two are the desired output:

- Epm_nEng_100ms : average engine speed of one cylinder segment (rpm)
- VehV_v_100ms : vehicle speed (km/h)
- ActMod_trqInr_100ms : current, back-calculated inner engine torque (Nm)
- RngMod_trqCrSmin_100ms : minimum engine torque at the crankshaft level (Nm)
- CoVeh_trqAcs_100ms : torque demand of accessories (Nm)
- Clth_st_100ms : debounced status of clutch (-)
- CoEng_st_100ms : engine operation status (enum, 0 COENG_STANDBY, 1 COENG_READY, 2 COENG_CRANKING, 3 COENG_RUNNING, 4 COENG_STOPPING, 5 COENG_FINISH)
- Com_rTSC1VRVCURtdrTq_100ms : desired torque or torque limit (%)
- Com_rTSC1VRRDTrqReq_100ms : torque requested by retarder (%)
- RoadSlope_100ms : actual slope from the ADASIS horizon (%, tan(slope) = (RoadSlope_100ms / 100))
- Vehicle_Mass: the weight of the vehicle, either 38 t or 49 t
    
# Evaluation
## Predicted Slope
- Compute the absolute error for each prediction
  
  ![image](https://github.com/CapHaTri/Driving-Declinometer-and-Vehicle-Weight-Estimation/assets/113035712/d1f96d77-6e30-4acb-87ef-fdeeb1e633b2)
  
  where ***yp*** is the predicted slope and ***yt*** the actual slope (in %)

## Predicted Weight
- Compute the recall for each class i ∈ {0, 1} (corresponding to 38 t and 49 t)
  
  ![image](https://github.com/CapHaTri/Driving-Declinometer-and-Vehicle-Weight-Estimation/assets/113035712/ba692897-0a7d-45ed-a6a1-a836c5d71948)

  where $TP_{i}$ are the true positives and $FN{i}$ the false negatives.
- Score is the geometric mean of the two values  ***W*** = $\sqrt{R0R1}$


