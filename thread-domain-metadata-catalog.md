---
title: thread-domain-metadata-catalog
tags: [dataset, metadata]
created: 2026-06-21T13:52:25.908Z
modified: 2026-06-21T14:37:54.210Z
---

# thread-domain-metadata-catalog

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-format/spec
- ## 

- ## 

- ## 

- ## 
# discuss-solutions
- ## 

- ## 

- ## 

- ## [Which Data Catalog Product is the best? : r/dataengineering _202509](https://www.reddit.com/r/dataengineering/comments/1nmyznp/which_data_catalog_product_is_the_best/)
- Open Metadata. Can be deployed fully on premise. There are AI features but I think they are available only in the SaaS version.
- Another vote for OpenMetadata. Really active community on Slack, really aggressive code development. You can run on prem, and if you want AI, it has to be installed specifically

- ## [Open source data catalog : r/dataengineering _202301](https://www.reddit.com/r/dataengineering/comments/10hx1gb/open_source_data_catalog/)
- I felt like OpenMetadata has a richer feature set and better docs as well, but I liked Amundsen's approach of using a graph db to store metadata.

- I got nice data catalog summary in case anyone would be interested - https://github.com/opendatadiscovery/awesome-data-catalogs

- Like CKAN, SOCRATA, CSW, SDMX, OPEN DATA SOFT? Are you talking about API/Software or protocol?
# discuss-ckan
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [PortalJS - 1-month content brief · Issue · datopian/portaljs _202606](https://github.com/datopian/portaljs/issues/1555)
  - Demo Video — From CKAN Backend to Modern Frontend in 5 Minutes 
  - CKAN operators know the backend is solid but the default frontend is showing its age. They want to improve the experience without a risky migration or rebuilding their data infrastructure.
  - Start with a CKAN instance — show the API endpoint returning dataset data
  - Show PortalJS Cloud connected to that CKAN instance as the frontend layer

- ## [FAQs about DataHub _202405](https://github.com/datopian/portaljs/discussions/1166)
  - DataHub can be used as a complement to CKAN. Specifically, DataHub PortalJS allows you to rapidly building powerful data portal frontends and integrates directly with CKAN. It is inspired by the "headless" CMS model and uses CKAN as a headless DMS. It can be used to create a alternative frontend to CKAN using modern frontend tooling and integrate alternative content sources.
  - DataHub can also be used as a full replacement for CKAN if you want to manage your metadata and content differently than CKAN. DataHub offers its own native metadata management but it also provides an innovative integration with GitHub as well as connectors to other metadata management solutions.
  - DataHub's real power is it allows you to mix and match especially in the backend. With DataHub you can have quickly and flexibly create a unified data portal experience that combines data in CKAN, docs in markdown in github, and blog and content in Wordpress.
  - DataHub can use many different data "backends" i.e. sources for data and metadata. For example, you can use CKAN, S3 etc. However, Git(hub) is our favorite and default backend.

- ## 👷 [Looking for an open source platform to host and share datasets elegantly (and easier than CKAN!) : r/opendata _202405](https://www.reddit.com/r/opendata/comments/1c54k8a/looking_for_an_open_source_platform_to_host_and/)
- 👷 Check out https://datahub.io/ and https://datahub.io/opensource
  - This does exactly what you want in terms of publishing from Github. There's a cloud version and a self-hosted version.
  - Disclosure: I helped create and build this. (I also created the original CKAN).

- ## [Why does nobody ever talk about CKAN or the Data Package standard here? : r/dataengineering _202504](https://www.reddit.com/r/dataengineering/comments/1kbbml9/why_does_nobody_ever_talk_about_ckan_or_the_data/)
  - CKAN is this open-source platform for publishing and managing datasets—used a lot in gov/open data circles.
  - Data Packages are basically a way to bundle your data (like CSVs) with a datapackage.json file that describes the schema, metadata, etc.
  - They're not flashy, no Spark, no dbt, no “AI-ready” marketing buzz - but they're super practical for sharing structured data and automating ingestion. Especially if you're dealing with datasets or anything that needs to be portable and well-documented.
  - So my question is: why don't we talk about them more here? Is it just too "dataset" focused? Too old-school? Or am I missing something about why they aren't more widely used in modern data workflows?

- Compared to other open source projects like DataHub and Amundsen, features in CKAN are comparatively lacking.
  - CSVs are insufficient in actually managing enterprise-scale data for tech-forward companies. CKAN is indeed a relatively old school method of looking at data. It, along with the CSV format, is not very well suited for larger datasets.
  - You also have data platforms like Snowflake and Databricks building native data packaging capabilities.

- Well, one can use CKAN as standalone, but here is (disclaimer: our) take on that - a modern CKAN based with AuthZ and AuthN, user controlled harvesters, JSON-LD, smart data models, API, extended DataGrids for metadata and data, user customizable scripting and rules, simple pricing, as a Data Catalog-as-a-service: https://fiwarebox.com/data-catalog-as-a-service or even (with additional modules) as a Data Space-as-a-service: https://fiwarebox.com/dataspace-as-a-service
# discuss-tips
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
