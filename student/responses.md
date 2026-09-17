# Week 07 Controls Lab — Responses

Answers and recorded model results from `submission.json`. This document does not recompute or independently validate the results.

## Submission status

- Schema: week07.submission/v1

- Record ID: 7b08c022-7b08-43fb-8903-0c73afa66bfe

- Record revision: 10

- Model hash: fnv1a-80e10508

- Readiness: Marked ready by the submission.

## Supplied setup (instructor supplied)

### question — instructor supplied
Calculate required control moment, elevator moment, and the change with airspeed. Explain whether the nominal response meets +0.12 rad/s².

### system — instructor supplied
Illustrative planar pitch model. Aircraft geometry, integration, force conversion and constraints are supplied.

### representation — instructor supplied
Body axes forward/right/down. Positive pitch moment nose-up. Positive Fz downward. Positive elevator trailing edge down. Reference/CG X=0 m; tail X=-3 m.

### inputs — instructor supplied
Iy=5000 kg·m²; target=+0.12 rad/s²; competing=-750 N-m; density=1.225 kg/m³; V=40 m/s; S=16 m²; chord=1.5 m; Cmδ=-0.8/rad; elevator=-5°. Inputs are illustrative, not calibrated.

## Student responses

### physics
**Prompt:** Explain why a downward force aft of the CG gives a positive nose-up moment.

**Student response:**
```
Demo workflow test: the tail is aft of the CG (negative x). A downward force has positive Fz, so My = -x Fz is positive: nose-up.
```

### assumptions
**Prompt:** Explain one supplied assumption and what could invalidate it: planar motion, fixed reference, local linear effectiveness, no trim or damping.

**Student response:**
```
Demo workflow test: planar pitch and local linear elevator effectiveness with fixed density and geometry. Large deflections or changing flow can invalidate the linear slope.
```

### model
**Prompt:** Write your demand, dynamic-pressure, coefficient and moment equations. Identify which quantities are supplied and which are unknown.

**Student response:**
```
M_required = Iy * alpha_target - M_competing. q = 0.5*rho*V^2. deltaCm = Cm_delta_e*delta_e (radians). deltaMoment = q*S*c*deltaCm. Inputs are supplied; required moment and elevator moment are calculated.
```

### prediction
**Prompt:** Before running your own implementation, predict the sign of its elevator moment and the effect of halving airspeed. Explain the competing moment.

**Student response:**
```
At -5 degrees with a negative derivative, elevator moment is positive. Halving speed quarters q and elevator moment; the fixed -750 N*m competing moment means net moment can turn negative.
```

### verification
**Prompt:** Show one independent hand calculation with units. Compare it with your model, and explain a sign, unit, or limiting-case check.

**Student response:**
```
Hand check at 20 m/s: q=0.5*1.225*20^2=245 Pa; -5*pi/180=-0.0872665 rad; deltaCm=(-0.8)*(-0.0872665)=0.0698132; M=245*16*1.5*0.0698132=410.501 N*m. Net=410.501-750=-339.499 N*m; alpha=-339.499/5000=-0.0678998 rad/s^2. This agrees with the model. Zero elevator gives zero incremental elevator moment.
```

### claim
**Prompt:** What do your computed results support at the stated condition? Include a limitation.

**Student response:**
```
At 40 m/s, -5 degrees produces 1642 N*m, exceeding the 1350 N*m required, and alpha=0.1784 rad/s^2 exceeds 0.12. At 20 m/s the same command falls below the target and the net moment is nose-down. This conclusion assumes the local linear planar model.
```

### reflection
**Prompt:** What additional evidence or missing physics would you investigate next?

**Student response:**
```
Investigate nonlinear effectiveness, tail-force limits, actuator rate and uncertainty before extending the result.
```

### AI use
**Prompt:** Identify the AI tool and how you used it, what you changed, and how you independently checked the result. State “No AI used” if applicable.

**Student response:**
```
This is an instructor-authorized automated workflow test performed by Codex on joshua-course-demo. Codex entered equations and test responses and checked numerical outputs against an independent hand calculation. It is not a student submission.
```

## Equations and model source

The recorded model JSON/expression source follows exactly as supplied. It is not interpreted or recomputed here.

```
{
  "schemaVersion": "week07.student-model/v1",
  "id": "joshua-course-demo-week07",
  "version": "1.0.0",
  "slots": [
    {
      "id": "controls.demand",
      "expressions": [
        {
          "name": "requiredMoment",
          "expression": "pitchInertia * requestedAcceleration - competingMoment",
          "unit": "N*m"
        }
      ]
    },
    {
      "id": "controls.effectiveness",
      "expressions": [
        {
          "name": "dynamicPressure",
          "expression": "0.5 * density * airspeed * airspeed",
          "unit": "Pa"
        },
        {
          "name": "deltaCm",
          "expression": "elevatorDerivative * elevatorAngle",
          "unit": "1"
        },
        {
          "name": "deltaMoment",
          "expression": "dynamicPressure * referenceArea * referenceChord * deltaCm",
          "unit": "N*m"
        }
      ]
    }
  ]
}
```

## Recorded verification status

Recorded as passed for the submitted model hash.

- Checked at: 2026-09-17T00:35:35.947Z
- Detail: Student artifact passed demand, baseline elevator, quadratic speed, and neutral-deflection checks.

## Recorded model runs

### Run 1
- Recorded: 2026-09-17T00:25:56.830Z
- Run ID: a081e577-6022-4de1-9206-9799a5488b7c
- Record revision: 6
- Model hash recorded with run: fnv1a-80e10508
- Prediction recorded with run: ```
At -5 degrees with a negative derivative, elevator moment is positive. Halving speed quarters q and elevator moment; the fixed -750 N*m competing moment means net moment can turn negative.
```
- Result status: recorded values shown below
- Values: requiredMoment=1350 N*m; dynamicPressure=980 Pa; deltaCm=0.06981317007977318 1; deltaMoment=1642.0057602762652 N*m

### Run 2
- Recorded: 2026-09-17T00:26:13.636Z
- Run ID: b0b7ea88-825c-4a96-9845-be410eca2463
- Record revision: 6
- Model hash recorded with run: fnv1a-80e10508
- Prediction recorded with run: ```
At -5 degrees with a negative derivative, elevator moment is positive. Halving speed quarters q and elevator moment; the fixed -750 N*m competing moment means net moment can turn negative.
```
- Result status: recorded values shown below
- Values: requiredMoment=750 N*m; dynamicPressure=980 Pa; deltaCm=0.06981317007977318 1; deltaMoment=1642.0057602762652 N*m

### Run 3
- Recorded: 2026-09-17T00:26:35.059Z
- Run ID: e84aad5d-16f6-49ec-b997-a8224b0331e8
- Record revision: 6
- Model hash recorded with run: fnv1a-80e10508
- Prediction recorded with run: ```
At -5 degrees with a negative derivative, elevator moment is positive. Halving speed quarters q and elevator moment; the fixed -750 N*m competing moment means net moment can turn negative.
```
- Result status: recorded values shown below
- Values: requiredMoment=1350 N*m; dynamicPressure=245 Pa; deltaCm=0.06981317007977318 1; deltaMoment=410.5014400690663 N*m

### Run 4
- Recorded: 2026-09-17T00:26:45.935Z
- Run ID: f31ade6f-0bc8-497a-afb0-6e61657c6650
- Record revision: 6
- Model hash recorded with run: fnv1a-80e10508
- Prediction recorded with run: ```
At -5 degrees with a negative derivative, elevator moment is positive. Halving speed quarters q and elevator moment; the fixed -750 N*m competing moment means net moment can turn negative.
```
- Result status: recorded values shown below
- Values: requiredMoment=1350 N*m; dynamicPressure=980 Pa; deltaCm=0 1; deltaMoment=0 N*m

## Submission instructions

Use Save to GitHub in the app to save both files, commit, and push. Submit your fork URL and the saved commit SHA. Manual fallback: save this file beside `student/submission.json`, run `npm run student:prepare` and `npm run student:validate`, then commit and push student/.
