# Ground Source Heat Pump Coil Optimization

[![Ground Source Heat Pump Coil Presentation](https://img.youtube.com/vi/ThvAVa0PFqQ/0.jpg)](https://www.youtube.com/watch?v=ThvAVa0PFqQ)

Ground source heat pump (GSHP) systems have gained a lot of attention for their ability to produce high energy performance while maintaining sustainability and offering extremely low operation costs. For a recent project, I optimized a simple GSHP system (a water coil and blower from a GSHP) that my Dad, an electrical engineer, and I are installing in our home. The objective was to minimize the cost per BTU of cooling, while meeting the required heating and cooling demand. The goal of the project was to determine whether or not the simple system would be more efficient than a state-of-the-art mini split with a high SEER rating.

The system can be idealized in the diagram seen below. Our system used data from a YORK MV16CN21C blower assembly, a Flotec FP2212-12, ½ HP 10 GPM pump, and a First Company water coil.

![System Diagram](https://github.com/froeca/Ground-Source-Heat-Pump-Optimization/blob/master/Images/systemDiagram.PNG)

Our optimization problem is put in standard form as seen below. In the equations below, <img src="https://render.githubusercontent.com/render/math?math=J"> is the cost function per BTU, <img src="https://render.githubusercontent.com/render/math?math=C_{fan}"> and <img src="https://render.githubusercontent.com/render/math?math=C_{pump}"> are cost functions in terms of (W), and <img src="https://render.githubusercontent.com/render/math?math=Q"> is the energy transferred to the air by the coil in units of BTU/hr. Our problem is constrained by the limitations of the fan and pump. A constraint on the BTU output of at least 18,000 BTU/hr will also be specified. This value represents ½ of the typical cooling demands for a normal American household. Thus, formalizing our optimization problem we have

min     <img src="https://render.githubusercontent.com/render/math?math=J(\vec{x}) = \frac{C_{fan}(\vec{x}) + C_{pump}(\vec{x})}{Q_{coil}(\vec{x})}">
w.r.t.  $`\vec{x} = \{CFM, GPM\}`$
s.t.    $`Q_{coil} \geq 18000`$
        $`688.5 \leq CFM \leq 1524`$
        $`0 < GPM \leq 5`$ 
        
The analysis was conducted using Excel and MATLAB on a mathematical model built with data collected from the actual coil and a model of the coil built via commerically used software to determine the thermal parameters of the coil. We had to make a couple of assumptions when constructing the model. These were:
  1. The coil parameters needed to create a model in software.
  2. The starting current of the pump.
A graph of the cost function is shown below.

![Cost Function](https://github.com/froeca/Ground-Source-Heat-Pump-Optimization/blob/master/Images/costFunction.PNG)

I used the general reduced gradient (GRG) algorithm to get a solution. If you need a refresher on how gradient descent works (or constrianed optimization), I'd recommend you check out Josh Starmer's YouTube channel [StatQuest](https://www.youtube.com/watch?v=sDv4f4s2SB8). He's got some good videos on some basic optimization principles. 

The optimization led to some interesting results (see [project paper](https://github.com/froeca/Ground-Source-Heat-Pump-Optimization/blob/master/Documentation/Froelich_MATH319_Project_Report.pdf) for full details). Overall, the mini-splits (we used a Fujitsu 9RLS3 in our analysis) seemed to be more economical with a cost of 0.051903 W / (Btu/hr). The cost of the GSHP was variable and depended on the startup cost of the pump. In order for the two system to be equal in efficiency, the startup power of the pump would need to be 78.42 W. 

While this solution is ideal for those interested in adding a ground source heat pump to replace an older less-efficient system, it is not as practical in our situation, since we already have several efficient minisplits installed. A more sensible solution would be to reroute the piping such that all water from the well goes through the coil. A simple microcontroller (Arduino Nano, Raspberry Pi, etc.) could then be used to start the fan whenever the well pump is turned on and/or when the water temperate is significantly
cooler than the air temperate. Arguably, the cost of the pump would then be negligible, as the cost was already incurred for other usage.

For more details and information, check out [my video](https://www.youtube.com/watch?v=ThvAVa0PFqQ) on YouTube (also linked above) and leaf through the rest of the documents and data that are provided. If you have any questions, let me know! I'm happy to help the best I can.
