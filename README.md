# CellFree-MassiveMIMO-PHY-Prototype
# GOAL ----> PHY-layer prototype for Cell-Free Massive MIMO and Grant-Free Access using GNU Radio, featuring packet synchronisation, pilot-based CSI estimation, multi-AP reception, and CSI-driven AP selection.

_**RECEIVER ARCHITECTURES**_

**ARCHITECTURE 1** - Uses BIT ERROR RATE (BER) and RECEIVED SIGNAL STRENGTH INDICATOR (RSSI) to choose the best ACCESS POINT.
<img width="1920" height="1080" alt="ACESS POINT -1" src="https://github.com/user-attachments/assets/c3cc0e25-2ead-4730-bb02-1fa6771d0d35" />
**PROBLEM:** The XOR Path of the APs is used to calculate the Bit Error Rate (BER) of the input signal. Issue: BER requires the input signal to be known. I connected the input signal to one of the XOR ports. But in real life, Access Points don't know what the input signal is. 
So, this architecture is wrong.

**ARCHITECTURE 2** - Instead of BER, I used CYCLIC REDUNDANCY CHECK (CRC) and RECEIVED SIGNAL STRENGTH INDICATOR (RSSI) to choose the best ACCESS POINT.
<img width="1920" height="1080" alt="ACESS POINT -1 (1)" src="https://github.com/user-attachments/assets/744f156d-505c-4958-b937-97f1bba5e5af" />
**PROBLEM:** This architecture is IP/NETWORK Layer valid. PHY Layer isn't tackled properly. RSSI didn't tell me about the information quality, packet errors, or channel quality. The CPU didn't consistently choose the right AP because of the lack of these vital parameters.

**ARCHITECTURE 3** - The Use of Only CRC and a PACKET BUILDER;
- | PREAMBLE | PILOT | UE_ID | PAYLOAD | CRC |
- | 16 bits  | 8 bits| 3 bits| 32 bits | 8 bits |
<img width="1920" height="1080" alt="ACESS POINT -1 (2)" src="https://github.com/user-attachments/assets/8c36bfbe-7288-469f-83e0-3757a9e5c099" />
_CHARACTERISTICS:_ This architecture solves the PHY Layer. Like many Research Papers, I assumed a fixed frequency for the APs and the User. The PHY Layer performs;
- Preamble Detection
- Packet Synchronisation
- Pilot Extraction
- CSI Estimation
- Demodulation
- UE ID Extraction
- CRC Verification

**What makes this "Cell-Free ready"?**
Because each AP now independently produces:
CRC, UE_ID, CSI.
**The CPU can make decisions based on:**
Which AP decoded?
Which AP has the strongest CSI?
Which APs decoded the same UE?






