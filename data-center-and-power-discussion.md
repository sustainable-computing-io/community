# Data Centers

## Telemetry

<!--- TODO: add a diagram to illustrate data center composition --->

### Cooling, BMC
* OCP Cooling Telemetry[^ocp-cooling]
* BMC Telemetry[^bmc-exporter]
* (thermal???)
### Software Agent

<!--- TODO: add a diagram to explain the relationship between workload and power sources  --->

#### Methodology
Runtime system power consumption estimate[^wiki-power-estimate]
#### Projects
* Profiler[^gprofiler]
* Energy Consumption Metrology Agent[^scaphandre]
* PowerAPI [^powerapi]
* Kubernetes Efficient Power Level Exporter [^kepler]

#### Open Telemetry
* Open Telemetry[^opentelemetry]

## Compute Node

### Device and Power
<!--- TODO: add a diagram to illustrate computing devices and power draw --->

### Power Management
* Kubernetes Power Manager[^k8s-power-manager]

## Energy Efficient Computing

### Scheduling 
Options in Kubernetes:
* Power Driven Scheduling and Scaling with CPU telemetry in K8s[^platform-aware-scheduling] 
* Energy aware scheduling[^ieee-k8s-scheduler]
* Carbon-aware Kubernetes scheduler[^low-carbon-scheduler]

Batch scheduling according to power costs (carbon, money, et cetera)

### Scaling
* On-demand: Serverless
* VPA[^ocp-vpa]

### Tuning
Options: 
* Node tuning[^ocp-nto]
* CPU tuning: x86, arm
* GPU tuning

# Current Research/Initiaives

## Current Sustainability Initiatives
* Equinix[^equinix]
* Etsy and Cloud carbon footprint.org[^ccf]
* LF Energy[^lfenergy]  
* Energy Efficient High Performance Computing Working Group[^llnl]

## Current Papers:

* Emissions - Global Energy and CO2 Status Report 2019[^iea-emission] 
* EU Greenhouse Emission Intensity[^europa-ghg]

### HPC Specific models to learn from:

* Metrics for Evaluating Energy Saving Techniques for Resilient HPC Systems [^osti]: 

## Repos:

* Energy Efficiency of Languages[^energy-lanaguage]

# References
[^ocp-cooling]:https://www.opencompute.org/documents/ocp-wp-dcf-improve-data-center-cooling-facility-efficiency-through-platform-power-telemetryr1-0-final-update-pdf
[^bmc-exporter]: https://github.com/gebn/bmc_exporter
[^opentelemetry]: https://opentelemetry.io/
[^wiki-power-estimate]: https://en.wikipedia.org/wiki/Run-time_estimation_of_system_and_sub-system_level_power_consumption
[^gprofiler]: https://docs.gprofiler.io/
[^scaphandre]: https://github.com/hubblo-org/scaphandre
[^powerapi]: https://github.com/powerapi-ng/
[^kepler]: https://github.com/sustainable-computing-io/kepler
[^platform-aware-scheduling]: https://github.com/intel/platform-aware-scheduling/tree/master/telemetry-aware-scheduling/docs/power
[^energy-lanaguage]:https://github.com/greensoftwarelab/Energy-Languages
[^osti]:https://www.osti.gov/servlets/purl/1140455
[^europa-ghg]:https://www.eea.europa.eu/ims/greenhouse-gas-emission-intensity-of-1
[^iea-emission]:https://www.iea.org/reports/global-energy-co2-status-report-2019/emissions
[^llnl]:https://eehpcwg.llnl.gov/
[^lfenergy]:https://www.lfenergy.org/
[^ccf]:https://www.cloudcarbonfootprint.org/docs/methodology/
[^equinix]:https://www.equinix.com/newsroom/press-releases/2022/04/equinix-prices-1-2-billion-of-green-bonds-in-its-fourth-offering-to-advance-sustainability-initiatives
[^k8s-power-manager]:https://github.com/intel/kubernetes-power-manager
[^ocp-nto]: https://docs.openshift.com/container-platform/4.10/scalability_and_performance/using-node-tuning-operator.html
[^ocp-vpa]: https://github.com/openshift/predictive-vpa-recommenders
[^ieee-k8s-scheduler]:https://www.researchgate.net/publication/333062266_Improving_Data_Center_Efficiency_Through_Holistic_Scheduling_In_Kubernetes
[^low-carbon-scheduler]:http://ceur-ws.org/Vol-2382/ICT4S2019_paper_28.pdf
