# OpenROAD 7nm Contest

Some observations about the flow:
  - The timing calculations are very cautious until the CTS step. They lack the information needed to model the timing accurately and therefore there is no  escape hatch to retry early.
  - Timing repair has a tendancy to add too many buffers on failing paths. https://github.com/The-OpenROAD-Project/OpenROAD/issues/2302 Changing the penalty did not help.
  - The LVT and SLVT flow has broken adder technology mapping.
  
I started with the ibex desiign and progressively made improvemnts. All reports are under the respective log directoy.

The base log is the benchmark where nothing has been changed. It did not manage to achieve timing closure.
First I modified the synthesis script used by Yosys. The abc speed script was not performing as well as the default abc command that Yosys uses. This allowed the design to close with a ws of 22.95, area of 5823.06 and a power of 0.0206163.
Next I tried out a tighter clock at 1250ps. The design did not find timing closure with a ws of -213.26, area of 5823.06 and power of 0.0294494.
Next I ran the autotuner after fixing some problems related to metrics collection. This resulted in a design with ws of -206.666, area of 3915.64 and power of 0.0292652.
Finally I changed the target clock period to 1600ps to achieve closure. The ws improved to -105.725 and area remained roughly the same as before.
