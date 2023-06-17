## Create Compute Cluster and Compute Instance

Compute resource is among the most expensive resources. <br><br>
Let go to the Azure Machine Learning Studio and Create Compute Cluster for the designer <br><br>
Steps : <br>
`1.` Click on the compute icon left side <br>
`2.` Under Compute Clusters tab click on create <br>
`3.` Here you will create a virtual machine in our region of your workspace.<br>
`4.` Then select the virtual machine size .<br>
`5.` Select the one with two core and maximum ram as we are just learning <br>
`6.` Select Standard_D11_v2 having core :2, Ram 14GB, Storage 100GB, $0.18/hr <br>
`7.` Click next <br>
`8.` in Configure settings Write the compute name AML-CC-A001  <br>
`9.` Select minimum number of nodes as 1 and maximum as 1 <br>
`10.` Click create <br>


### Create Compute Instance
- click on compute instance tab
- click on create compute instance
- select virtual machine with the least possible cost Standard_D2_v3  2 8core 8GB 50GB
- click next
- now it will ask the compute name.
- write AML-CL-D001 as compute name.
- now just click `create` to start creating compute instance ..
