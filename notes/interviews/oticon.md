
- don't use all of SV and UVM features
- some SV are *forbidden* 
- some UVM features are not used

- using UVM has the advantage when hiring though
- using a standard framework allows for easier hiring

- a lot of VIP comes in C which is opaque in the simulation and therefore hard to debug
- that's why they try to avoid C VIP
- sometimes they have models for chips like eeproms that are vendor provided which are in C or verilog

- they use standard interfaces like APB or SWD

- use synopsis tools

- prefer to have everything in one language (SV) to optimize compilation time and enable incremental compilation

- create module level testbenches where CRV is used to generate stimuli
- modules usually have matlab models as golden models
- CRV is not used for DSP streams, here typical streams are used
- time series constraints and patterns are impossible to capture using constraints

- use FSM coverage, not line or branch coverage
- use functional coverage

- the verification process can start when structure and interfaces are defined
- this allows for the creation of the testbench structure
- then the verification plan has to be created
- this starts in parallel with the design process
- usually testbench setup done earlier than design -> wait for design to be ready
- then finish verification process and coverage closure

- debugging is done using testbenches but mostly using assertions and formal methods
- distinguish assertions which can be formally proven
- those that can be only checked in simulation
- and those that can work with both

- one useful formal check is connectivity checks
- check whether a certain chip configuration connects the right signals

- use continuous integration
- regression tests are run on every commit
- 6 hours to run
- also includes synthesis
- coverage is checked

- no ISO standards for testing are followed
- the ISO standards for their products are at a higher level
- ISO standards are fulfilled by system design and translated to functionality
- that functionality is verified by the verification team

- the verification team has one code base which is continuously updated
- verification components are incrementally improved
- agile

- simulating just the boot phase takes 20 minutes

- 65 employees working on the chipset
- 8 in the verification team

- have looked into PyUVM
- but speed is an issue with any cosimulation framework
- have looked at systemC
- but as always, difficult to find people to hire with prerequisites
- its rare enough that software engineers become verification engineers

- would like a framework to generate skeleton of UVM testbench

- would like something for small quick unit tests 
- these get thrown away when the real testbench is created

- prefer formal methods over unit tests
- it is very fast and easy to add assertions
- the formal tool is quick at proving for a small design

- formal scoreboard used to assertions of datapath ??
- formal is good for control signals but not as easy for datapath signals


- bottlenecks are in the actual specification and verification plan creation
- also having to wait for design team
- not the development of the testbench
- only not anticipated testbenches can slow down the process and bugs which make it hard to verify remaining features

- use basically all the runtime UVM phases
- use pre- post- reset phases to setup chip into known state
- using these phases also makes it easier to use inheritance, since e.g. reset behavior is decoupled from test code

- DO NOT use uvm factory
- very hard to debug and you don't really know e.g. what sequence type you are actually working with
- callbacks are now supported by SV
- they weren't when UVM was created
- how does this fix the problem with uvm factory?

- have their own default scoreboard implementation since UVM does not provide one

- UVM was created by a group of companies each insisting on some of their own features
- so UVM is not perfect and one should choose the features that are useful

- the register abstraction in UVM is not a finished implementation
- not very clear what limitations are, e.g. you can't put a register in two different maps which use different access ports
- they developed their own solution
- would require common development of standard to avoid vendor lock


- examples on the net may be outdated and don't represent current best practices
- they only show small examples and things that sometimes don't work for larger designs
- e.g. clocking blocks are bad inside the design
- you should control the sampling yourself
- it can else be hard to debug who triggered a signal transition


- don't use any hierarchical references, only virtual interfaces

- mixed signal is hard in verification

- power aware verification is hard
- UPF format is used to capture power domains
- in simulation, powered down blocks generate `X` values -> need to be aware

- would like to have a skeleton/template generator for UVM testbenches to reduce the setup time
- have their own internal jinja2 based python template generator