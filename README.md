# Workshop on Digital VLSI SoC design and planning

**Digital VLSI SoC Design and Planning**

***It consists of Five day activities done by me.  
The workshop has taught me what OpenLane is and how to use it.***

The activities includes:
<div class="toc">
  <ul>
    <li><a href="#header-1">Day 1 - Introduction and Invoking the openlane</a></li>
  </ul>
</div>  

<div class="toc">
  <ul>
    <li><a href="#header-2">Day 2 - Good floorplan vs bad floorplan and introduction to library cells</a></li>
  </ul>
</div>  

<div class="toc">
  <ul>
    <li><a href="#header-3">DAY 3 - Adding new inverter cell to the library</a></li>
  </ul>
</div>  

<div class="toc">
  <ul>
    <li><a href="#header-4">Day 4 - Timing Analysis</a></li>
  </ul>
</div>  

<div class="toc">
  <ul>
    <li><a href="#header-5">Day 5 - Final step - Routing</a></li>
  </ul>
</div>  

<div class="toc">
  <ul>
    <li><a href="#header-6">Acknowledgements</a></li>
  </ul>
</div>  


## <h2 id="header-1">Day 1 - Introduction and Invoking the openlane</h2>

In today’s era, everyone has heard the word chip. Somewhere in the news or on social media.
The electronics world works on these small chips. To find a chip you need to find a PCB board, which can be found easily around you. For example, Tv, Computer, A.C., Smartphones, and the list goes on. Or simply you can refer to the following image which shows a PCB board Arduino  
![Img1](https://github.com/Shank012/nasscom-vsd/assets/163320647/ac9738ca-055d-4444-9a01-c82e4bad5136)  
The yellow circled mark is an Integrated circuit. The chip is inside that package.  

![Img2](https://github.com/Shank012/nasscom-vsd/assets/163320647/f12adf2d-b89f-4ae6-9df3-929b444ae8dc)  
The Size of the package is 7x7 mm. It consists of 48 pins. The package type is QFN (Quad Flat No-leads).  
There are different packages available such as BGA, SOIC, LGA, QFP, etc. But for our project, we are going to discuss the QFN package.  

![Img3](https://github.com/Shank012/nasscom-vsd/assets/163320647/f8f744a3-1d9e-4f02-8979-1c2086bbf56b)  
The chip is inside the package. It is connected with the outside world with the help of pads. The pads are the 48pins which are seen in the above figure.  

![img4](https://github.com/Shank012/nasscom-vsd/assets/163320647/fbf6d9ed-1565-4e84-befa-76a80e5f9cb5)  
A chip consists of a Die, core area, Pads, IPs, Macros, and std cells.  

So the question arises why do we need chips?  

Chips do all the computation work and make our lives easy.
Let's take an example of a stopwatch.  
![Img5](https://github.com/Shank012/nasscom-vsd/assets/163320647/9b0a26a8-d142-4f5d-b1bf-29882e4b9236)  
The Application or software is written in some language such as C, C++, or Java (human language/ coding language).
The OS (System Software) with the help of a compiler converts those coding statements into Instruction sets which are again converted to Machine language (Binary numbers 0’s or 1’s) with the help of an assembler. 
The Hardware(chip) will understand the program and will produce the output.

The figure shows the RTL to GDSII Flow,  
![Img6](https://github.com/Shank012/nasscom-vsd/assets/163320647/46c8b720-58e0-4c23-9969-18560311deac)

1.	**Synthesis:** Converts RTL to a circuit out of components from the standard cell library (SCL)
2.	**Floor Planning:** Partition the chip die between different system building blocks and place the I/O pads, defining pin locations, macro placements, and power planning by placing Power rings, power straps and power pads.
3.	**Placement:** Place the cells on the rows and align with the sites by using global and detailed method.
4.	**CTS(Clock Tree Synthesis):** Create a clock distribution network to deliver the clock to all sequential elements. It is done by using different types of Tree such as H, X, Fishbone etc.
5.	**Route:** Implement the interconnect using the available metal layers by using global routing(Which generates routing guides) and detailed routing(Uses the routing guide and implements the actual wires).
6.	**Sign Off:** In this step, we will do physical verification which includes DRC(Design Rule Check), LVS(Layout Vs Schematic), and timing verification which includes STA(Static Timing Analysis).

![Img7](https://github.com/Shank012/nasscom-vsd/assets/163320647/f74e1bd1-07a6-451d-a8a4-beae7654261b)  
By using docker and flow.tcl the openlane tool is invoked.  

![Img8](https://github.com/Shank012/nasscom-vsd/assets/163320647/9a7413a8-5fb3-44ae-a472-ef7e3b09d006)  
Once the openLane is opened we need to load all the package everytime. By using command package require openlane 0.9
After that we need to do design setup by providing all the input files. By using command prep -design picorv32a.  

![1](https://github.com/Shank012/nasscom-vsd/assets/163320647/e6242275-4b80-469e-88aa-dd4d0f0d58b7)  
Flop Ratio,

![Img9](https://github.com/Shank012/nasscom-vsd/assets/163320647/f5180780-40b7-408a-b122-3177ba5e23bf)  
These are the commands we used in Day1 to understand the tool and get the basic Idea.

You can get and understand all the openlane commands from this [link](https://armleo-openlane.readthedocs.io/en/merge-window-3/docs/source/openlane_commands.html)  

---------------------------------------------------------------------------------------------------------------------------
## <h2 id="header-2">Day 2 - Good floorplan vs bad floorplan and introduction to library cells</h2>
For floorplannning utilization factor needs to be checked. The formula for utilization factor and aspect ratio is given in below image.
![2](https://github.com/Shank012/nasscom-vsd/assets/163320647/02e3faab-2e76-41e9-9dd0-62ade089ab60) 
As seen the Netlist Area is 2x2= 4sq unit, and the total area of the core is 4x4 = 16sq unit. 
So the Utilization Factor becomes 4/16 = 0.25 which is not good. 1 means there is no space for routing and placing additional cells. 
The aspect ratio is 4/4 = 1  

After running Synthesis, we got the Chip area as  
![3](https://github.com/Shank012/nasscom-vsd/assets/163320647/7c25a8da-e5fa-41ce-a506-2ceddb90e8e0)  

All pre-configured files can be found at the following location:
![4](https://github.com/Shank012/nasscom-vsd/assets/163320647/c6c26da1-c369-4e6a-b2dd-e60ac959394a)  

Now we need to run_floorplan. The reports and results are generated in the location shown in the below image:
![5](https://github.com/Shank012/nasscom-vsd/assets/163320647/1da09b69-c02d-4c44-85ba-e7a380071508)  

The ioplacer log can be found at the following location:  
![6](https://github.com/Shank012/nasscom-vsd/assets/163320647/6e204c87-59a1-41ff-b8a3-eabdfc8a9d68)  

The details of the ioplacer.log are as follows:  
![7](https://github.com/Shank012/nasscom-vsd/assets/163320647/c65bc441-03cd-4aa2-99e5-7d1b5b914613)  

Invoke Magic tool by attaching tech file with the generated floorplan.def
![8](https://github.com/Shank012/nasscom-vsd/assets/163320647/394ddb46-b168-459e-b1ff-beaa3c05d56c)

Magic tool and the detail of a pin.  
![9](https://github.com/Shank012/nasscom-vsd/assets/163320647/cf6bf264-0810-4d71-b2a8-cb021b58a9f2)  

Standard cells before placement
![10](https://github.com/Shank012/nasscom-vsd/assets/163320647/3f78181b-925a-4b0c-b123-c29391c698d2)  

After using command global_placement, we can see the following image through Magic
![11](https://github.com/Shank012/nasscom-vsd/assets/163320647/b2bcb610-2621-43e6-af43-416460f2f5c7)

By zooming in we can see the cells as follows:
![12](https://github.com/Shank012/nasscom-vsd/assets/163320647/22d6db8f-5be0-4800-982e-dd845716bcc4)  

----------------------------------------------------------------------------------------------------------------------------
## <h2 id="header-3">DAY 3 - Adding new inverter cell to the library</h2>

Get the git files of the inverter from [VSDstdcelldesign git](https://github.com/nickson-jose/vsdstdcelldesign.git)  
We can get a detail understanding of the inverter from the repository of [Nickson Jose](https://github.com/nickson-jose/vsdstdcelldesign?tab=readme-ov-file#plugging-custom-lef-to-openlane-flow)  
Clone the Git from above links to the system.  
![13](https://github.com/Shank012/nasscom-vsd/assets/163320647/b5528322-9903-4d8d-a052-8a1a6443b60d)  

By using magic we can open the mag file
![14](https://github.com/Shank012/nasscom-vsd/assets/163320647/dfb371e6-17f4-47bb-9913-cfa80e2479bc)  

Now by zooming in and enabling grid (Press g on keyboard) we can see the grid dimensions (by using command- box). The value we get here is 0.01u which we will use in spice file.  
![15](https://github.com/Shank012/nasscom-vsd/assets/163320647/119df2c6-e930-434c-bd95-5e5d9769d591)  

There are no DRC’s in the mag file
![16](https://github.com/Shank012/nasscom-vsd/assets/163320647/85132d3b-87c7-4614-b7de-f88ff834954f)  

Now extract the spice file,  
![17](https://github.com/Shank012/nasscom-vsd/assets/163320647/09189641-0201-402d-97e9-661a5cbf2fd7)  

Now edit the spice file, change the scale to the size of grid of inverter. Include the lib files, provide pulse and do the transient analysis.  
![18](https://github.com/Shank012/nasscom-vsd/assets/163320647/548b9a7e-5cd7-47a9-93ed-5af5aa6cd21f)  

Run the ngspice solution and plot the graph using command -plot y vs time a  
![19](https://github.com/Shank012/nasscom-vsd/assets/163320647/23df7505-0d64-43e3-9b33-4b07ccaa5c24)  

The plot is shown below  
![20](https://github.com/Shank012/nasscom-vsd/assets/163320647/48fac51a-c9e6-4dd8-86c0-13a683b549b1)  

Now open tracks.info, to know the pitch and set the grid of inverter as per the track pitch
![21](https://github.com/Shank012/nasscom-vsd/assets/163320647/90c48b76-ee4f-454a-a43e-3c687a25b8c7)  
![22](https://github.com/Shank012/nasscom-vsd/assets/163320647/bdaedb63-2be7-4250-97d0-6e1ac7a2827b)  

Setting the grid of track size to check whether the input and output port of the inverter are on the grid or not. The figure also ensures the width is multiple of the pitch as well as the height.  
![23](https://github.com/Shank012/nasscom-vsd/assets/163320647/49fdc019-5a87-4acc-bc8b-12f9315a281e)  
From the above figure we can say that the stdcell layout is as per the requirement

Write lef to include the cell in our design file  
![24](https://github.com/Shank012/nasscom-vsd/assets/163320647/859037da-2340-4c7c-b8c6-c1568fd34b7a)  

Contents of the lef file  
![25](https://github.com/Shank012/nasscom-vsd/assets/163320647/09d9da4c-a4cd-4b75-add5-5469586ec379)  

Change the config file, add the libs and our new cell lef.  
![26](https://github.com/Shank012/nasscom-vsd/assets/163320647/1bc3cc92-8b21-46ac-9179-8c2aff5f83f5)

Add the following commands to include lef in the design after changing the config file.  
![27](https://github.com/Shank012/nasscom-vsd/assets/163320647/7a8ce905-859b-4291-950e-918bcff8846d)  
run_synthesis again  

As we can in the following image the new inverters are added to the design  
![28](https://github.com/Shank012/nasscom-vsd/assets/163320647/32fbfd57-4c74-4eac-868e-eda9a0bd0b07)  

---------------------------------------------------------------------------------------------------------------------------
## <h2 id="header-4">Day 4 - Timing Analysis</h2>  

Setting the commands to solve the negative slack  
![29](https://github.com/Shank012/nasscom-vsd/assets/163320647/68fb3e4c-16f8-4fea-a6bc-fafce53a0f20)  

As we can see from the results the negative slack is gone and the area of chip is increased.  
![30](https://github.com/Shank012/nasscom-vsd/assets/163320647/1549914c-f9cf-4f47-83ff-90b3da2074ff)  

After placement we can see our new inverter is placed in the design.
![31](https://github.com/Shank012/nasscom-vsd/assets/163320647/bc03b44f-db3b-4add-b4e8-8fa306222eb7)  

run_cts command if there are any violations, solve in openroad until the slack is met.
Openroad can be invoked in openlane by simply typing openroad. The inputs to openroad are as follows:  
![32](https://github.com/Shank012/nasscom-vsd/assets/163320647/ebb2d142-12d3-4eb7-b1b5-78e31c0c3a39)  

From the report, we can see that the timing slack is met  
![33](https://github.com/Shank012/nasscom-vsd/assets/163320647/96c10f59-69e9-419b-bf0d-c80f160031fb)

---------------------------------------------------------------------------------------------------------------------------

## <h2 id="header-5">Day 5 - Final step - Routing</h2>

To check the current def or what was the last def file that we generated. Use the command `echo $::env(CURRENT_DEF)`  
![To check the current def](https://github.com/Shank012/nasscom-vsd/assets/163320647/5d826036-2b68-4bdb-a587-22d101ec49b0)


Location for setting parameters for various stages.  
![Locations for script or set parameters](https://github.com/Shank012/nasscom-vsd/assets/163320647/72a5d85f-a4bc-483d-9b8c-f74fbd0a3926)  

The following image shows the parameters set for routing stage.  
![Routing parameters](https://github.com/Shank012/nasscom-vsd/assets/163320647/6af68b90-7ebe-4810-b726-5f0027949979)  

To run routing script, we just need to write the command `run_routing` in OpenLane tool. After the routing is done. we can get the report from the location as shown in the below image. 
![Routing report location](https://github.com/Shank012/nasscom-vsd/assets/163320647/d0142f35-69df-4567-95ec-17f8f8a6049f)  

If there are any errors in routing, we can check those error in the DRC report:  
![DRC error report](https://github.com/Shank012/nasscom-vsd/assets/163320647/c5a8ba31-f558-423f-ba0f-3cbc17206e15)  

Routing def file can be find at the location shown in the below image  
![Routin_def file location](https://github.com/Shank012/nasscom-vsd/assets/163320647/64996bd9-e1e6-472c-8552-c01a17743d29)  

Now by opening the routing.def file in Magic, we can see the final output as,  
![Routing](https://github.com/Shank012/nasscom-vsd/assets/163320647/840e9045-4344-44b0-9a99-5a056d19d337)  

A zoom in portion of the image, to see the routed tracks.  
![zoom routing](https://github.com/Shank012/nasscom-vsd/assets/163320647/170c73dd-2d13-4c79-a14a-e7d25373f93c)  
![routing_zoom)in](https://github.com/Shank012/nasscom-vsd/assets/163320647/79f06055-5a21-45c1-aeb6-d4507de2a4e1)  

The inverter that we added is also routed, perfectly without any DRC's.  
![Inverter](https://github.com/Shank012/nasscom-vsd/assets/163320647/3b75499f-68b2-416a-b7cd-91cc7e5dfb89)  



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## <h2 id="header-6">Acknowledgements</h2>

[Kunal Ghosh](https://github.com/kunalg123)  
[Nickson Jose](https://github.com/nickson-jose)  
[R Timothy Edwards](https://github.com/RTimothyEdwards)  


