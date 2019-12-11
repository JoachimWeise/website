---
title: Data Leader Days 2019
subtitle: Great event in Berlin near Oberbaumbrücke
date: 2019-11-14
bigimg: [{src: "/img/2019-11-14-data-leader-days/Spree.jpg", desc: "River Spree in the morning"}]
tags: ["ai-applications", "event"]
---

Today I had the pleasure to present at [Data Leader Days](https://www.dataleaderdays.com/), a two-day management forum for leaders in the data space. 2019 marked its 5th edition, hosting data practitioners from Retail, Telco, Industrial Goods and Finance. Focus was on practical data science applications, with excursions into more specific areas such as data catalogs or deep learning based image processing. The event was located in the [030 event loft](https://www.spreespeicher-events.de/locations/030eventloft/), an unusual venue with direct access to river Spree near [Oberbaumbrücke](https://de.wikipedia.org/wiki/Oberbaumbr%C3%BCcke). Here are some impressions:

{{< gallery caption-effect="fade" >}}
  {{< figure thumb="-thumb" link="/img/2019-11-14-data-leader-days/Oberbaumbrücke.jpg" caption="Oberbaumbrücke">}}
  {{< figure thumb="-thumb" link="/img/2019-11-14-data-leader-days/Joachim.jpg" caption="Presenting ...">}}
  {{< figure thumb="-thumb" link="/img/2019-11-14-data-leader-days/Spreespeicher.jpg" caption="Location">}}
{{< /gallery >}}


<!--more-->


There were too many presentations to mention them all. Instead I just summarize a few recurring themes.

**Business Value**

- Data science in industry is not an R&D topic and doesn't resemble a  Kaggle contest 
- It needs to focus on solving business problems and generating P&L impact
- Especially in SME companies management will closely monitor spending and progress


**No data science without data**

- 80% of time in data science projects is spent battling issues regarding data availability, accessibility or quality 
- Among the reasons are legacy, disparate systems, decentral data ponds, unclear data ownership etc.
- Data access for new projects can be a month-long struggle, trying to figure out
	- who are data owners and stewards ?
	- what are the rules for data access and use ?
	- what is the content of data sources ?
	- what is the data lineage ?
	- who can help with domain expertise ?
- Data engineers are overwhelmed by repeated ad-hoc requests for data access
- They spend most of their time supporting one-time requests instead of  establishing proper pipelines
- Against this background many companies are now establishing or revitalizing data governance or data management functions in their organizations that rely on dedicated and part time roles, both on the business and IT sides, to improve data quality, data lineage documentation, data cataloging etc.


**Sophistication of models**

- Many practitioners showed an inclination towards not-too-sophisticated models
- Sometimes it may even turn out that a certain questions doesn't require machine learning at all, but can be solved with classic IT and/or BI approaches
- The focus should be on 'getting the task done', not applying the latest modelling innovation just for the sake of it
- This tendency can be due to the fact that some companies act in regulated industries, such as banking, that require white-box models. 
- Or their applications depend on very fast inference times (milliseconds) 
- Or their use cases simply don't require the ultimate accuracy of complex black-box models
- One of the presenters went into approaches towards explainable AI (XAI), e.g. using LIME or SHAP (a nice online book on these topics can be found [here](https://christophm.github.io/interpretable-ml-book/)). Still, few of the participants seemed to be aware of or apply these techniques so far



**Building data science teams**

- Recruiting 'data scientists' with adequate competencies is in fact not the ultimate bottleneck factor today. However, mathematical intuition paired with programming experience is often not sufficient 
- Many companies are therefore struggling how to structure data science teams when they are leaving initial 'lab' phases
- On the one hand, data scientists should ideally be good communicators, develop a deep understanding of business specifics and take end-to-end ownership of project success. Many speakers stressed that were looking for people who are curious and want to proactively come up with relevant insights rather than those who are primarily interested in the tech for the tech's sake
- To support these aspects, several speakers indicated that they have dedicated roles in their teams who work at interface between business and tech, by the name of 'product owners', 'digital strategists' or 'data consultants'
- On the other hand, a major part of all data science projects is spent on hardcore engineering tasks beyond the pure 'science' part, i.e. data pipeline engineering, software engineering, testing etc.
- There is no clear blueprint how to get the mix and ratio between data science and engineering roles right and how exactly to split tasks between these disciplines - it very much depends on the specific context of companies and the expertise and preference of team members. Related discussion can be found in other blogs e.g. [here](https://monzo.com/blog/2019/11/04/how-we-scaled-our-data-team-from-1-to-30-people-part-1) and [here](https://www.locallyoptimistic.com/post/analytics-engineer/)





