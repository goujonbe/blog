---
title: "What does the future of data engineering look like"
date: 2022-05-06T19:27:38+01:00
tags: ["Data engineering"]
---

The field of data engineering is evolving quickly. This article describes three major trends I see become prominent in the coming years.

![Photo by Daniel Lerman on Unsplash](/img/future_data_engineer/telescope.jpg)

The role of a data engineer was almost nonexistent ten years ago. But, the need for this particular kind of software engineer has grown. As the field got more mature, the role evolved.

The responsibilities of a data engineer vary from one company to another and the role does not evolve at the same pace everywhere. But I see the role change in three aspects:

- Data engineers will massively leverage cloud technologies and SaaS products
- Data engineers will spend less time coding and more time monitoring
- Data engineers will switch teams from feature teams to foundation teams

Let’s go into the details.

## Data engineers will massively leverage cloud technologies and SaaS products

Ten years ago, companies were relying on on-premise infrastructure for storing their data. This is why **the first big data technologies were built for on-premise environments**. During this era, data engineers were spending a lot of time tuning the configuration of their machines at the cost of creating business value.

Then, **cloud providers came with the promise of providing services they manage for you**. Thus, you can focus on your business needs. This has been a game-changer.

Now, cloud providers and tech companies like Snowflake and Databricks have made big data easy. The data ecosystem also got more mature. New data startups arose in specific fields like data quality, data governance, or data ingestion. The integration between those products is seamless.

![Data landscape by LakeFS](/img/future_data_engineer/data_landscape.png)

The days when data engineers had one tool from the Apache Foundation for their specific need is long gone. They have a myriad of tools to do the same thing. Nowadays, data engineers have **the responsibility to choose the best tools**. As a result, they need to have a good knowledge of the ecosystem and know how to conduct benchmarks and choose relevant decision criteria.

Choosing the right tool for the right job is not easy. But **integrating tools to form a consistent data platform is also a challenge**. Some data engineers already leverage infrastructure as code to assemble these bricks and automate infrastructure deployment. I see this becoming a mandatory skill.

## Data engineers will spend less time coding and more time monitoring

The time when data engineers were developing complex ETL pipelines in Scala and Spark seems over.

For the extraction part, you can now use technologies like Airbyte to schedule extraction jobs from a lot of different sources. The loading part is no longer a pain point. Snowflake for example made it easy to load a file from blob storage into a table in a one-liner SQL command.

As far as the transformation step is concerned, dbt brought a new paradigm in which **you transform your data in your data warehouse using SQL as a primary language**. The **shift from ETL to ELT is complete**.

So, deploying a workflow has never been easier and we can say thank you to the modern data stack. The modern data stack is a set of technologies that aim to reduce the complexity of data workflows and increase data team velocity. Thanks to the modern data stack, data analysts can now be autonomous. They no longer need the help of data engineers to collect and transform raw data. But does it mean data engineers are no longer necessary in data teams? :worried:

I might be biased but I think the answer is NO.

![Credits imgflip](/img/future_data_engineer/meme_ambulance.jpg)

My guess is that **the role of data engineer will evolve towards a more ops-oriented role**-. The next generation of data engineers will focus on improving data reliability across the company. Their responsibilities will be:

- monitor execution of data workflows and configure alerts in case of incidents
- deploy the underlying infrastructure of data use cases
- create CI/CD pipelines to verify code correctness and automate deployments
- ensure data quality at all times

A few years ago, we noticed for software development the rise of software reliability engineers (SRE). We may see a similar trend in the data world. A new job title will come up: the **data reliability engineer**. They will be in charge of **making sure data is available on time and is trustworthy**.

We will see more data engineers being responsible for defining Service Level Indicators (SLI) and Service Level Objectives (SLO). They will also participate in on-call rotations and respond to incidents.

The day-to-day of a data engineer will evolve but the position inside the organization will also change.

## Data engineers will switch teams from feature teams to foundation teams

Historically, data engineers were members of feature teams. The issue is that it led to data silos and a lack of global consistency. This is why companies started to adapt themselves by creating transversal teams.

The next generation of data engineers won’t work on a particular data product. Their objective will be to **make product teams more productive**. To do so, they will responsible for providing the right set of tools. This is what the data mesh paradigm is all about: **distributed ownership with a foundation team that provides all the tools needed** to build data products.

So, the next time you will need to develop a dashboard for financial reports, you won’t need a feature team composed of a product owner, a data analyst, and a data engineer. The data analyst will be autonomous and will leverage the tools the foundation team deployed allowing him to quickly extract the necessary data and then compute KPIs upon this raw data.

Conclusion
Looking at the crystal bowl is a tough exercise. There’s a bit of uncertainty associated with the opinions expressed above. But I hope this article makes you think about the future of the role too and I would be happy to read your thoughts in the comments!
