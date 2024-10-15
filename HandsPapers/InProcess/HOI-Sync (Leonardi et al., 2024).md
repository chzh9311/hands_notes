---
tags:
  - Hand-Object
  - Egocentric
  - DomainAdapt
  - Dataset
Institute: University of Catania, Next Vision
Corresponding Author: Giovanni Maria Farinella
Code: https://fpv-iplab.github.io/HOI-Synth/
Year: "2024"
Publisher: ECCV
---
# Are Synthetic Data Useful for Egocentric Hand-Object Interaction Detection?
> [!note]
> Task: HOI detection. The main finding is to exploit synthetic data to enhance this task.
## Motivation
In domain adaptation, many questions remain:
> 1)Is there a gap between real and synthetic data? 2) Where does it originate? 3) How can it be reduced? 4) Can synthetic data entirely replace real data? 5) Can synthetic data enable training in the presence of unlabelled real data? 6) Can synthetic data increase efficiency when few real data are labelled? 7) What scale of synthetic data is needed? 8) Is in-domain synthetic data, aligned to the target real domain in terms of objects and environment, beneficial?

a. domain gap exists: around 30%-40% in performance.
b. un-/semi-/fully-supervised domain adaptation have different 

## The task
Originated from [[Understanding human hands in contact at internet level]], the task includes identifying the actively manipulated object, the presence of hands, and the contact state between hands & objects.
![[HOIDetectionExample.png]]

## HOI-Synth
The authors get this benchmark by 3 egocentric benchmarks ([[Epic-Kitchens]], [[EgoHOS]], [[ENIGMA-51]]) + synthetic data.