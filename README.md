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

The TryHackMe lab then asks a few questions:

1. Upload the data attached to this task and create an index "VPN_Logs". How many events are present in the log file?
The lab asks me to create a new index, meaning the 5724 events I saw in the original "test_index" I chose were not going to be the answer.
I could very easily go back and create a new index for this in the "Input Settings" section of a new upload:
<img width="983" height="526" alt="image" src="https://github.com/user-attachments/assets/253b8ba0-063c-4de9-9c1c-e2b03a3d9745" />
My answer here is 2862:
<img width="698" height="423" alt="image" src="https://github.com/user-attachments/assets/674f632e-ed1d-4203-9336-9aab8f9c4b48" />

2. How many log events are captured by the user Maleena?

This answer I took some time to poke around and explore the splunk dashboard here. On the left I could see an "interesting fields" column with "UserName" as one of the options. After selecting it, it showed the top values used in these logs for the UserName field. Meleena had 60.
<img width="1220" height="843" alt="image" src="https://github.com/user-attachments/assets/c40f4caa-7a14-401e-90be-95de46ba0504" />
Another cool thing I found was that in the fields column there is an "a" or "#" next to the field indicating if this field's value was a string or integer. This is just a small touch that really makes manual log investigation a little bit quicker and easier to understand at first glance!

3. What is the username associated with IP 107.14.182.38?
I looked at the top 10 values associated with the Source_ip field, but there were none returned:
<img width="1227" height="865" alt="image" src="https://github.com/user-attachments/assets/8a846114-7f6d-40e3-bd5a-ebd5ca276422" />

By looking at the current key-value pairs at the top, it looks like all I need to do is enter the key-value pair for Source_ip and the target IP address.
<img width="1227" height="865" alt="image" src="https://github.com/user-attachments/assets/6181fc1b-cf80-487c-a7f1-39abf9639555" />
This wasn't my first try. I learned that the syntax here is case-sensitive, so Source_IP nor source_ip was working. I had to make sure I followed the exact spelling of Source_ip from the log. This then returned "Smith" as my answer in the first log.
<img width="696" height="658" alt="image" src="https://github.com/user-attachments/assets/09e1641a-12a5-4316-b90c-2e5cd87df2b0" />

4. What is the number of events that originated from all countries except France?
Of course it would be silly to look at the 7 Countries that are listed, and write an operator listing only the 6 that are not France.
To combat this, I utilized the not equal operator (!=) to show me any Source_Country NOT EQUAL to France. Sure enough, this did the trick! My answer was 2814 logs.
<img width="1219" height="149" alt="image" src="https://github.com/user-attachments/assets/566b5454-a893-4513-8f33-eebf6a344588" />
<img width="1222" height="825" alt="image" src="https://github.com/user-attachments/assets/15dd8fa2-35de-4092-9dff-bea02d1a0a0e" />

5. How many VPN events were associated with the IP 107.3.206.58?
This last question was pretty straight forward, I just needed to do the same thing in question 3 to query for any logs associated with the specified IP address. This ended up being 14 logs.
<img width="1220" height="400" alt="image" src="https://github.com/user-attachments/assets/7aeb10fe-e22f-49a8-ae08-49c43a0d5daf" />

I know this was only scratching the surface of what Splunk can do. This taught me that Splunk is a very straight forward interface when it comes to log injestion and analysis. It breaks down the log for you so you can utilize its interface to search for what you need much quicker. 
I enjoyed getting familiar with the interface, as the concepts and techniques tend to be universal to many SIEMs. Splunk has definitely been my favorite interface to work with so far, and I look forward to doing more labs to uncover what else it has to offer!





 




