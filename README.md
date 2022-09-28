# STA - Static timing analysis
<img width="601" alt="image" src="https://user-images.githubusercontent.com/110079648/191461642-7ab4f453-5601-4170-91ce-bf6ad9e414bd.png">

## 1. Introduction: Static timing analysis Part 1 "checks"

### Definition
Static timing analysis (STA) is a method of validating the timing performance of a design by checking all possible paths for timing violations. STA breaks a design down into timing paths, calculates the signal propagation delay along each path, and checks for violations of timing constraints inside the design and at the input/output interface.

Another way to perform timing analysis is to use dynamic simulation, which determines the full behavior of the circuit for a given set of input stimulus vectors. Compared to dynamic simulation, static timing analysis is much faster because it is not necessary to simulate the logical operation of the circuit. STA is also more thorough because it checks all timing paths, not just the logical conditions that are sensitized by a set of test vectors. However, STA can only check the timing, not the functionality, of a circuit design.
### How does STA work?
When performing timing analysis, STA first breaks down the design into timing paths. Each timing path consists of the following elements:

**Startpoint** The start of a timing path where data is launched by a clock edge or where the data must be available at a specific time. Every startpoint must be either an input port or a register clock pin.

**Combinational logic network** Elements that have no memory or internal state. Combinational logic can contain AND, OR, XOR, and inverter elements, but cannot contain flip-flops, latches, registers, or RAM.

**Endpoint** The end of a timing path where data is captured by a clock edge or where the data must be available at a specific time. Every endpoint must be either a register data input pin or an output port.

<img width="1324" alt="image" src="https://user-images.githubusercontent.com/110079648/190870494-6458f966-d7f7-4687-bfe4-13d382415fca.png">

> Input port to D pin of Lauch Flop.

<img width="1303" alt="image" src="https://user-images.githubusercontent.com/110079648/190870534-fb7c2d8f-05de-4d95-8335-56c098e27050.png">

> Clock port of capture flop to Output port

<img width="1334" alt="image" src="https://user-images.githubusercontent.com/110079648/190870572-128aee34-04d2-4ed9-805a-9fe43a021a78.png">

> Clock port of lauch flop to D pin of Capture flop

<img width="1363" alt="image" src="https://user-images.githubusercontent.com/110079648/190870573-d5f596e9-2707-4f06-9770-2d285ea81e8a.png">

 > Input port to Output port

<img width="1354" alt="image" src="https://user-images.githubusercontent.com/110079648/190870581-85909633-e22e-416f-b66f-62aa6176a198.png">

These are valid paths to caluculate timing

<img width="1313" alt="image" src="https://user-images.githubusercontent.com/110079648/190870624-ed535397-b007-4b1f-aaf3-98f31b4cc7f9.png">

> The time required by a signal to travel form start point to the end point is called **Arrival time**
> Arival time is caluculated at end points.

<img width="1316" alt="image" src="https://user-images.githubusercontent.com/110079648/190870654-181008e3-daaa-4d5d-a919-8660e5dfdb5a.png">

> **Required time** is expected time of signal arival

<img width="1345" alt="image" src="https://user-images.githubusercontent.com/110079648/190870745-dfb3c9e6-aa6e-4586-9899-b2d11facd4cd.png">

<img width="1333" alt="image" src="https://user-images.githubusercontent.com/110079648/190870790-bda2d346-88c1-40a7-8005-f47a2c143cec.png">
 
 <img width="334" alt="image" src="https://user-images.githubusercontent.com/110079648/190870844-8848ddb9-265d-496d-9abf-346083ef1d3a.png">

let arival time is 3.5ns

<img width="916" alt="image" src="https://user-images.githubusercontent.com/110079648/190870871-991035b6-4f44-447a-9763-d1e3345a86fe.png">

<img width="940" alt="image" src="https://user-images.githubusercontent.com/110079648/190870874-b3e66795-7368-454f-a544-72263e6af989.png">

<img width="1236" alt="image" src="https://user-images.githubusercontent.com/110079648/190870923-8bbe198f-3258-4eaa-b335-5368125509f1.png">

<img width="1152" alt="image" src="https://user-images.githubusercontent.com/110079648/190870935-1b72aacd-1de2-4a1c-9494-6ffa137ea93a.png">

```
Max difference (max slack)= 0.8ns =>setup slack, setup timing, setup analysis
(Setup slack = Expected time max - Arrival time)
```
```
Min difference (min slack)=-0.1ns =>hold slack, hold timing, hold analysis
(Hold slack = Arrival time - Expected time min)
```
## 2. Types of setup/hold analysis
 
Types of setup/hold analysis
1. reg2reg
2. in2reg
3. reg2out
4. in2out
5. clock gating
6. recovery/removal 
7. data-to-data
8. latch (time borrow/time given)

Slew/Transition analysis
1. Data (max/min) CLK
2. Clock (max/min)

Load analysis
1. Fanout (max/min)
2. Capacitance (max/min)

Clock analysis
1. Skew
2. Pulse width
 
 <img width="1373" alt="image" src="https://user-images.githubusercontent.com/110079648/190871255-14fde47d-4f34-4711-acb8-ce99fb482cda.png">
 
 <img width="1370" alt="image" src="https://user-images.githubusercontent.com/110079648/190871264-87571f50-18c2-45e3-a426-16cd01c33f96.png">

<img width="1396" alt="image" src="https://user-images.githubusercontent.com/110079648/190871291-1656fea0-4e93-47de-b03c-999ea1366abc.png">

<img width="1366" alt="image" src="https://user-images.githubusercontent.com/110079648/190871323-5cb86380-4045-42b0-9dde-7684e5fffacc.png">
 
> Cat 2,3,4 belongs to IO timing 

<img width="1093" alt="image" src="https://user-images.githubusercontent.com/110079648/190871547-10796f35-6420-4260-9690-805979cd142c.png">


> Clock coming to capture flop is coming throgh an and gate. we are trying gate the clock. this thechnique is called **clock gateing**. This is used to reduce the chip power. if that portion of circuit is not using we can turn of clock which imples flop dosent switches.

<img width="1375" alt="image" src="https://user-images.githubusercontent.com/110079648/190871567-1b04c473-a104-43c7-8eb8-2f8a76d99cdf.png">

> For flops we have asynchronous pins also present.

<img width="1404" alt="image" src="https://user-images.githubusercontent.com/110079648/190871605-06124220-ba92-4d5c-b472-91b31f90d626.png">

> Now the combination logic that connected to reset pin is replaced by and gate, this is done to save some power in reset path. if control is high, the gate is open.

<img width="1410" alt="image" src="https://user-images.githubusercontent.com/110079648/190885750-aef6b504-5768-4c36-a4e2-3247a16e7541.png">

> And control signal should be in sync.to get them into synchronous level, so we take **a** and **ctrl** as final points to analise the ariving time.

<img width="1406" alt="image" src="https://user-images.githubusercontent.com/110079648/190885946-106fa3cf-8cb4-4513-bdb0-09b51516179a.png">


> **latch** is level triggered. if previos flop to latch dosent met timing constraints, it can barrow some time from level triggerd latch. similarly flop connected at output of latch failted to meet timing constraints, latch can give time to lext flop. thats why latches are very important in design.


<img width="1411" alt="image" src="https://user-images.githubusercontent.com/110079648/190886130-42e0eed9-80c5-45c4-9fc5-8f4e053b00cb.png">

### Slew/Transition analysis 
There is some minium and maximum requirement of slew. 
slew and the transition analysis ensures that each and every point on this particular set of it meets that criteria.

> Basically if you the slew is too sharp, it will increase short circuit power and if it is too large then it will increase opening time for gate.

Slew analysis has two parts i.e. data and clock

data dosent switch so often as compared to clock.
clock has to switch at equal intervels, that that's why the clock transition requirements becomes a bit stringent compared to the data requirements. 
 
<img width="1390" alt="image" src="https://user-images.githubusercontent.com/110079648/190886365-21d6c35a-42d4-4c76-98f2-65a7a349fe3b.png">

<img width="1412" alt="image" src="https://user-images.githubusercontent.com/110079648/190886377-25f47977-04ce-4b06-a442-7ea227959e06.png">

### Load analysis
fanout analysis- eg. if fanout is 3 whether it is able to charge that load or not.

<img width="1385" alt="image" src="https://user-images.githubusercontent.com/110079648/190886419-2f0b08cf-c733-4f76-b3f2-f5d2db874d43.png">

> Capacitance

<img width="1419" alt="image" src="https://user-images.githubusercontent.com/110079648/190886468-c6895bca-6c80-47b5-bad5-de1bf794a2ab.png">

### Clock analysis

<img width="1396" alt="image" src="https://user-images.githubusercontent.com/110079648/190886518-e4a04ac7-d785-4c4e-9c2c-6a868cd03e9c.png">

 <img width="1426" alt="image" src="https://user-images.githubusercontent.com/110079648/190886587-dfb2f241-d7b3-4845-ae7e-aad1f3716463.png">
 
 ## 3. Detailed analysis of Reg2Reg
 
 <img width="1335" alt="image" src="https://user-images.githubusercontent.com/110079648/190896130-0da83810-ead4-48a4-a185-d02b3d26d0b1.png">

<img width="803" alt="image" src="https://user-images.githubusercontent.com/110079648/190896165-696e7fd2-1dc4-429f-9ffb-3a119c949e55.png">

<img width="917" alt="image" src="https://user-images.githubusercontent.com/110079648/190896212-59720aab-5361-4c75-805c-53754a064f73.png">

<img width="941" alt="image" src="https://user-images.githubusercontent.com/110079648/190896244-9f845b4c-9387-43a1-8c35-0074dea7814e.png">

<img width="1340" alt="image" src="https://user-images.githubusercontent.com/110079648/190896294-4647b494-4d6a-4104-8fcd-751eaf6ca569.png">

<img width="1318" alt="image" src="https://user-images.githubusercontent.com/110079648/190896384-a8709c9f-118a-4107-bc08-2e03de6d4ddb.png">

<img width="1232" alt="image" src="https://user-images.githubusercontent.com/110079648/190896424-2659c9a5-8530-45ae-84b8-e8ec4953bc36.png">

<img width="1286" alt="image" src="https://user-images.githubusercontent.com/110079648/190896434-071de0de-1c64-4fcf-9aa6-25d67f76a045.png">

<img width="1103" alt="image" src="https://user-images.githubusercontent.com/110079648/190896514-6055ea43-7741-4ff6-8962-a0c0085f73dc.png">

<img width="1146" alt="image" src="https://user-images.githubusercontent.com/110079648/190896527-a1305ada-cd53-414d-b7eb-802071491e97.png">

<img width="1102" alt="image" src="https://user-images.githubusercontent.com/110079648/190896540-dec6a7c6-7ee9-491a-bc5d-d83ebcb7ffc5.png">

now among A1 and A2 which we have to consider?
that depends on type of analysis that we are doing. lower value considered if we are doing hold analysis, higher value while while doing setup analysis.
not lets go with setup time.

<img width="1123" alt="image" src="https://user-images.githubusercontent.com/110079648/190896654-bfcab204-4209-40e7-a5f5-348e8f508c63.png">

<img width="1116" alt="image" src="https://user-images.githubusercontent.com/110079648/190896675-a1d3c0c7-99ca-44df-b683-e7dc6785f563.png">

<img width="1300" alt="image" src="https://user-images.githubusercontent.com/110079648/190896695-d2474caf-5a99-468d-a326-5753143eb5a6.png">

<img width="1231" alt="image" src="https://user-images.githubusercontent.com/110079648/190896709-fa2c1f80-752c-47c3-94a8-5c924dbe87b2.png">

<img width="1144" alt="image" src="https://user-images.githubusercontent.com/110079648/190896819-3c656ba3-3257-4bdc-8c36-03d70241d9d7.png">

AAT-addition.
RAT subtraction.
RAT defined at destination and from that we go back every node by subtracting delays to find their respective RAT, so that we can find out what causing negative slack.
based on that we modify that node. that is called as Engineering Change Order(ECO).

<img width="1279" alt="image" src="https://user-images.githubusercontent.com/110079648/190897052-bbbb20b5-9534-443d-bc13-568388ab124e.png">

<img width="1159" alt="image" src="https://user-images.githubusercontent.com/110079648/190897058-a589486b-aac6-4e0b-bcc7-cdf309e836c7.png">

<img width="1159" alt="image" src="https://user-images.githubusercontent.com/110079648/190897102-e1acc652-7947-4686-b7a6-ecd82220cbb6.png">

<img width="1210" alt="image" src="https://user-images.githubusercontent.com/110079648/190897111-bd063bca-d780-44a3-80d2-bfcb28439f29.png">
 
 for setup analysis we take the lowest and for( hold we take the highest RAT)
 
 <img width="1190" alt="image" src="https://user-images.githubusercontent.com/110079648/190897220-2d9983fb-26f2-416a-a5af-41c2bee6684e.png">

<img width="1169" alt="image" src="https://user-images.githubusercontent.com/110079648/190897239-98a7cfde-6b74-4c56-91c9-0028e8dc5d2a.png">

<img width="1194" alt="image" src="https://user-images.githubusercontent.com/110079648/190897307-3e6330d6-cb30-4b47-b9f8-3866e3063002.png">

if delay of d(2) is 2-0.35 i.e d(1.65)(diif cell of same fun) the slack would be zero. that is Engineering change order ECO.

<img width="1168" alt="image" src="https://user-images.githubusercontent.com/110079648/190897438-8d6d4cdc-9ab0-4e98-b0f1-e627803b4a7a.png">
 
 at A0 also we can reduce delay by connecting a lunch flop for lower delay.

## 4. introduction to GBA-PBA analysis 
 GBA is Wrost case analysis (take all the wrost case paths)
 PBA take real path/ actual path that will be traced on sillicon.
 
 <img width="1168" alt="image" src="https://user-images.githubusercontent.com/110079648/190897581-c8332ccb-900f-459b-bce7-2c56c203c13e.png">
 
Path based analysis is more realistic than graph based analysis.
Lets go for PBA.

  <img width="1229" alt="image" src="https://user-images.githubusercontent.com/110079648/190897618-bab325d6-c694-4131-866d-85b814573a8e.png">

<img width="985" alt="image" src="https://user-images.githubusercontent.com/110079648/190897665-1062a822-6480-4e47-be95-a8b160838c7d.png">

<img width="1184" alt="image" src="https://user-images.githubusercontent.com/110079648/190897730-c212c830-88a1-4dcd-9b51-e1df2b54c6b7.png">
 
 <img width="1259" alt="image" src="https://user-images.githubusercontent.com/110079648/190901583-a283e427-c3a4-466a-8182-dd42579796c0.png">

<img width="1334" alt="image" src="https://user-images.githubusercontent.com/110079648/190901744-5c6a2216-993a-4d44-8745-8f5286450a56.png">


## 5. Transistor level Circuits 

<img width="1355" alt="image" src="https://user-images.githubusercontent.com/110079648/190901813-55b52ae8-dbec-47a8-85a2-0e92e8bb2403.png">

<img width="1367" alt="image" src="https://user-images.githubusercontent.com/110079648/190901904-b666bc0a-168d-4371-bc35-e58174d43942.png">

> Lanch flop gets clock after 2 buffer delays and capture flop gets clock after 3 buffer delays

<img width="1333" alt="image" src="https://user-images.githubusercontent.com/110079648/190902016-6e022eae-6be9-47c0-9ccc-74908dd01c15.png">

<img width="1357" alt="image" src="https://user-images.githubusercontent.com/110079648/190902060-d3b9a8d3-8ecf-475c-8327-bdf4f020a96b.png">

<img width="295" alt="image" src="https://user-images.githubusercontent.com/110079648/190902078-93ae7d15-1e6f-4bee-af89-fd96d36f1a80.png">
 
 <img width="1358" alt="image" src="https://user-images.githubusercontent.com/110079648/190902098-f1b42639-7153-426a-98c9-4ca09a09759c.png">

<img width="1408" alt="image" src="https://user-images.githubusercontent.com/110079648/190902545-44259542-5d08-4baf-877d-91cb5e003d00.png">

<img width="1376" alt="image" src="https://user-images.githubusercontent.com/110079648/190902622-ec3969ba-a6f3-4967-9851-42a91f2be2c2.png">

<img width="1390" alt="image" src="https://user-images.githubusercontent.com/110079648/190902667-59fc6464-7c20-4163-bb2d-8a1f77a07eb9.png">

<img width="1367" alt="image" src="https://user-images.githubusercontent.com/110079648/190902691-b4546f45-7429-4bab-927c-849f4b8c5341.png">

<img width="1435" alt="image" src="https://user-images.githubusercontent.com/110079648/190902769-6b60369a-7f0c-47e6-aac2-aa886271f66f.png"> 

<img width="1405" alt="image" src="https://user-images.githubusercontent.com/110079648/190902865-09d642a6-d702-4827-ba4c-e04880343b21.png">

<img width="1418" alt="image" src="https://user-images.githubusercontent.com/110079648/190903004-3203fe66-d932-4f2e-b8be-dcbb43075478.png">

**Setup Time** is the time before rising edge of CLK, that input D become valid i.e. 'D' input has to be stable such that Qm is sent out, to Q reliably

> Input 'D' takes at least 3 inverter delays (Inv1, Inv3 and Inv5/Inv2) + 1 transmission gate delay (Tr1) to become stable before rising edge of CLK

> Setup Time = 3 Inverter delay + 1 Transmission gate delay

<img width="1414" alt="image" src="https://user-images.githubusercontent.com/110079648/190904279-861a60bd-ba10-4ca3-8dda-9ea2b8eafb21.png">

> CIk-Q delay is the time needed to propagate 'Qm' to 'Q'.
> Note, that 'D' (or 'Qm' from low 'CLK') was stable till output of 'Inv5'. So the time required, to propagate is 1
> Clk-Q = transmission gate delay(tr4) + 1 inverter delay(inv6)

> Hold Time is the time for which 'D' input remain valid after clock edge. In this case, 'Tr1' is OFF after rising 'CLK'. So, 'D' is allowed to change OR can change, immediately after rise 'CLK' edge. So **Hold time is 'zero'**
 
<img width="1396" alt="image" src="https://user-images.githubusercontent.com/110079648/190904700-a5e170c1-ccb2-4efa-b819-e176457eebd6.png">

> Hence finite Time 'S' required (before clk edge) for 'D' to reach QM i.e. internal delay of Mux1 = Setup time

<img width="1018" alt="image" src="https://user-images.githubusercontent.com/110079648/190904758-17a290d2-dbf8-4434-87aa-68cf05d09d9e.png">

> Clock edge dosent come exactly. Practically, there is a window in which the edge arives.

<img width="1301" alt="image" src="https://user-images.githubusercontent.com/110079648/190904870-bb8826cc-ae95-4507-ad39-38746f382586.png">

> Reason for having Clock window is clock network in which we have lot of gates that results in variations in clock. Each and Every buffer on sillicon is diffarent.

<img width="755" alt="image" src="https://user-images.githubusercontent.com/110079648/190904951-65b995e9-031c-4e51-bab6-9ef27efd79e4.png">

## 6. Generating jitter values - Eye diagram
It is done in foundry

<img width="976" alt="image" src="https://user-images.githubusercontent.com/110079648/190905090-a0e8b991-b237-4d47-904a-3f5351400c1b.png">

<img width="1130" alt="image" src="https://user-images.githubusercontent.com/110079648/190905107-facf9c85-1990-4bc8-a40a-7a2550666065.png">

<img width="1141" alt="image" src="https://user-images.githubusercontent.com/110079648/190906435-7181d19a-c4ae-45bf-bfd4-3ba3dd1d6023.png">

<img width="1168" alt="image" src="https://user-images.githubusercontent.com/110079648/190906628-3f481919-57ea-403c-997e-239666f4f96a.png">

> ideal clock operates at 0 and 1. but practically, there might be voltage droop and ground bounce. this cause variations in clock levels

<img width="411" alt="image" src="https://user-images.githubusercontent.com/110079648/190907602-201eb859-8646-4f0b-b57d-f2eedfd283db.png">

<img width="1190" alt="image" src="https://user-images.githubusercontent.com/110079648/190907985-db73707e-2bf1-4ecb-85e8-fd265ffc09f3.png">

<img width="1403" alt="image" src="https://user-images.githubusercontent.com/110079648/190908415-c1248a18-ea9f-4392-8a25-5c3305a9cdbd.png">

<img width="1184" alt="image" src="https://user-images.githubusercontent.com/110079648/190908923-743e0de0-c8f5-46d3-8c6f-e7d6f8bc445a.png">

> There is a temporary variation in clock period due to jitter

<img width="1069" alt="image" src="https://user-images.githubusercontent.com/110079648/190909797-a0774a30-0316-40fa-ba34-efe1f0c0a837.png">

<img width="424" alt="image" src="https://user-images.githubusercontent.com/110079648/190910010-03130c8f-5f49-4319-bab3-2923516bc47a.png">

<img width="1330" alt="image" src="https://user-images.githubusercontent.com/110079648/190910531-85e5357e-cb98-4a5e-8308-f4b00d59e6eb.png">

> SU-Setup Uncertanity

<img width="1000" alt="image" src="https://user-images.githubusercontent.com/110079648/190910624-50561845-20f2-4ae6-9c89-3ee7471a6058.png">


## 7.SETUP TIME GRAPHICAL TO TEXTUAL CONVERSION

<img width="683" alt="image" src="https://user-images.githubusercontent.com/110079648/190914743-595b2611-c42f-4474-8db4-0d04245bf793.png">
 
 <img width="955" alt="image" src="https://user-images.githubusercontent.com/110079648/190914764-f8d98020-1069-4fbf-b0c9-07d485bacb0a.png">

<img width="1424" alt="image" src="https://user-images.githubusercontent.com/110079648/190914873-ad375209-a3cd-48a6-884d-d561d595c986.png">

<img width="1436" alt="image" src="https://user-images.githubusercontent.com/110079648/190915084-e8a1babb-d4e9-4973-8e9d-8ab3f7fc1787.png">

## 8. Hold Analysis Single Clock

<img width="1193" alt="image" src="https://user-images.githubusercontent.com/110079648/190915174-a3fd5a09-bef5-46b3-a597-72fc298883c4.png">

<img width="1188" alt="image" src="https://user-images.githubusercontent.com/110079648/190915373-d592f7d0-d67e-43e5-82a8-48a1db6349b3.png">

<img width="1107" alt="image" src="https://user-images.githubusercontent.com/110079648/190915385-ed326681-7b14-427c-8ac4-0535106950f8.png">

> Since there is only one edge jitter value of hold is less compared to setup(2 edges).

<img width="1268" alt="image" src="https://user-images.githubusercontent.com/110079648/190915485-9f09af98-b49d-4fa8-8b9f-f99a743abb2a.png">

<img width="1355" alt="image" src="https://user-images.githubusercontent.com/110079648/190915574-7f750e54-d92b-4261-81ed-e6a3f095b307.png">

## 9. Hold Analysis Single Clock Textual Representation

<img width="660" alt="image" src="https://user-images.githubusercontent.com/110079648/190915682-fc3a1961-2b85-48ed-9a12-433c7784d007.png">
 
<img width="1014" alt="image" src="https://user-images.githubusercontent.com/110079648/190915699-a1a5d600-e70d-4f9e-ac94-8365d434b460.png">

<img width="1435" alt="image" src="https://user-images.githubusercontent.com/110079648/190915943-32f878af-0c35-496e-91a9-64eafbca2cf0.png">
 
 ## 10. OCV : On-Chip Variation
 
> Sources of Variation : Etching Process Variation

<img width="1399" alt="image" src="https://user-images.githubusercontent.com/110079648/190916085-fa465971-9c44-41e9-a21e-c5d279b49f79.png">

Etching process defines the structures in layout (metal,diff..)(rectangle)

<img width="429" alt="image" src="https://user-images.githubusercontent.com/110079648/190916193-822e2238-02cb-43ce-9dbb-641596207817.png">

<img width="1425" alt="image" src="https://user-images.githubusercontent.com/110079648/190916223-aae6f7dc-6dbe-44c9-bd62-a219fcf47f09.png">

 <img width="1080" alt="image" src="https://user-images.githubusercontent.com/110079648/190916255-d0b879fd-1700-4c01-9f18-b009aae45cec.png">

Overlap area is diffarent. 

it is variation in one inverter. In chain of inverters lot more changes

<img width="1370" alt="image" src="https://user-images.githubusercontent.com/110079648/190916854-c0d8caa9-d319-46c1-a540-55cbd83f1522.png">

Gates in middle have some kind of variation as they connected to inverters only
inverters at ends may have another variation as they connected to flops.

<img width="978" alt="image" src="https://user-images.githubusercontent.com/110079648/190917265-592abda6-2bb4-477f-913e-30ec6342f131.png">

> Sources of Variation : Oxide Thickness

<img width="1438" alt="image" src="https://user-images.githubusercontent.com/110079648/190917352-0414f9be-f92f-44cb-a7d8-8d92e061e862.png">
 
<img width="1394" alt="image" src="https://user-images.githubusercontent.com/110079648/190917516-c9ce7788-23cc-4a7d-adf4-5188c924e411.png">

Middle invs have slighntly lower variations

<img width="1155" alt="image" src="https://user-images.githubusercontent.com/110079648/190918022-e1a4aec9-acf5-40b4-b836-d0f0ea4e452e.png">

<img width="1189" alt="image" src="https://user-images.githubusercontent.com/110079648/190918370-08474730-1199-4df1-8952-39e9f38f3223.png">

<img width="1210" alt="image" src="https://user-images.githubusercontent.com/110079648/190918626-aea546b3-8692-42c3-a510-cf2fa64236f3.png">

<img width="1231" alt="image" src="https://user-images.githubusercontent.com/110079648/190918648-7655d0f7-ae69-45af-8a71-a3e1c11904ae.png">

<img width="1127" alt="image" src="https://user-images.githubusercontent.com/110079648/190919006-6eac1b1d-3b63-4634-8666-f755792963fc.png">

<img width="1196" alt="image" src="https://user-images.githubusercontent.com/110079648/190919076-e9d628fe-7b0f-4810-bac8-ae55b5572bab.png">

R is not constant, but varies of Id

 <img width="855" alt="image" src="https://user-images.githubusercontent.com/110079648/190919141-9371db76-0556-427f-9907-7a3a06fbf00e.png">

<img width="960" alt="image" src="https://user-images.githubusercontent.com/110079648/190919169-2bf83a86-801a-411d-969d-b493f114cb65.png">

<img width="1381" alt="image" src="https://user-images.githubusercontent.com/110079648/190919283-1fd4662b-6a44-4e65-8b0c-3e69d4236d79.png">

> If these series of inverters are designed to have 100ps delay, it might end up having 101ps,102ps,99ps etc.

<img width="1186" alt="image" src="https://user-images.githubusercontent.com/110079648/190958157-a6b87d08-d3ad-4ebe-8007-131c858911ba.png">

## 11. OCV timing and pessimism removal

<img width="1438" alt="image" src="https://user-images.githubusercontent.com/110079648/190958372-83835e8b-7eb1-4f49-bca3-832524035ac9.png">

OCV on setup timing analysis
any of flowing combination
DRT +20% +20% -20% -20%
DAT +20% -20% +20% -20%

<img width="696" alt="image" src="https://user-images.githubusercontent.com/110079648/190958946-7a713e68-6468-44e3-bd62-8e16ccb38c5e.png">
 
 if are reducing by 20%(i.e.-20%) that is **CLock Pull-in**
 (we are reducing delay of every cell in clock path)
 
 <img width="1440" alt="image" src="https://user-images.githubusercontent.com/110079648/190959236-5539a799-4b1c-4976-ab1b-f5490f23378e.png">

if are increasing by 20%(i.e.+20%) that is **CLock Pull-out**
 (we are increasing delay of every cell in clock path)
 
  <img width="525" alt="image" src="https://user-images.githubusercontent.com/110079648/190959369-8ed9e5ae-9043-49a0-bb96-a572f3b6c506.png">
 
 this will give more realistic and conservative approch.
 Clock pull in for DRT and Clock pull out for DAT
 
 <img width="1355" alt="image" src="https://user-images.githubusercontent.com/110079648/190959646-6cc14b66-4b40-4f58-9821-945392520b53.png">

<img width="1365" alt="image" src="https://user-images.githubusercontent.com/110079648/190959681-763227e9-2c1c-4ebe-8924-8de361f0e9e7.png">

<img width="547" alt="image" src="https://user-images.githubusercontent.com/110079648/190959889-95c3a86e-a19c-43eb-afac-2d2b5fbc9ab8.png">

<img width="1376" alt="image" src="https://user-images.githubusercontent.com/110079648/190960046-6cb5d7c1-d594-43e2-b27e-851b93546f00.png">

in DRT lets delete old numbers and keep new numbers

<img width="1433" alt="image" src="https://user-images.githubusercontent.com/110079648/190960347-3702a67f-fb9a-4711-9536-569a3a29cc18.png">

The Launch clock section and capture clock section highlighted part is common

<img width="1075" alt="image" src="https://user-images.githubusercontent.com/110079648/190960625-131e7b9e-f3a5-4c13-bc8b-64d87b7d5e6c.png">

> A cell is showing 2 diffarent delays which is practically not possible.

> At a time instant (say 't'), the delay of cell 'b1' can be either 0.043ns or 0.0344ns

> So there is an additional pessimism of |0.043ns - 0.0344ns| = 0.0086ns
> We need to remove this Pessimism

<img width="1402" alt="image" src="https://user-images.githubusercontent.com/110079648/190961578-9fadcd27-8406-4ea8-9e1e-b513ed66627d.png">

we can Add Additional Pessimium to DRT or subtract from DAT.

<img width="1355" alt="image" src="https://user-images.githubusercontent.com/110079648/190961864-f4c94533-1a67-4b6e-bd2d-7597b69d6c84.png">
 
 Now lets do this on hold timing
 
 <img width="1426" alt="image" src="https://user-images.githubusercontent.com/110079648/190962345-12080df4-aca7-44a8-b688-55f324149213.png">

<img width="628" alt="image" src="https://user-images.githubusercontent.com/110079648/190962528-580291e3-9f09-4a41-a911-84cdcd9534b0.png">

<img width="755" alt="image" src="https://user-images.githubusercontent.com/110079648/190962556-10ac7b4c-1030-47b2-b7a4-8c6e6d1d90a4.png">

<img width="1437" alt="image" src="https://user-images.githubusercontent.com/110079648/190962810-85e474f8-26db-423b-80a4-4ba6c3074c00.png">

<img width="1223" alt="image" src="https://user-images.githubusercontent.com/110079648/190962956-66a50b28-00db-4e6e-a63e-01b5a3af5b26.png">

<img width="392" alt="image" src="https://user-images.githubusercontent.com/110079648/190963075-759a2871-0378-410c-b260-2cc1db1a12c8.png">

<img width="737" alt="image" src="https://user-images.githubusercontent.com/110079648/190963344-b71337cd-611e-41aa-9cc5-7b6ca8280981.png">

<img width="1423" alt="image" src="https://user-images.githubusercontent.com/110079648/190963646-76fcec50-3875-43fe-9650-cd3954a96421.png">

we can remove Additional pessimissum from DRT or add to DAT

<img width="1437" alt="image" src="https://user-images.githubusercontent.com/110079648/190963825-62da5639-d9a1-4e42-8a0a-1d9c4014fd85.png">

## 12. Conclusion of workshop part`1

<img width="1147" alt="image" src="https://user-images.githubusercontent.com/110079648/190964049-ef49f671-8479-4819-a40e-4e032564eddd.png">

these concepts will be same for these also

<img width="990" alt="image" src="https://user-images.githubusercontent.com/110079648/190964270-4e4536fc-de27-435a-b629-f0e4bbdc377f.png">

<img width="1071" alt="image" src="https://user-images.githubusercontent.com/110079648/190964369-24687bed-e1dd-44f0-b1a5-6c8e53affec8.png">

<img width="1021" alt="image" src="https://user-images.githubusercontent.com/110079648/190964437-87da9ec3-72e0-438f-98c9-70e2e9f0242f.png">

- We summarized rer2reg timing analysis. The concepts we learned for reg2reg analysis can be applied to any other setup/hold analysis.

- While doing Slew/Transition analysis we will be using library setup and hold time.

- Clock analysis is highly dependent on on-chip variation and pessimism removal.



# ################################
# STA PART 2
# ################################

<img width="1415" alt="image" src="https://user-images.githubusercontent.com/110079648/190999613-e97a911f-402b-4573-9116-9f6bc1e1b36f.png">

## 13. Installing open timer
make sure you have atleast
- GNU C++ Compiler v7.3 with -std=c++1z
- Clang C++ Compiler v6.0 with -std=c++17
to check
```
$ gcc --version
$ clang --version
```

install cmake with following command
```
$ sudo apt  install cmake
```
To install Opentimer
```
$ git clone https://github.com/OpenTimer/OpenTimer.git
$ cd OpenTimer
$ mkdir build
$ cd build
$ cmake ../
$ sudo make 
```
to test
```
$ make test
```
in opentimer directory, use the following command to invoke open timer.
```
$ ./bin/ot-shell
  ____              _______              
 / __ \___  ___ ___/_  __(_)_ _  ___ ____
/ /_/ / _ \/ -_) _ \/ / / /  ' \/ -_) __/
\____/ .__/\__/_//_/_/ /_/_/_/_/\__/_/       v2.1.0
    /_/                                     
MIT License: type "license" to see more details.
For help, type "help".
For bug reports, issues, and manual, please see:
<https://github.com/OpenTimer/OpenTimer>.
```
to know commands
```
ot> help
```

Exploring Example:

<img width="847" alt="image" src="https://user-images.githubusercontent.com/110079648/191029417-be1329fb-408a-45f4-bd47-1a15d69a9b40.png">

<img width="1373" alt="image" src="https://user-images.githubusercontent.com/110079648/191029842-0af6b182-4eb7-493e-a69b-9f3fb87c5786.png">

<img width="1335" alt="image" src="https://user-images.githubusercontent.com/110079648/191029894-3c5aca13-8abf-4e8d-9a6e-8278c766fd2e.png">

<img width="1281" alt="image" src="https://user-images.githubusercontent.com/110079648/191030018-7ecff4e6-bf3e-4f48-9566-93681350d7b7.png">


























## Contributors
> Nishit Chechani 

> Kunal Ghosh

## Acknowledgments
> Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.

## Contact Information
> Nishit Dinesh Chechani, Postgraduate Student, International Institute of Information Technology, Bangalore 
> > E-Mail: nishitchechani@gmail.com

> Kunal Ghosh, Director, VSD Corp. Pvt. Ltd
> > E-Mail: kunalghosh@gmail.com
