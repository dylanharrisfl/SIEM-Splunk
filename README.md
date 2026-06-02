# SIEM-Splunk
Utilizing the Splunk basics to injest and query log data.

I started out with utilzing the Splunk VM provided free by the Try Hack Me platform. They provide a VM I can use to access the Splunk interface at the provided IP.

This lab starts off by going over the 3 components of Splunk:
The forwarder: This is the agent-based utility that runs on all endpoint devices. It can then collect and forward logs from the machine to the Splunk Indexer
The Indexer - The indexer receives and processes data injested by the forwarders. It fomrats data into key-value pairs and stores them to be queried later by the Search Head
The Search head is where users can query the data within the indexer. It uses SPL (Search Processing Language) to search the data, which is then returned to the user in a key-value pair

In the next step, the lab asks where we can injest data from files and ports.
By going to the Add Data tab in the dashboard, I can see the "Monitor" tab is described as accomplishing this:
<img width="1214" height="837" alt="image" src="https://github.com/user-attachments/assets/b34a8594-9621-4817-9e7d-126aa6fa2b55" />

Next, I am going to manually upload VPN log files as a log source to the Splunk interface.
I can go to Add Data and traverse to the upload option as seen in the above capture.

Here I need to follow five steps:

1. Select Source. In this case, it will be my VPNlogs.json file
<img width="1223" height="792" alt="image" src="https://github.com/user-attachments/assets/06454f78-f814-43a5-a554-e6da5e4f9a07" />
2. Source Type. Here, I select the source type of the data, which in this case auto-filled with json, given this is a .json file:
<img width="1222" height="785" alt="image" src="https://github.com/user-attachments/assets/078c5a64-a0e8-4f28-b7b3-0f3d4c45fcdf" />
3. Input settings. Here, I can change which index these logs are dumped into, as well as a device name to be associated with said logs:
<img width="1221" height="755" alt="image" src="https://github.com/user-attachments/assets/3848af4c-dda7-49d3-8c44-b4f8af4639d5" />
4. Review. In the fourth tab we will review what we have configured to verify before proceeding
<img width="1210" height="483" alt="image" src="https://github.com/user-attachments/assets/54e13f1c-e369-49a0-8f29-9c797282cddd" />
5. Done. Finally, we can begin searching through our logs (along with other various options like building dashboards or adding more data)
<img width="1233" height="635" alt="image" src="https://github.com/user-attachments/assets/7abcdd54-a67b-476a-821a-51aca1cb01e7" />







