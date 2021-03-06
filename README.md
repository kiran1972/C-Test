# C-Test
Digital Circuit Simulation
1.	Digital Circuit Simulation
A combinational circuit is made up of gates, which are devices that take Boolean (True / 1 and False / 0) input signals, and output a signal that is a function of the input signals. Gates take some time to compute their functions, so a gate’s output at time τ reflects the gate’s inputs at time τ − δ, where δ is the gate’s delay. For the purposes of this simulator, a gate’s output transitions between
0 and 1 instantly. Gates’ output terminals are connected to other gates’ inputs terminals by wires
that propagate the signal instantly without altering it.

For example, a 2-input XOR gate with inputs A and B (Figure 3) with a 2 nanosecond (ns) delay works as follows:


Time (ns)	Input A	Input B	Output O	Explanation
0	0	0		Reflects inputs at time -2
Reflects inputs at time -1
0 XOR 0, given at time 0
0 XOR 1, given at time 1
1 XOR 0, given at time 2
1 XOR 1, given at time 3
1	0	1		
2	1	0	0	
3	1	1	1	
4			1	
5			0	



A
O

B

Figure 3: 2-input XOR gate; A and B supply the inputs, and O receives the output.

The circuit simulator takes an input file that describes a circuit layout, including gates’ delays, probes (indicating the gates that we want to monitor the output), and external inputs.  It then simulates the transitions at the output terminals of all the gates as time progresses. It also outputs transitions at the probed gates in the order of the timing of those transitions.

The input file supports following keywords:
table – truth table. 
Format: table <name> <output values printed on single line> 
Truth table supports only 1 or 2 input gates. 
For 1 input gate the output values are listed for following inputs (0), (1)
For 2 input gate the output values are listed for following inputs (0,0), (0,1),(1,0),(1,1) 

type – gate type
Format: type <name> <truth table> <delay>
Describes a gate type with certain name, using certain truth table, that changes output after <delay>

gate – concrete gate instance
Format: gate <name> <type> [input gate1] [input gate2]
Describes a gate instance with <name> that uses <type> gate type and has up to 2 optional inputs

flip – set the gate input
Format: flip <gate> <value> <time offset>
Sets the <gate> input to <value> at <time offset>

probe – monitor the gate output
Format: probe <gate> 
Instructs the simulator to monitor gate output and collect all output value changes. 
Those should be printed to simulator console. 

done – end of the simulation section
layout – start of layout section. Contains svg description for visualizer. 
It only used to validate that json generated by the simulator provides correct visualisation. 
See tests/README for more details.

There are following issues with the program:
-	JSON output ( simulator.exe <simfile> json ) works, but simulator does not output gate transitions configured in simulator file (probe keyword) to the console – running simulator.exe <simfile> produces no output when it should.
-	The simulation itself can be made much faster, e.g. 5devadas13.in takes a very long time to run. (Just check in debug build). Please optimize the runtime of the application.
-	The JSON output is quite slow. We are not interested in pretty formatting or tree structure, just the output must be well-formed. Could you please rewrite/optimize it?
-	There are other issues in the code (such as wrong types, missing initializers, wrong method declarations and names etc). Please submit code improvement changes/suggestions.
Please correct those issues and submit the code either to Github or zip-file with the local Github repo.

Please make a separate commit for each of the issues.
