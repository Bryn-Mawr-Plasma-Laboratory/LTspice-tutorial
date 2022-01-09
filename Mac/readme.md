# LTspice Startup Guide
## Introduction
This tutorial is does not include all the capabilities of LTspice. In fact, the reason for this document is to reduce stress for anyone using LTspice on a Mac, there are differences between Windows and Mac versions.

## Installation
Download LTspice from the Linear Technology Webpage:
[LTspice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)

##Tutorial
Once the software is installed, open the program. In the file menue, open a new schematic.

Circuit elements are listed on the top right. You can hover the mouse over an icon to see what it is. Place a resistor, a capacitor and an inductor on the schematic. It is most useful to make sure to place the capacitor vertically on the left hand side of the circuit, the resistor vertical on the right hand side, and the inductor horizontally on the top. You can rotate any of the elements by first selecting the element, then selecting the rotate icon (to the right of the circuit element icons). If you make any mistakes, you can delete elements by hovering over them, and hitting delete. This will bring up the scissors cursor and if you
click on the element, it will be removed. Hit escape to get rid of the scissors.

Complete circuit by connecting the elements together using the wire icon to draw wires. 

Now, give the elements values. Each element has a label and a value. The label has a number attached to it, while the value just has a letter. Right-click on the value letter and input a value. You can specify a unit (mF, uF, nF, etc). If you just type in a number without a until, it will assume the MKS unit for that element (ohms, farads, henries, etc). To start, let’s make the capacitor 0.5mF, the resistor 1ohm, and the inductor 10uH. 

Next, we have to establish a ground reference. Place a ground element at the bottom of the circuit. Make sure it connects to one side of the capacitor (it doesn’t really matter which side). 

Finally, we have to establish some initial conditions. We do so using something called Spice Directives. The Spice directive icon is the very last icon on the right. Click it and make sure it is toggled to Spice directive. The directives are input in the text box. First, we need to set the voltage on the capacitor. We will set the voltage of the first node of the circuit to 100V. This assumes that the capacitor has been placed vertically and on the left hand side of the circuit.

Write:
`.ic V(n001) = 100V`

And hit ok. You now have to place that directive somewhere on the schematic. It doesn’t matter where. I typically put it at the bottom of the page.

We can now check to see that our circuit operates correctly.

Click run at the top left (the running person icon). This will bring up an edit simulation command box. Under the first tab labeled transients, input a stop time of 1ms. Press ok and an empty graph will appear. Next you have to indicate what you want to graph. Hover over the first node. This should be the wire between the capacitor and the resistor. A probe cursor will appear. When you click, it plots the voltage above. Does the curve make sense given what you know about RC circuits?

Next, we want to measure the current through the resistor. Hover over the resistor and a loop looking cursor will appear. Click and a trace of current will appear with units listed on the right side of the graph.
Does this curve make sense? It shouldn’t because this is supposed to be an LRC circuit, not an RC circuit. This means we need to add one more directive. We need to set the initial current of the inductor to zero. This is more reflective of reality. 

Click on the spice directive icon again.

Write:
`.ic I(L1) = 0`

Click ok and place the directive anywhere.

Delete the graph to clear the memory. Now hit run again and click on the voltage. It should be roughly the same as before. Now click on the current of the resistor. This time it grows from zero, peaks a particular time, then decays exponentially along with the voltage. Congratulations! You’ve just made and measured your first simulated LRC circuit.

Now its time to play around with this model. Here are some possible experiments to try, but feel free to make up some of your own. Take some data and make some plots for ranges of inductance, resistance or capacitance values. We want to start getting a sense of how each component affects the circuit. Remember, you need to delete the graph and re-plot the current or voltage every time you make a change to your circuit.

1) How does the rise time of the current trace vary with inductance? Record the time for peak current for a variety of inductance values. Try scaling by orders of magnitude.
2) What changes as you vary the resistance of the circuit?
3) Try building a simple pulse-forming network. Add a second capacitor in parallel to the first one and with enough space to add a second inductor between the two. Connect the circuit and give the new elements the same values as the originals. You will need to add initial conditions for the voltage of the second capacitor (note, adding a capacitor to the left means that the new capacitor is now node 1 and the second capacitor is now node 2) and for the current of the new inductor.
    a) What does the voltage at node 1 look like now? What about the current in the resistor?
    b) What happens if I make the inductance of L2 larger than that of L1?
    c) What happens to the current if I add another capacitor inductor pair? Two more?


