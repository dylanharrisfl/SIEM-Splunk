# SIEM - Splunk Basics

Utilizing Splunk basics to ingest and query log data.

**Platform:** [TryHackMe](https://tryhackme.com/)

---

I started out by utilizing the Splunk VM provided free by the TryHackMe platform. They provide a VM I can use to access the Splunk interface at the provided IP.

This lab starts off by going over the 3 components of Splunk:

- **The Forwarder** is the agent-based utility that runs on all endpoint devices. It collects and forwards logs from the machine to the Splunk Indexer.
- **The Indexer** receives and processes data ingested by the forwarders. It formats data into key-value pairs and stores them to be queried later by the Search Head.
- **The Search Head** is where users can query the data within the indexer. It uses SPL (Search Processing Language) to search the data, which is then returned to the user in key-value pairs.

---

## Ingesting Data

The lab asks where we can ingest data from files and ports. By going to the Add Data tab in the dashboard, the "Monitor" tab is described as accomplishing this:

<img width="700" alt="Add Data Monitor tab" src="https://github.com/user-attachments/assets/b34a8594-9621-4817-9e7d-126aa6fa2b55" />

Next, I manually uploaded VPN log files as a log source to the Splunk interface. I went to Add Data and navigated to the upload option. There are five steps to follow:

**1. Select Source:** In this case, my VPNlogs.json file.

<img width="700" alt="Select source" src="https://github.com/user-attachments/assets/06454f78-f814-43a5-a554-e6da5e4f9a07" />

**2. Source Type:** Here I select the source type of the data, which auto-filled as JSON given the file type.

<img width="700" alt="Source type" src="https://github.com/user-attachments/assets/078c5a64-a0e8-4f28-b7b3-0f3d4c45fcdf" />

**3. Input Settings:** Here I can change which index these logs are dumped into, as well as a device name to associate with the logs.

<img width="700" alt="Input settings" src="https://github.com/user-attachments/assets/3848af4c-dda7-49d3-8c44-b4f8af4639d5" />

**4. Review:** Verify everything configured before proceeding.

<img width="700" alt="Review settings" src="https://github.com/user-attachments/assets/54e13f1c-e369-49a0-8f29-9c797282cddd" />

**5. Done:** From here I can start searching through logs, build dashboards, or add more data.

<img width="700" alt="Upload complete" src="https://github.com/user-attachments/assets/7abcdd54-a67b-476a-821a-51aca1cb01e7" />

---

## Lab Questions

**1. Upload the data and create an index "VPN_Logs". How many events are present in the log file?**

The lab asked me to create a new index, so the 5724 events I saw in the original "test_index" I had chosen weren't going to be the answer. I went back and created a new index in the Input Settings section of a new upload:

<img width="600" alt="Creating VPN_Logs index" src="https://github.com/user-attachments/assets/253b8ba0-063c-4de9-9c1c-e2b03a3d9745" />

<img width="500" alt="Event count result" src="https://github.com/user-attachments/assets/674f632e-ed1d-4203-9336-9aab8f9c4b48" />

> **Answer: 2862**

---

**2. How many log events are captured by the user Maleena?**

I took some time to poke around and explore the Splunk dashboard here. On the left I could see an "interesting fields" column with "UserName" as one of the options. After selecting it, it showed the top values used in these logs for the UserName field and Maleena had 60.

<img width="700" alt="UserName field values" src="https://github.com/user-attachments/assets/c40f4caa-7a14-401e-90be-95de46ba0504" />

One thing I noticed while exploring: there is an "a" or "#" next to each field indicating whether the value is a string or integer. A small touch that makes manual log investigation a little quicker and easier to understand at first glance!

> **Answer: 60**

---

**3. What is the username associated with IP 107.14.182.38?**

I first looked at the top 10 values associated with the Source_ip field but nothing was returned:

<img width="700" alt="Source IP top values empty" src="https://github.com/user-attachments/assets/8a846114-7f6d-40e3-bd5a-ebd5ca276422" />

Looking at the key-value pairs, I figured I just needed to query directly using the Source_ip field and the target IP. This wasn't my first try though. I learned that the syntax is case-sensitive, so `Source_IP` and `source_ip` weren't working. I had to match the exact spelling of `Source_ip` from the log. Once I did that, "Smith" came back as the answer in the first result.

<img width="500" alt="Smith result" src="https://github.com/user-attachments/assets/09e1641a-12a5-4316-b90c-2e5cd87df2b0" />

> **Answer: Smith**

---

**4. What is the number of events that originated from all countries except France?**

It would be silly to look at the 7 countries listed and write an operator listing only the 6 that aren't France. Instead I used the not equal operator (`!=`) to show any Source_Country not equal to France. Sure enough, this did the trick!

<img width="700" alt="Not equal France filter" src="https://github.com/user-attachments/assets/566b5454-a893-4513-8f33-eebf6a344588" />

<img width="700" alt="Result excluding France" src="https://github.com/user-attachments/assets/15dd8fa2-35de-4092-9dff-bea02d1a0a0e" />

> **Answer: 2814**

---

**5. How many VPN events were associated with the IP 107.3.206.58?**

This last question was pretty straightforward. I just needed to do the same thing as question 3 and query for any logs associated with the specified IP address.

<img width="700" alt="VPN events for IP" src="https://github.com/user-attachments/assets/7aeb10fe-e22f-49a8-ae08-49c43a0d5daf" />

> **Answer: 14**

---

## Wrap-Up

I know this was only scratching the surface of what Splunk can do. This taught me that Splunk is a very straightforward interface when it comes to log ingestion and analysis. It breaks down the logs for you so you can utilize its interface to search for what you need much quicker. I enjoyed getting familiar with it, as the concepts and techniques tend to be universal to many SIEMs. Splunk has definitely been my favorite interface to work with so far and I look forward to doing more labs to uncover what else it has to offer!

