# Fast Sense X 

## What is it?

Fast Sense X Robotics AI Platform is a powerful on-board computer bringing scalable Edge AI capabilities to mobile robotics. 

It consists of single board COM Express module with Intel CPU, set of edge AI accelerators to inference several neural nets on-board in real time and has numerous hardware interfaces to robotic sensors and actuators. AI accelerators are connected using M.2 PCIe interface and can be scaled depending on the task. 

It is shipped as ready to use device with software examples of running ROS algorithms with integrated neural nets meaningful for robotic applications running in isolated Docker containers. 

![](./assets/img/FastSenseX.png)

Possible configuration below consists of Intel CPU coupled with six edge AI inference devices including Intel Myriad X VPUs and Google Coral Edge TPUs.

![](./assets/img/FastSenseX_BlockDiagram.png)

## Specification

|                          | |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Edge AI devices** | Intel UHD Graphics (Gen11)*  <br /> 2x Intel Myriad X ([AI CORE XM 2280 m.2 module](https://www.aaeon.com/en/p/ai-edge-computing-board-ai-core-xm-2280)) <br /> 3x Google Edge TPU ([Coral M.2 Accelerator](https://coral.ai/products/m2-accelerator-bm/) +  <br />[Coral M.2 Accelerator with Dual Edge TPU](https://coral.ai/products/m2-accelerator-dual-edgetpu/)) |
| Edge AI perf          | 20 TOPS                                                                                  |
| CPU*                  | Intel® Atom™ x6425E 3.00 GHz (Burst)   <br />  1.8 GHz Clock Quad Core L2 cache 2MB      | 
| DRAM*                 | max. 16GB LPDDR4x                                                                        |
| I/O Interfaces*       | 2x USB 3.1, 6x USB 2.0, 6x UART, I2C, 1wire, Display port                                |
| Onboard storage*      | UFS 2.0 onboard flash up to 64 GB                                                        |
| Operating System      | Lubuntu 18.04.5 LTS                                                                      |
| Power Consumption     | less then 24W TDP (CPU/GPU - 12W, Edge AI - 11W)                                         |
| Size                  | 30 x 55 x 84 mm (1.18” x 2.17” x 3.31”) incl. heat-spreaders                             |
   

