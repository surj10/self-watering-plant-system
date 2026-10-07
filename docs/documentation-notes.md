# Documentation notes

The README is grounded in the supplied final group report. The original technical extract is retained as historical documentation; these notes identify inconsistencies rather than silently rewriting that record.

## Threshold and hysteresis

Section 2.4.2 describes a 3% hysteresis margin and stopping at a moisture boundary. The Appendix C implementation instead stops watering after a timed pulse. In `applySetpointToController()`, `X = max(percentToVoltage(sp - 3), percentToVoltage(sp))`. With the documented increasing voltage-to-moisture mapping, this reduces to `percentToVoltage(sp)`, so the 3% constant does not implement the stated hysteresis. The README consequently describes a threshold, pulse and soak controller without claiming verified hysteresis.

## Moderate and severe dryness

Both `WATER_SMALL_MS` and `WATER_LARGE_MS` are 1000 ms in the final configuration. The severe-dryness threshold is 10 percentage points below the setpoint, but both branches run the same pulse length.

## Calibration

Table 3.1 and the calibration screenshot use different endpoint observations. The screenshot's displayed percentages are also inconsistent with the final 0.80–2.00 V mapping. The README states the final constants and treats percentages as relative indicators; it does not combine these records into a precision claim.

## Sampling and filtering

The prose assumes roughly 500 ms between samples when estimating filter response. `PRINT_PERIOD_MS = 500` controls serial reporting, and the listed main loop has no fixed 500 ms sampling delay. A 5-second filter time constant is therefore not established by the supplied code. The README gives the EMA formula without a time-response claim.

## Network behaviour

The report describes connectivity obstacles and a successful router configuration. These are project observations. It does not establish that an ESP32 is fundamentally incapable of enterprise Wi-Fi authentication. Reconnection calls in the firmware can block, so strict non-blocking behaviour and uninterrupted control during network faults require testing.

## Hardware protection

The report discusses a possible cause of the damaged board, while meeting notes state that 9 V was accidentally supplied to the ESP32. The exact electrical failure path was not demonstrated. No specific protection component is claimed here to fix an unverified failure path, and successful bench operation does not prove full electrical isolation.

## Repository scope

This package includes existing report figures and source listings, not invented firmware, new test results or missing original build files. Personal assessment forms, signatures and student IDs are omitted from the technical extract. Account-specific Blynk template configuration is replaced in the firmware extract; the original token and Wi-Fi password fields were already obscured in the supplied report.
