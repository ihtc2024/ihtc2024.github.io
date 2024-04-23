---
layout: default
title: Basic Concepts
parent: The Problem
usemathjax: true
nav_order: 1
---

<!-- TODO: Correct citations, streamline description of the problem -->

## Resources
We start by introducing the times and physical resources involved in the
problem:
* **Scheduling period:** The scheduling period is defined as a number $$D$$ of
  consecutive days; $$D$$ is always a multiple of seven, and it varies
  between 14 (two weeks) and 28 (four weeks).
* **Shifts:** We assume a fixed structure of working shift types for
  nurses, with three shifts per day, called _early_, _late_, and _night_.
  Therefore, there is a total of $$3D$$ shifts in the scheduling period.
* **Operating Theaters:**  All operating theaters are identical, and thus suitable for 
  accommodating all the different surgeries. Each theater has for each day
  in the scheduling period a maximum usage expressed in minutes. Some
  theaters might be unavailable on some specific days, and this is
  expressed by setting its maximum usage to 0 minutes.
* **Rooms:**  Rooms in the wards host the patients
  during their recovery. Rooms are characterized by their capacity,
  expressed in terms of number of beds.  The room equipment is not
  explicitly taken into account, although, as shown below, some rooms
  might be declared unsuitable for some specific patients.

Next, we describe the human resources that are involved in the
problem:

* **Nurses:** Each nurse has a skill level, which is an integer that
  goes from 0 (lowest) to $$L-1$$ (highest), where $$L$$ is the number of levels. Furthermore,
  each nurse has a predetermined roster, which is expressed as the set
  of shifts in which the nurse works. Each shift is an integer between
  0 and $$3D - 1$$. Finally, for each working shift, the nurse has a
  maximum workload that he/she can take in that shift.
* **Surgeons:**  Each surgeon has a maximum operating time for each
  day. The time is set to 0 when the surgeon is not working. It is assumed
  that if a surgeon is available his/her surgical team is also 
  available. In other words, the team is assumed as an atomic
  indivisible resource (called surgeon for simplicity). 

Note that the maximum workload of a nurse is shift-dependent, as they 
can be employed in auxiliary duties during some specific working
shifts, which might reduce their availability.  Also note that we consider the so-called _open scheduling policy_
[^fn], such that all surgeons can operate in all operating theaters.

## Patients
The central entity of the problem is the patient. For each patient, we
have the following relevant information:

* _mandatory/optional_: mandatory patients must be admitted during the scheduling period, while the admission of optional patients can be postponed until a future scheduling period;
* _release date_: earliest possible admission date for the patient;
* _due date_: latest possible admission date, provided only for mandatory patients;
* _age group (category)_: a patient belongs to an age group (e.g.,~infant, youth, adult, elder); the list of age groups is fully ordered;
* _gender_: each patient is either female or male;
* _length of stay_: duration of the hospitalization in days;
* _incompatible rooms_: set of rooms that cannot be allocated to the
  patient because they do not have the specific equipment or the
  necessary isolation;
* _surgeon_: each patient needs a surgery with an expected duration
  that will be performed by a surgeon who
  is pre-assigned to the patient; 
  we assume that the surgery is always performed on the
  admission day, so that surgery day and admission day coincide;
* _generated workload_: the workload profile generated by a patient is described by a vector and starts from the early shift of the admission day until the night shift of the discharge day; 
the length of the vector is 3 times his/her length of stay;
* _minimum skill level_: this is another vector of length 3 times the length of stay of the patient. It represents the minimum skill level of the nurse, required by the patient in a shift/day.

Note that both the generated workload and the minimum skill level of a
patient are variable and depend on the shift and the day of the stay, given that they are related to
the patient's treatments and their recovery
stage. Both values are usually lower during the night
shift and higher during the initial days of the stay.

[^fn]:Guerriero, F., Guido, R.: Operational research in the management of the operating theatre: a survey [link](https://link.springer.com/article/10.1007/s10729-010-9143-6)