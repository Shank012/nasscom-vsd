# nasscom-vsd

Digital VLSI SoC Design and Planning

It consists of Five day activities done by me. And later the labs 

The activities includes as follow:

Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK.

## Day 2 - Good floorplan vs bad floorplan and introduction to library cells.  
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



## DAY 3 Adding new inverter cell to the library

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


Day 4 - Pre-layout timing analysis and importance of good clock tree.

Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA.
