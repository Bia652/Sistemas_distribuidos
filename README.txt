# 🌐 "Googol" Full-Stack Search Platform

**Technologies:** Java RMI, Spring Boot, REST APIs, HTML/CSS/JavaScript, OpenAI API, Ngrok, Jsoup

## 📖 Project Overview
[cite_start]Googol is a complete, distributed search engine platform built from the ground up, evolving from a distributed backend architecture to a fully functional Web application[cite: 144]. [cite_start]It features a parallel Web Crawling system, search result ranking by popularity, and a multi-tier architecture communicating via RMI[cite: 159, 160, 201]. 

[cite_start]In its final evolution, Googol integrates a Web server that allows users to index URLs and perform searches through a web browser[cite: 161, 162]. [cite_start]It also features REST integrations with Hacker News and the OpenAI API to provide intelligent search summaries and index popular external content[cite: 155, 156, 222].

---

## 🏗️ System Architecture
[cite_start]The software is built upon a distributed architecture using the MVC pattern for the Web Server and RPC/RMI for backend communication[cite: 141, 147]:

1. [cite_start]**Gateway:** Acts as the intermediary between clients (both the RMI Client and the Web Server) and the Barrels[cite: 161]. [cite_start]It manages a queue of URLs waiting to be processed and distributes client queries to active Barrels via RMI[cite: 170].
2. [cite_start]**Barrels (Index Storage):** The central servers storing the inverted index (`processed`) linking keywords to URLs, and the popularity index (`reachable`) linking a URL to other URLs that point to it[cite: 203]. These handle the search logic and return results to the Gateway. 
3. [cite_start]**Downloaders (Web Crawlers):** Work in parallel across multiple terminals to analyze web pages, extracting text and metadata (using libraries like Jsoup), and sending the processed information back to the Barrels via the Gateway[cite: 182, 183].
4. [cite_start]**Web Server:** Replaces the basic Desktop Client[cite: 146]. [cite_start]It provides a modern interface allowing users to access the same functionalities across devices, handling search queries, displaying results (grouped by 10), and pushing real-time statistics via WebSockets[cite: 145, 152, 200].

---

## 🚀 Key Features
* [cite_start]**URL Indexing:** Manually input a URL to be crawled and indexed[cite: 167, 168].
* [cite_start]**Recursive Web Crawling:** Automatically processes links found within visited pages using a URL queue[cite: 169, 170].
* [cite_start]**Search Engine:** Query terms and receive results containing the URL, title, and a short text citation[cite: 171, 199].
* [cite_start]**Popularity Ranking:** Search results are ranked based on the number of inbound links (importance)[cite: 201, 202].
* [cite_start]**Inbound Link Query:** View exactly which known pages link to a specific URL[cite: 204, 205].
* [cite_start]**REST API Integrations:** * **Hacker News:** Index the top Hacker News stories that contain the queried search terms[cite: 220, 221].
  * [cite_start]**OpenAI (AI Summaries):** Generates contextualized textual analysis based on search terms and result citations using the OpenAI Chat Completions API[cite: 222, 223].

---

## ⚙️ How to Run the Project

[cite_start]**Prerequisites:** * Ensure your operating system uses the correct end-of-line characters for shell scripts[cite: 121]. If you are on Windows, it is highly recommended to use `.cmd` files[cite: 122].
* [cite_start]Modify IP addresses and Port numbers in the configuration files if the default ones are occupied[cite: 122].

**Execution Steps:**
[cite_start]Open separate terminal windows for each of the following steps[cite: 123]:

1. **Build and Run Gateway:**
   [cite_start]Execute the `build.sh` script to compile the classes[cite: 123]. [cite_start]In the same terminal, run `run-gateway.sh` to initialize the Gateway server[cite: 123].
2. **Run Barrels:**
   [cite_start]Execute `run-barrel.sh` to initialize the index storage[cite: 124].
3. **Run Downloaders:**
   [cite_start]Execute `run-downloader.sh`[cite: 124]. [cite_start]The downloader will immediately start navigating web pages and processing data[cite: 124]. [cite_start]*(Note: Run multiple downloader terminals to increase crawling speed and index size [cite: 126]).*
4. **Run Client:**
   [cite_start]Execute `run-client.sh` to open the interface[cite: 125]. [cite_start]Here you can search, add new URLs, and query inbound links[cite: 125].

---
[cite_start]*Developed for the Distributed Systems course[cite: 127].*
