---
title: lib-viz-mermaid-examples-prompts
tags: [ai, diagramming, examples, flowchart, large-language-model, mermaid, prompt]
created: 2025-11-20T08:33:28.192Z
modified: 2025-11-20T08:34:08.347Z
---

# lib-viz-mermaid-examples-prompts

# guide

# prompts
- collections
  - [Mermaid Chart - A smarter way of creating diagrams. Step by Step Guide _202507](https://docs.mermaidchart.com/blog/posts/how-to-create-perfect-flowcharts-using-ai-in-2025-step-by-step-guide)
  - [The ChatGPT prompt list for Software Engineers: Prompts to generate software diagrams in Mermaid _202405](https://medium.com/@martin-jurran/chatgpt-prompt-list-for-software-engineers-prompts-to-generate-software-diagrams-in-mermaid-deaf2f373104)
  - [Create Mermaid Diagram - AI Prompt](https://docsbot.ai/prompts/technical/create-mermaid-diagram)
  - [Sample LLM prompt for Mermaid sequence: Client, Server, Database](https://gist.github.com/heitorlessa/8a652bad6a432a3d17fc7797107e3ac3)
  - https://github.com/fladdict/llmermaid
    - LLMermaid is a framework that enhances the capabilities of Large Language Models (LLMs) by integrating markdown-style diagram charts.
# prompts-examples
- official mermaid ai editor 

```
Write the Mermaid code for a sequence diagram describing a process. 

Flowchart diagrams in Mermaid start with "sequenceDiagram". Stricly follow this format:

sequenceDiagram
  Alice --> John: Hello John, how are you?
  John  --> Alice: Great!
  Alice --> John: See you later!

Only use the provided information. 
- write mermaid code for this workflow: user login with email or username
```

```prompt
Create a state diagram showing the states of a document in an approval workflow: Draft → Submitted → Reviewed → Approved/Rejected.

Create a sequence diagram for a customer placing an online order, detailing interactions between the Customer, Website, Payment Gateway, and Warehouse.

Create a mindmap to plan a product launch, with main branches like Marketing, Development, Timeline, and Budget, each with several sub-tasks or considerations.

Generate a class diagram for a library system with classes for Book, Member, and Librarian, including relationships and main attributes and methods for each class.

```

```
There are three participants: Client, Server, Database: 
Client makes a GET /products request to the Server
Server verifies whether Client is authorized to make this request
Server confirms Client is authorized and makes a request to the Database to fetch all products
Database returns 100 products to the Server, along with a pagination token to retrieve 100 more tiems
Create a loop between Server and Database, where Server fetches 100 more products with the pagination token provided by Database until there are no more products to be fetched
Server returns response to the Client

```

- 🌰 [DiagramGPT – AI diagram generator created by Eraser](https://www.eraser.io/diagramgpt)
  - 从下面的示例中精选了部分

## [AI Architecture Diagram Generator](https://www.eraser.io/ai/architecture-diagram-generator)

- chatbot architecture

```
Cloud architecture for a service that can take PDF files and allow users to have AI chat sessions regarding the content of the PDF files.
- Vectorize the PDF files using OpenAI's Embedding API
- Store them on a cloud vector database
- store the text chunks in a separate storage.
During a chat session, when a user asks a question
- turn the question in to a vector using OpenAI's embedding API
- query the vector database
- Use query result vectors to retrieve the associated text chunks.
- Query OpenAI's chat API with the retrieved text chunks and the original user question
- Return results from OpenAI's chat API to the user. Use AWS and OpenAI infrastructure where applicable.
```

- product page with microservices

```
A microservices architecture where a product page hits an api gateway, which hits microservices. The relevant microservices are:
- item API
- reviews API
- recommendations API
- auth API
- search API
Each has its own database, some have AI.
Reviews, recommendations, and search use the item API
recommendations uses the search API.
```

- gig marketplace architecture

```
Cloud architecture for a marketplace for freelance developers to find work. Allow authentication via GitHub and LinkedIn. Use machine learning to recommend listings. Use React for the frontend, Vercel for deployment. Use a graph database to store user activities, use a SQL database for job listings. Allow payments to be directly made on the platform via Stripe. Use AWS infrastructure where applicable.
```

## [AI Flowchart Generator](https://www.eraser.io/ai/flowchart-generator)

- expense submission and approval process

```
An expense submission and approval process (BPMN):
- The user logs in and is confirmed to have expense submission access.
- The user starts a new expense report.
- The user uploads receipts. The system extracts the date and amount using OCR.
- The system checks the amount:
    - If under $50, the expense is auto-approved.
    - If between $51–$500, it goes to the user's manager for approval.
- The approver reviews and either approves or rejects.
- If approved, the reimbursement is processed automatically.
- The flow ends with the user being reimbursed.
```

- Product-returns process

```
Product-returns process:
01. Customer requests a return.
02. Check if the item is still within the return window and in acceptable condition.
    - If not, tell the customer why it can’t be returned and close the case.
03. Send the customer a prepaid label or drop-off instructions.
04. Customer ships or drops off the item.
05. Warehouse receives and inspects the item.
    - If damage or missing pieces are found, offer a partial refund or send it back.
06. Approve eligible returns and update stock records.
07. Issue the refund, store credit, or replacement.
08. Notify the customer that the return is complete.
```

- customer support call flow

```
A support desk call flow:
- Standard Call Flow (General Support)
  - Used during normal operations
  - All calls go to a general support queue
  - Covers issues like software access, password resets, and technical help
  - Calls are answered in order by the next available technician
- High-Volume Call Flow (Peak Periods)
  - Activated during busy times (e.g., onboarding, system updates)
  - Callers hear a menu with options:
    - Press 1 for password resets
    - Press 2 for software access
    - Press 3 for other issues
  - Calls are routed to specific queues or voicemail based on availability
- Voicemail Handling
  - If no agent is available, caller is prompted to leave contact info
  - A support ticket is automatically created from the voicemail
  - Technicians follow up based on ticket priority and queue order
```

## [AI Data Flow Diagram Generator](https://www.eraser.io/ai/data-flow-diagram-generator)

- ecommerce website data flow

```
Draw a data flow diagram for a eCommerce website that can take orders, check inventory, create invoice, and process orders.

Processes should be circles, data stores should be cylinders, external entities should be rectangles.

On each connection, label what data is being passed through.
```

- PTO management system data flow

```
Draw a data flow diagram for PTO management system. 
It should sync to the payroll system as well as the HR management system. Employees should be able to submit PTO requests, managers approve requests, and HR staff create weekly reports.

Processes should be circles, data stores should be cylinders, external entities should be rectangles.

On each connection, label what data is being passed through.
```

## [AI Use Case Diagram Generator](https://www.eraser.io/ai/use-case-diagram-generator)

- learning management system

```
Generate a use case diagram for a learning management system for an school where the users are students, teachers, parents, and school admins.

A use case diagram consists of users and use cases. Users are rectangle shapes and use cases are oval shapes. Connections between users use cases show what users have what use cases, don't add any other connections. Put use cases in a group called use cases. Don't put users in a group and don't group use cases by users. Include "Use Case Diagram" in the title.

```

- order shiping management system

```
Generate a use case diagram for a order shipping management system for an eCommerce brand where the users are customers, IT manager, warehouse workers, logistics workers, and business analyst.

A use case diagram consists of users and use cases. Users are rectangle shapes and use cases are oval shapes. Connections between users use cases show what users have what use cases, don't add any other connections. Put use cases in a group called use cases. Don't put users in a group and don't group use cases by users. Include "Use Case Diagram" in the title.

```

## [AI State Diagram Generator](https://www.eraser.io/ai/state-diagram-generator)

- issue tracking system

```
Generate a state diagram representing states of an issue in a issue tracking system. The states are open, in progress, resolved, and closed. Tickets can be re-opened.

States are circle shapes. And connections represent the transition between states. Use icons as appropriate.
```

- user authentication

```
Generate a state diagram representing states of user authentication. The states are the following:
- Logged Out
- Submitting Credentials
- Waiting for MFA
- MFA Verified
- Logged In
- Session Expired
- Account Locked

States are circle shapes. And connections represent the transition between states. Use icons as appropriate.
```

- 3 states of water

```
Generate a state diagram representing the three states of water.

States are circle shapes. And connections represent the transition between states. Use icons as appropriate.
```

## [AI User Journey Map Generator](https://www.eraser.io/ai/user-journey-map-generator)

- food delivery app order flow

```
A user journey for a QuickBite user, a food delivery app:
    - The user feels hungry and decides to order food.
    - The user opens the QuickBite app.
    - The user browses restaurants based on location, cuisine, or ratings.
    - The user selects a restaurant or exits the app.
    - The user views the menu and adds items to their cart.
    - The user reviews the cart and selects either pickup or delivery.
    - The user logs in or creates an account if not already signed in.
    - The user enters or confirms the delivery address and payment details.
    - The user places the order and receives an estimated delivery time.
    - The user tracks the order status in real time.
    - The user receives the order and rates the experience.
    - The user is offered a promo or loyalty points for a future order.
```

- puppy training user journey

```
A user journey for a PawPath user, a puppy training platform:
- The user gets a new puppy.
- The user learns about PawPath training.
- The user decides whether to join the program or exit.
- The user selects the puppy’s age group. If the puppy is under 4 weeks old, the user is informed that the puppy is too young for training and is advised to return later. If the puppy is between 4–12 months, the user continues with PawPath. If the puppy is over 1 year old, the user is referred to a partner platform.
- The user creates a puppy profile.
- The user chooses a training plan from the following options: Starter, Plus, Premium, or Custom.
- The user selects either a self-guided or trainer-led training path.
- The user begins basic training.
- The user checks the puppy’s progress and either adjusts the training or advances to the next lesson.
- The user completes the training or continues lessons as needed.
- The user decides whether to continue with advanced training or exit.
- The user ends with a well-trained puppy.
```

## [AI Workflow Diagram Generator](https://www.eraser.io/ai/workflow-diagram-generator)

- leading score process

```
A lead scoring process:
01. Lead Capture
  - Web forms (e.g., demo requests, gated content) via HubSpot
  - Ad and webinar integrations (e.g., LinkedIn Lead Gen)
  - Manual entry from events or outbound efforts
02. Lead Enrichment
  - Append company and contact data using LinkedIn
  - Supplement with real-time enrichment from web traffic or form fills
  - Optionally validate emails for quality
03. Lead Qualification
  - Filter for:
      - Business email addresses
      - Complete contact details
  - Match against ICP:
      - Industry
      - Company size
04. Scoring & Evaluation
  - Behavioral Scoring (tracked via HubSpot and Mixpanel)
      - Website visits (e.g., pricing page +3)
      - Email activity (open +1, click +2, reply +5)
      - Product actions (e.g., trial started +10, feature usage +2 each)
  - Demographic Scoring
      - Job title/seniority (e.g., VP = +10)
      - Department match (e.g., IT, Ops = +5)
  - Total Score Calculation
      - Combine behavioral + demographic points
      - Apply score decay for inactivity (e.g., -1/week)
05. Score Thresholds & Routing
  - High score → Routed to sales via HubSpot automation
  - Mid score → Added to nurture campaigns
  - Low score → Sent to long-term nurture list

```

- Production downtime root cause analysis 

```
Production downtime root cause analysis process:

01. Downtime Trigger
  - Downtime automatically detected via MES/SCADA
  - If duration < threshold → Auto-log only, no RCA required
  - If duration ≥ threshold → Proceed to RCA
02. RCA Kickoff
  - Plant manager reviews the incident and assembles RCA team (cross-functional)
03. Root Cause Investigation
  - Analyze system data and gather input from involved personnel
  - Use structured methods (e.g., 5 Whys, Fishbone)
  - If root cause is unclear → Escalate or increase monitoring
  - If root cause is clear → Proceed to next step
04. Action Planning
  - Define corrective and preventive actions
  - Assign ownership based on cause:
      - Maintenance, Operations, QA, or EHS
  - Log and track actions in the CAPA system
05. Resolution & Closure
  - Verify effectiveness (e.g., test uptime)
  - Plant manager signs off
  - Document findings and share lessons learned

```

## 💡 [AI Block Diagram Generator](https://www.eraser.io/ai/block-diagram-generator)

- CI/CD pipeline

```
Generate a block diagram of the CI/CD pipeline.

All nodes are rectangles. Create sensible groupings. The diagram title should include "block diagram".

```

- pc components

```
Generate a block diagram of components inside a PC.

All nodes are rectangles. Create sensible groupings. The diagram title should include "block diagram".

```

- microservices architecture

```
Generate a block diagram of the microservices architecture.

All nodes are rectangles. Create sensible groupings. The diagram title should include "block diagram".

```

## [AI Org Chart Generator](https://www.eraser.io/ai/org-chart-generator)

- manufacturing company with many employees and 5 sites

```
Draw an org chart of a mid-sized manufacturing company with ~1,000 employees and 5 sites.
- CEO
    - CFO
        - Controller
        - AP/AR
        - FP&A
    - COO
        - Dir. Supply Chain
        - Dir. Manufacturing
        - Logistics Mgr
        - Facility Mgrs (repeat 5x for each facility)
            - Prod. Supervisor
                - Line Workers
            - QA Mgr
                - QA Techs
            - Maintenance Mgr
                - Techs
            - Safety & Compliance Officer
            - HR/Admin
    - CTO/CIO
        - IT Infra Lead
        - ERP Lead
        - Security Lead
    - CHRO
        - Talent Acquisition
        - Employee Relations
        - Training & Dev
    - VP Sales & Mktg
        - Sales Mgrs
        - Mktg Mgr
        - Cust. Service Lead
```

- a sofware company

```
Draw an org chart of a public software company with ~2,000 employees.

    CEO (~2000)
- Chief of Staff
- Exec Assistant
Engineering (~900)
- VP Eng
    - Dir Backend
    - Dir Frontend
    - Dir Infra
    - Dir Quality (~100)
    - Dir Security Eng (~100)
Product (~200)
- CPO
    - Dir Product
    - Dir UX
    - Dir Docs
Sales (~250)
- CRO
    - VP Enterprise
    - VP Mid-Market
    - Dir Sales Ops
    - Dir Solutions Eng
Marketing (~150)
- CMO
    - VP Product Mktg
    - VP Demand Gen
    - Dir Content
    - Dir Brand
Customer Success (~150)
- VP CS
    - Dir Services
    - Dir TAM
    - Dir Support
Finance (~100)
- CFO
    - VP Finance
    - Dir Accounting
    - Dir FP&A
    - Dir IR
Legal (~40)
- GC
    - Dir Legal
    - Dir Compliance
People (~70)
- CPO (People)
    - Dir Recruiting
    - Dir HR Ops
    - Dir L&D
    - Dir DEI
IT (~40)
- Dir IT
Ops & Strategy (~30)
- VP Ops
    - Program Leads
    - BizOps

```

## [AI Sequence Diagram Generator](https://www.eraser.io/ai/sequence-diagram-generator)

- auth0 auth flow

```
User selects Login within application.
Auth0's SDK redirects user to Auth0 Authorization Server (/authorize endpoint).
Auth0 Authorization Server redirects user to login and authorization prompt.
User authenticates using one of the configured login options, and may see a consent prompt listing the permissions Auth0 will give to the application. Repeat this step until authentication is successful.
Auth0 Authorization Server redirects user back to application with single-use authorization code.
Auth0's SDK sends authorization code, application's client ID, and application's credentials, such as client secret or Private Key JWT, to Auth0 Authorization Server (/oauth/token endpoint).
Auth0 Authorization Server verifies authorization code, application's client ID, and application's credentials.
Auth0 Authorization Server responds with an ID token and access token (and optionally, a refresh token).
Application can use the access token to call an API to access information about the user.
API is activated.
If API is JSON endpoint, return JSON data.
If API is XML endpoint, return XML data.
API is deactivated.
```

## [AI Swimlane Diagram Generator](https://www.eraser.io/ai/swimlane-diagram-generator)

- insurance claims adjustment process

```
Steps for an insurance claims adjustment process (BPMN):
01.    Customer reports a loss.
02.    Intake team records the details and checks whether the policy is active and covers the loss.
03.    If the loss is covered, assign a claims adjuster — otherwise tell the customer and close the case.
04.    Adjuster asks the customer for photos, receipts, or other proof.
05.    If the loss is small enough for quick payment, skip inspection; otherwise schedule an inspection.
06.    Adjuster (or inspector) reviews the damage and figures out the repair or replacement cost.
07.    A supervisor gives the cost estimate a quick check.
08.    Adjuster sends the payout offer to the customer.
09.    If the customer agrees, the payments team sends the money; if not, the claim is re-checked and a new offer is made.
10. When payment is sent and accepted, the claim is marked complete.
```

## [AI Network Diagram Generator](https://www.eraser.io/ai/network-diagram-generator)

- office network diagram with cisco icons

```
Fiber connection connects to router 1, cable connection connects to router 2. Router 1 and 2 connect to router 3. Router 3 connects to Switch 1. Switch 1 to both of switch 2 and 3. Each of switch 2 and 3 connects to separate ip phones, PCs, and wireless routers.

Use Cisco icons.
```

- office network diagram with general icons

```
Internet traffic comes in through an external firewall to a router which connects to a server switch. The server switch connects to a web server, file server, database server, and a mail server. The server switch also connects to an internal firewall. The internal firewall connects to an internal switch, which connects to PCs, smartphones, IP phones, laptops and a directory server.

Use generic networking icons. Don't group nodes.
```

## [AI AWS Diagram Generator](https://www.eraser.io/ai/aws-diagram-generator)

- aws fleet management system

```
A three-tier web application of a fleet management system using AWS resources:

- Presentation Layer: S3 and CloudFront power the frontend web interface for users (fleet operators, drivers) to access.
- Application Layer: ECS with Fargate and API Gateway manage the backend services. Amazon SNS power event-driven notifications.
- Database Layer: RDS for structured data and DynamoDB for real-time data
```

- aws wordpress website

```
Host a wordpress website using AWS resources. Use Route 53 for DNS management to route traffic to an Elastic Load Balancer (ELB), which distributes requests across EC2 instances in an Auto Scaling group. These instances run a web server with PHP to serve WordPress, accessing RDS for the database and EFS for shared file storage. CloudFront acts as a CDN, caching static assets closer to users for faster delivery, while S3 can optionally store large media files, serving them through CloudFront. All components are hosted within a VPC with the RDS in a private subnet.
```

## [AI Azure Diagram Generator](https://www.eraser.io/ai/azure-diagram-generator)

- student record management system

```
A three-tier web application of a university student record management system using Azure resources.

- Users: Students and faculty
- Presentation Layer: React web interface supported by Azure Blob Storage and Azure CDN.
- Application Layer: Azure Kubernetes Service (AKS) manages the backend services with Azure API Management managing the API endpionts. Service Bus handles event-driven notifications and backend processing.
- Database Layer: Azure SQL Database stores structured records; Azure Cosmos DB supports real-time interactions.

```

- rag based queries on a codebase 

```
An Azure-based RAG application for querying a company’s codebase. Azure Front Door manages global request routing, directing users to a web interface hosted on Azure App Service or Static Web Apps. When a user asks a question, it’s routed through Azure API Management. Azure Cognitive Search indexes the codebase stored in Azure Blob Storage or Azure DevOps Repos to retrieve relevant snippets. These results are then passed to Azure OpenAI Service to generate context-rich responses. Azure Functions handle data transformations, while Azure Cache for Redis speeds up response times by caching frequent queries. The response flows back through API Management to the web interface, with monitoring managed by Azure Monitor and Application Insights.
```

## [AI Kubernetes Diagram Generator](https://www.eraser.io/ai/kubernetes-diagram-generator)

- wordpress hosting using azure kubernetes services

```
Public Internet as the entry point for external traffic.

Azure Front Door with an Azure Web Application Firewall (WAF) to protect against common web vulnerabilities, receiving traffic from the Public Internet and forwarding it to internal components.

An Internal Load Balancer to manage traffic directed to a WordPress pod hosted in an Azure Kubernetes Service (AKS) cluster.

Within the AKS cluster, include:
- Ingress to manage external access to services.
- 2 WordPress pods connected with via autoscaling for dynamic scaling based on load.
- Secret store CSI pod for secure storage of secrets.
- Azure NetApp Files for storage.

Outside the AKS cluster include:
- Azure Container Registry for storing container images.
- Azure Key Vault for managing keys, secrets, and certificates.
- Azure Database for MySQL.
- Azure Cache for Redis for caching and data storage.

4 private endpoints connect:
- AKS to the Azure Container Registry
- CSI pod to Azure Key Vault
- 2 WordPress pods to Azure Database for MySQL
- 2 WordPress pods to Azure Cache for Redis

Use kubernetes icons where possible.

```

- prestashop hosting using google kubernetes engine

```
Architecture to host Prestashop on GKE which contains:
- Browser: End-user device connecting to the application.
- Cloud CDN: Caches content to improve load times for users.
- Cloud Load Balancing: Distributes traffic across multiple instances for load management and availability.
- GKE Cluster:
    - Hosts 2 PrestaShop pods, each with:
      - Cloud SQL Auth Proxy: Secures access to Cloud SQL database.
      - PrestaShop: The e-commerce application.
    - NFS (Network File System): Provides shared storage for GKE instances
    - PV and PVC connecting to the NFS
- Cloud SQL: Managed database for PrestaShop.
- SSD: Backs the NFS

Data flows as follows:
- Browser → Cloud CDN → Cloud Load Balancing → PrestaShop → NFS
- Auth Proxy → Cloud SQL.
- NFS → PVC → PV → SSD

Use Kubernetes icons and GCP icons where possible.
```

## [AI ERD Generator](https://www.eraser.io/ai/erd-generator)

- twitter data model

```
Data model for Twitter that includes users, followers, DMs, likes, bookmarks, retweets, tweets, lists

```

- ecommerce sql schema

```

// SQL schema creation script
CREATE TABLE CART
(
  ID INTEGER PRIMARY KEY NOT NULL, 
  CUSTOMER_ID INTEGER NOT NULL, 
  NAME VARCHAR(50) NOT NULL
); 
CREATE TABLE CART_ITEM
(
  CART_ID INTEGER NOT NULL, 
  PRODUCT_ID INTEGER NOT NULL, 
  ITEM_QTY INTEGER NOT NULL, 
  LAST_UPDATED TIMESTAMP DEFAULT CURRENT_TIMESTAMP() NOT NULL, 
  PRIMARY KEY ( CART_ID, PRODUCT_ID )
); 
CREATE TABLE CATEGORY
(
  ID INTEGER PRIMARY KEY NOT NULL, 
  NAME VARCHAR(50) NOT NULL, 
  DESCRIPTION CLOB
); 
CREATE TABLE CUSTOMER
(
  ID INTEGER PRIMARY KEY NOT NULL, 
  NAME VARCHAR(100) NOT NULL, 
  PASSWORD VARCHAR(20) NOT NULL, 
  LAST_UPDATED TIMESTAMP DEFAULT CURRENT_TIMESTAMP() NOT NULL, 
  REGISTRATION_DATE DATE DEFAULT CURRENT_DATE() NOT NULL
); 
CREATE TABLE PRODUCT
(
  ID INTEGER PRIMARY KEY NOT NULL, 
  NAME VARCHAR(50) NOT NULL, 
  DESCRIPTION CLOB NOT NULL, 
  PRICE DECIMAL(5, 2) NOT NULL, 
  STOCK_QTY INTEGER NOT NULL, 
  LAST_UPDATED TIMESTAMP DEFAULT CURRENT_TIMESTAMP() NOT NULL, 
  CATEGORY_ID INTEGER NOT NULL
); 
ALTER TABLE CART ADD FOREIGN KEY ( CUSTOMER_ID ) REFERENCES CUSTOMER ( ID ); 
CREATE INDEX FK_CUSTOMERCART_INDEX_1 ON CART ( CUSTOMER_ID ); 
ALTER TABLE CART_ITEM ADD FOREIGN KEY ( CART_ID ) REFERENCES CART ( ID ); 
ALTER TABLE CART_ITEM ADD FOREIGN KEY ( PRODUCT_ID ) REFERENCES PRODUCT ( ID ); 
CREATE INDEX FK_CARTITEMPRODUCT_INDEX_B ON CART_ITEM ( PRODUCT_ID ); 
CREATE UNIQUE INDEX UNIQUE_NAME_INDEX_F ON CATEGORY ( NAME ); 
ALTER TABLE PRODUCT ADD FOREIGN KEY ( CATEGORY_ID ) REFERENCES CATEGORY ( ID ); 
CREATE INDEX FK_PRODUCTCATEGORY_INDEX_1 ON PRODUCT ( CATEGORY_ID ); 

```

- music site prism schema

```

// Prisma schema
model albums {
  AlbumId  Int      @id
  ArtistId artists  @relation("albums_ArtistId_artists")
  Title    String
  tracks tracks[] @relation("albums_tracks_AlbumId", references: [AlbumId])
}
model genres {
  GenreId  Int      @id
  Name     String?
  tracks tracks[] @relation("genres_tracks_GenreId", references: [GenreId])
}
model artists {
  ArtistId Int      @id
  Name     String?
  albumses albums[] @relation("albums_ArtistId_artists")
}
model playlists {
  Name            String?
  PlaylistId      Int              @id
  playlist_tracks playlist_track[] @relation("playlist_track_PlaylistId_playlists")
}
model playlist_track {
  PlaylistId playlists @id(strategy: NONE) @relation("playlist_track_PlaylistId_playlists")
  TrackId    tracks    @id(strategy: NONE) @relation("playlist_track_TrackId_tracks")
  @@unique([PlaylistId, TrackId], name: "sqlite_autoindex_playlist_track_1")
}
model tracks {
  AlbumId         albums?          @relation("albums_tracks_AlbumId")
  Bytes           Int?
  Composer        String?
  GenreId         genres?          @relation("genres_tracks_GenreId")
  MediaTypeId     media_types      @relation("media_types_tracks_MediaTypeId")
  Milliseconds    Int
  Name            String
  TrackId         Int              @id
  UnitPrice       Float
  invoice_itemses invoice_items[]  @relation("invoice_items_TrackId_tracks")
  playlist_tracks playlist_track[] @relation("playlist_track_TrackId_tracks")
}
model invoices {
  BillingAddress    String?
  BillingCity       String?
  BillingCountry    String?
  BillingPostalCode String?
  BillingState      String?
  CustomerId        customers
  InvoiceDate       DateTime
  InvoiceId         Int             @id
  Total             Float
  invoice_itemses   invoice_items[] @relation("invoice_items_InvoiceId_invoices")
}
model invoice_items {
  InvoiceId     invoices @relation("invoice_items_InvoiceId_invoices")
  InvoiceLineId Int      @id
  Quantity      Int
  TrackId       tracks   @relation("invoice_items_TrackId_tracks")
  UnitPrice     Float
}
model media_types {
  MediaTypeId Int      @id
  Name        String?
  tracks    tracks[] @relation("media_types_tracks_MediaTypeId", references: [MediaTypeId])
}
```

# more
