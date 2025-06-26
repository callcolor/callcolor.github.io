---
layout: post
title: "Sellozo Campaign Studio"
date: 2025-06-26 11:53:03 -0500
categories: Projects React Front-end Javascript Typescript
image: /images/sellozo
---

### Opportunity

Help independent 3rd party Amazon sellers to maximize keyword advertising.

### Existing Technology

Sellozo had an existing platform to optimize PPC advertising by discovering long-tail keywords. However, there was no way to customize the Sellozo keyword strategy to client needs.

### Solution

React, Typescript, HTML

[![](/images/sellozo_2.jpg)](/images/sellozo_2.jpg) A graph data schema was created with graph nodes defining advertising campaigns and graph edges defining how keywords are added and removed from those campaigns. A drag-and-drop interface was built to allow users to create and manage their optimized campaign strategies. Additionally, CSV import/export functionality was added to help users to make bulk edits to their strategies.

[![](/images/sellozo_3.jpg)](/images/sellozo_3.jpg) React Diagrams (https://github.com/projectstorm/react-diagrams) was chosen to handle the graphical interface because it allowed us to associate custom data objects and UI elements with both nodes and edges, allowed us to hide unnecessary features to keep the user experience simple, and fit well with our existing technology stack. Custom logic for drawing edges avoided elements overlapping or the need for customers to fiddle with irrelevant style-only elements.

Papa Parse (https://www.papaparse.com/) was used for CSV import/export. A custom algorithm traversed each graph, ensuring that each edge was included in the CSV only once even when the graph itself is cyclical.

Ultimately, Sellozo was able to give sellers and agencies more fine-tuned control over their marketing spend, which resulted in a competitive advantage.
