--- 

title: Lab 8 Report
author:Brian Lu
partner:tyler Akau
date:4/23/2020

---

Lab 8: Architectural Wizard and IP Catalog

#Objective
	This lab brings up the topic of utilizing the onboard clock feature of the basys board to run modules instead of creating our own. The onboard clock feature is capable of creating a continuous signal that only needs to be initialized to use. Although the clock feature does allow us to choose the specifications of the clock there are limitations to what the basys board is capable of producing. To overcome this we physically code in a solution.

##8_1_1
This portion of the lab is focused on making a pulse generator, specifically a one second pulse on signal. A 100Mhz wave is sent to the clocking wizard which outputs a 5Mhz wave, which is the lower limit of the capabilities of this clocking wizard, at this setting. The 5Mhz wave is taken into account and for each 50,000 positive edges of the 5Mhz signal we output a signal that is an invert of itself. By doing this we are able to create a wave that is active with a period of one second. A reset and enable feature was implemented as well, so the pulse generator is active and takes count of positive edges only when enable is on, and when reset is hit the count becomes 0. Since we had no basys board we created a testbench instead. We created our own 5Mhz source that runs through our pulse generator. The code as well as the simulated waveform can be found below. 
```
module lab8_1_1_tb(
	);
	
reg clk_5Mhz;
reg reset;
reg enable;
wire count;
wire Q;
  
	pulse_generator DUT (.clk_5Mhz(clk_5Mhz), .reset(reset), .enable(enable), .Q(Q) );
	
    	initial
        	begin
            	
            	clk_5Mhz =0;
            	reset = 0;
            	enable = 1;
         		 #1000000000
                        		reset = 1;
                        		enable = 0;
         		#1000000000
                                       	reset = 0;
                                     	enable = 1;
         	
         	end
         	initial forever #500 clk_5Mhz = ~clk_5Mhz;
	
endmodule
```
```
module pulse_generator(input clk_5Mhz, input reset, input enable, output reg Q );
  
integer count = 0;
 
initial
Q = 0;
always @(posedge clk_5Mhz or posedge reset or posedge enable)
	begin
    	if (reset)
        	begin
            	count <= 0;
            	Q <= 0;
        	end
   	
    	if (enable)
        	begin
            	if (count < 5000000
                	begin
                    	count<= count + 1;
                	end
            	else
                	begin
                    	count <= 0;
                    	Q <= ~Q;
                	end
        	end
	end
 endmodule
```

![](lab8_1_1waveform.PNG)

###8_1_2
	The idea of the code for this part of the lab is to design a divider module capable of using a 5Mhz output clock from the wizard and generate two 500hz clock signals that go to a BCD converter that connect to two displays to show a 2 digit number. Importing the code from lab 2_2_1 and modifying it to be used as a BCD converter for two displays instead of one display and one LED. The 500hz signal is created in a similar way as the pulse generator from the previous portion, except the denominator of counts is a different value. 
```
module lab8_1_2(
    input clk, enable, reset,
    input [3:0] ain,
    output reg [6:0] segment,
    output reg [3:0] an1
  
    );
    
    wire clk_out1;
    wire [6:0] seg;
    wire Qo,z;
    wire [3:0] ex;
    integer k;
    
    clk_5Mhz CLOCK(clk_out1,clk);
    pulse_generator PULSE(clk_out1,enable,reset,Qo);
    BCD DISPLAY(ain[3:0],ex, seg[6:0],z);
    
    initial k=0;
    
    always @(posedge Qo)
        begin 
            if(k==0)
              begin
                an1 = 4'b1110;
                segment<=seg;
                k = 1;
               end
            else
               begin
                k = 0;
                an1 = 4'b1101;
                
               if(z==1)
                   segment=7'b0000001;
                else if(z==0)
                    segment=7'b1001111;                                          
              end
       end

endmodule
```

#Conclusion 
Unfortunately we were unable to get 8_1_2 to work. Our understanding of the instructions for that part might have been flawed which led to our current outcome. The lab was very detailed as to how to make a clocking wizard, which was new material so it made sense. For 8_1_2 we used the clocking wizard and had to modify old code, which felt a little overwhelming all in one part. Our largest setback in trying to understand how to get 8_1_2 working was the portion that required the BCD to output to two displays, as the pulse generator and clocking wizard just needed a bit of adjustments to the denominators from 8_1_1.
