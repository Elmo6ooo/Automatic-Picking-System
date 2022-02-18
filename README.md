# Automatic-Picking-System
**※The code property belongs to the lab, so it is not allowed to open source.**

This project cooperates with mechanic students. They added a picking module controlled by PLC to the existing machine. I was in charge of putting data on the socket to succeed the handshake between IPC(industrial computer) and PLC, also control the machine according to different picking situations.

The system will involve three objects machine/picking module, IPC, PLC.
* **machine/picking module**: This machine is a commercial stamping machine provided by the manufacturer, which is mainly used in the shoemaking industry. The picking module is added that would hopefully reduce occupational accidents and labor costs.
* **IPC**: Control all actions of the machine.
* **PLC**: Responsible for controlling electric cylinders, pneumatic cylinders, vacuum suckers, and according to the position of the bed, applying different picking situations.

# Stamp & Pick process
When we select the object to be cut from the control interface, it will first transmit the layout file on the right to the PLC through the socket so that both PLC and IPC will have the same target. 
![image](https://user-images.githubusercontent.com/88305396/152675415-9798f6f8-178d-4214-9534-b274754d3bb5.png)
Then it will enter the stamp and pick process, which can divide into two parts.
* **IPC**: After the bed is moved to the stamping coordinate this current coordinate will be sent to the PLC.
When this row stamping is complete, the machine will be controlled by different signals sent by PLC.
* **PLC**: After receiving the current bed coordinate, PLC will apply different picking situations by measuring the distance of the next row of objects to be stamped and returning a signal to IPC.
![process](https://user-images.githubusercontent.com/88305396/152679925-cb1cad0a-728e-4cae-9e91-a6f0c269c31f.png)

# Four different picking situations
* **Pick**: When the punch moves to the start position of the row to be stamped, at the same time, the coordinates of the center point of the finished product enter the pick-up area.
![收料](https://user-images.githubusercontent.com/88305396/152682787-4c662308-d4bd-4a92-974d-a3fa53560d86.png)
* **Finish**: All objects are stamped and picked. 
![收料完成](https://user-images.githubusercontent.com/88305396/152685597-bce02460-e667-4658-ad1a-e32758b674ec.png)
* **No Pick**: When the progress has not pushed the finished products into the pick-up area, the status will remain No Pick, and the punch can continue to stamp.
![不收料](https://user-images.githubusercontent.com/88305396/152683212-22c12222-4e71-463e-b676-014c84a054d8.png)
* **Pause stamping & Pick**: Let's assume there is some damage in the middle of the material, so we only select a few rows to stamp. If we want to stamp the last row, finished products will get pushed out of the pick-up area, so we should Pause stamping & Pick.
![暫停裁切先收料](https://user-images.githubusercontent.com/88305396/152683313-109075db-012d-4936-8795-f7b9b46db644.png)

# Automatic picking system demo
From the right part of the video, we can see that we select four rows to stamp. When the stamping process starts, the first-row PLC returns No Pick, second-row PLC returns Pick, third-row PLC also returns Pick, fourth-row PLC returns Pause stamping & Pick, and then returns Finish.


https://user-images.githubusercontent.com/99638331/154633805-9cb4bb72-0a1b-48e6-9246-04629ef586f0.mp4

