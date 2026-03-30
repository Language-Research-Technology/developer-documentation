---
title: Use Cases, Software Architecture and Deployment Patterns

---

(This page is a work in progress, first version is a quick update from the Arkisto website: will be updated with fresh examples in Q2 2024)

There are multiple use cases for RRKive which we will document in the abstract, in addition to the specific [case studies](/case-studies/) we're already working on. Due to its standards-based and extensible nature, RRKive can realise the goal of making data [FAIR](https://www.force11.org/group/fairgroup/fairprinciples) (Findable, Accessible, Interoperable, Re-usable).

# The (mythical) minimal RRKive platform

The simplest possible RRKive platform deployment would be a repository with some
objects in it. No portal, no data ingest or preservation service, eg:

![An OCFL repository containing two RO-Crate data objects](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDuIfAJIv9p4lFILLGydTsyr48IYt8ByuioI-gL59GgEP2bW_ortKkIYn9LV1FoWAAAXWg0HNKubLY15K2n0wfUIb02m40)

That might not seem very useful in itself but a standards-based repository is a
great candidate for data preservation - it puts the _I_ in FAIR (Interoperable)
data. It can also provide a basis for re-activation via services that can Reuse
the data by making Findable and Accessible. Because of RRKive's use of
Standards, the repository is the core to which services can be added.

# Adding a web portal

To make the data Findable - the F in FAIR Data a portal may be added - this
requires some configuration but significantly _less_ than building a service
from scratch.

![Adding a portal with an indexer, configuration and authorization service](http://www.plantuml.com/plantuml/svg/VP2n2i8m48RtFCMHlOEE3gLIS18AVOFOdZLIS-Lo0RNuxiQsOAGW8Slt_VbpNE75i8HRhnWRCQxh4VH0BARNCARGkXRlo1_wIdb3xcox5Tu7kH3Rfn5BRhBnABMqG9RbeAloS8GQ1_9MY1yQTZ3vRog7kJwQu56fv8VrQnX_V5rb9Hj1g4xNI64pJ_4libqYyHReshYMDm00)


For example the [Oni](https://github.com/Language-Research-Technology/oni-ui)
toolkit is used by the Language Data Commons of Australia for its portals, the
main one being <https://data.ldaca.edu.au/search> 

![Alt text](image.png)

The same portal software has been used in other contexts and is being adapted at
the University of Sydney for a variety of data collections. 

Web portals depend on the repository content being *indexed* - web pages are
generated mostly from calls to the index, and thus can be highly performant.
There is more on indexing below.


# Data ingest pathways

But how does data get into an OCFL repository? There are several patterns in production, in development and planned.

## A snapshot repository

Exporting a repository to RO-Crate can be a matter of writing a script to
interrogate a database, convert static files, or otherwise traverse an existing
dataset.

This pattern was used by
[the 2020 snapshot of ExpertNation](https://expertnation.research.uts.edu.au/) -
where we were given an XML file exported from the Heurist Content Management System and used a script to
convert that data to the RO-Crate format. This RO-Crate can in turn be deposited
in a repository - in this case the
[UTS data repository](/case-studies/uts-repo) - and
[served via a portal](#adding-a-web-portal), preserving the data while at the
same time making it Accessible.

![Screenshot of the Expert Nation Portal 2020 snapshot showing a website with faceted search](image-1.png)

![A conversion script converts existing objects in a repository to RO-Crate format and deposits them in an OCFL repository](http://www.plantuml.com/plantuml/svg/RP7DQiKW44RtFiNWta2tfPI0RLU5GFe4apW4Kwj19_qXzDsluYRX2hCPptTq6Fl467d_Si8WuuI9GBx-siJMBw23SpIp3Lx28OI8kK6_E08vJ6jkuA60_mlfkau2fbpcSwsq8Vegbhfo7VmtnPJVX8yvserBiCHQv4djcpeFymWZeMc7bGa_NZs370Ub8pB1sNkXBIJBrrdrspkC5OJu9m6E4szSrDn6FMoBTzleoPly6pS0)

This pattern has also been used extensively in the Language Data Commons of Australia where individual collections of data are converted using a series of scripts - instead of creating an entire site from one collection as in Expert Nation, each collection is loaded into the site.

![](https://raw.githubusercontent.com/Language-Research-Technology/plantuml-diagrams/7e60dc60cb129c65c99382fba8ea7dbabd52b89a/onboarding/ldaca-batch-data-conversion.svg)


<!----

## A growing cultural collection

In [PARADISEC](/case-studies/paradisec/), research teams add collections and items using bespoke tools that were written for the archive.

![A researcher describes data using Describo and deposits it in the PARADISEC repository](http://www.plantuml.com/plantuml/svg/XO_DQi904CVl-nH33hqfzDg366C5mLP9ds2wEyR5pOxCRcgB-ExTL9CgIWk1BFF_cD-CGqI9JUrKs5g_Gy4QuA1o4TuNx5XWub1lLQuZouJ5aDoEqwiIRhmvIVkDZQHAqX5zvUWcr2ltWqUb5BQzK58W5BqXKKgw46HJ2bhiEsTmk1olyZAVpj-U2tYXY0OZmafuRHrbbxP5-ZTO4MWs5AwabT27vIP0mJxIPymIowK-i-GC97mMOtqLu05UEQOIm03hHDFwrIyr30pl_M2Kj2SuKvDIwtxUNP9ItHE6mn7iVlmx3ZQ2ZLG7G6z02s5ikPrBJ9PzKFVlNnQp1PIdFCjNYvSguN1bBvU3Gjg-ULe0ZzaP_vwZw3VslZ-gV6iv_bFKkT8t9c-Qsdq3)

-->


## Field data capture

Data from sensors in the field is often streamed directly to some kind of database with or without portal services and interfaces. There are multiple possible RRKive deployment patterns in this situation. Where practical, the UTS eResearch team aimed to take an approach that first keeps copies of any raw data files and preserves those. The team then built databases and discovery portals from the raw data, although this is not always possible.

This diagram shows an approximation of one current scenario which was implemented at UTS where raw files were NOT available, but readings could be extracted from a Database:

![Sensor data capture via a vendor-supplied database, with a custom script to convert monthly reading ](https://www.plantuml.com/plantuml/svg/XP11Q_f04CNl-oa63_zRHFDlBwM8cc1BArWIw7tT7M8mxgIpkreHltiJ5x56eI67v3VlpSoRiNMIdTzKmgvBKqkM6u23c33JBg6A6AQLL6inKOvuIgoHRt7pLJ1veqDfjoeTYWoLawQei6kwLEuRaugylXqLy5t7KRIFQWMGex74jid0vp5WXytlyJU8k-1_5pnqmUC9jEzvn7EaQMSYq4juWbV9MxGE6AKkJM65IAMJIsaHUfzeD35yC6rBZHhEbHv8sxeF8aIuJEkr4aXaxJmZv8hBsWMrwWWpj2XPhU25oTUmI6PpoB0cMphY_SbJ01okF2508mkhGZo81z5W215aYoXXwS9cbkEmsfMvt--Vgca-Uv-d-LkG_Db-6Dzf7Wwg5KI-ZaRXa5yUUT-oSDrHgspmH6j8o3ZyTl0Fqf1GZD5elwb-0000)



## Analytical and housekeeping tools

So far on this page we have covered simplified views of RRKive deployment patterns with the repository at the centre, adding discovery portals and giving examples of data-acquisition pipelines (just scratching the surface of the possibilities). These things in themselves have value: making sure data is well described and as future proof as possible are vitally important but what can we DO with data?

### OCFL + RO-Crate tools

Having data in a standard-stack, with OCFL used to lay-out research data objects and RO-Crate to describe them, means that it is possible to write simple programs that can interrogate a repository. That is, you don't have to spend time understanding the organisation of each dataset. The same idea underpins RRKive's web-portal tools: standardization reduces the cost of building.

-   <b>Validators and preservation tools</b>: there are not many of these around yet, but members of the RRKive community as well as the broader OCFL and RO-Crate communities are working on these; expect to see preservation tools that work over OCFL repositories in particular.

-   <b>Brute-force scripts</b>: for moderate-sized repositories, it is possible to write a scripts to examine every object in a repository and to run analytics. For instance, it would be possible to visualise a number of years' worth of sensor readings from a small number of sensors or to look for the geographical distribution of events in historical datasets.

![Simple brute-force script to draw a graph can visit every object in OCF](http://www.plantuml.com/plantuml/svg/VL1DRzD04BtxLpprWE3WACc9ze3Q92eIL2fA9Ew3Ts8lNU-kPcU9eeh_pc0e2afKomVxVRotRs-BacWTGrEUVCmaD0BFpPr8EgnJI89LeEwfkUiqoIg9Opc7xQkNLAFxGnq6hznikLEAVU0pqp_cid4TKdNdLHDysV6piKTUKh7nrDiEcs7C2NwraghSxfDqZDA9pte5AYXDKz2wT8Zj1_IumLTVl89_i1oHldst051qw5dXIEctkcRJlXJTu8iaLotLVlE0jzn3USmif5KORr0e-AX7a2Nu_Pw5eneuvi1md7KeI5O77HY1YkB89EzEpxxbOb0tuAFDptXStpzWopaLhqcEquuUDldKi-DOafYCd8zzmUBw-dqxNw35zh5T2obFliNoxrMTUcUpsKHkTlUV7pQxJvFarVJbV3blBUk_R6jxDf-zjnnT7SCl)

### Adding databases and other indexes

For larger-scale use, visiting every object in a repository can be inefficient. In these cases, using an index means that an analysis script can request all the data in a particular time-window or of a certain type - or any other query that the index supports. 

![Adding an index can improve script performance](https://www.plantuml.com/plantuml/svg/VL7DRjim3BxhAOWSXktW8CbfpQ5ewg33jWBjd2SWB5OMAai6HSqpWhxxv7WD7AIOxGFz_V27l8k2BAbrAhvQto5Z2t1KE-RGby45Xdk7zQlQrHBuFh0clePpP3WahoUgRwoGggWMzCRHbUdCV6miNKZwkjG4V-XuK_dXzwomjsZ6EOugCpDyiVFeXcWZn9fj9ml075uedWCBkWKSP-1th-bFHjxogoO153hqlhW50zj_V4LTY3PlOr3nJ4_K5dubuW4aW241ZOAZvlRSw1QUEUXK4-JVhe7FPA178GQXbXWbCS4dYEYibm4mvx0lByJa9ODjvmWqTT942Bz7KqFWC0eCXFnbFbv5CKDr0zyuf0wUoeV7MUEdVPZn_7FFWNmCd6MehJSHrZStNulL6WgedeeoDqSdttepxVl2krmkJ-J-yF3pSN_uyIvH_wsmMMrMnNfpcJzN74-GlploEhNkBm00)

While the index engines used in our current portals are based on full-text search and metadata, we expect others to be built as needed by disciplines using, for example, SQL databases or triple stores.

### Analysis tool integration

Above, we have looked at how people or machines can access an RRKive platform deployment by querying the repository, either directly or via an index. However, there is a much larger opportunity in being able to integrate RRKive deployments with other tools in the research landscape. To take one example, text analysis is in great demand across a very wide range of disciplines. This _hypothetical_ scenario shows the potential for a researcher to use a web portal to locate datasets which contain text and then send the whole results set to a an analysis platform, in this case an interactive Jupyter notebook.

![Researcher uses a web portal to locate datasets "Show me all records with attached text from 1950-196" and send the subsequent results set to a Jupyter notebook in Binderhub](https://www.plantuml.com/plantuml/svg/VL5DRvj04BtlhnZvr1xiGjHKIWzLR4UfcbfjP5VgUO0D89OTD3ihOaN-xrqWDAP65HpGpFjuRxXrWYo-DifLfMsGiGPuKMjcQhTaY65ZCAtKEXNY3N6c-N8Sld8cRxDXrHQbQBNNgQ3DZRuW_TtC4xU6V7PfDOnd6IUbi0i2U-qqSbfeLef75rXiIXl42fyi01su5YsydEz_wMU1jKLpTAM31zySHJFy8D49KTMJRDAvg3S3M6RKskKNU2GMDF0P3WMrK6j0Oo28Xm8Esb8AG14Cb0oaytbYgY6--HWjuvjFqVybT-XjMa1fOHhnqQ0y4TTAlK83oIPlXFO3P2W8xsOStqyiH-9lucf8QrzhJouus2mcP_iMZleS9gVmZ3d61dcG7FPxtP0hXVWu4HmZm5Scty3FxVtk3DgVF8SW_kzlSg58r1MvZdfGVDM1Jce2NArM_VBkSFzzTtTu625gLkuwNbv5qI0NnNsXyDvgc_dQ_040)

RRKive already allows re-use of visualisation tools and viewers that can be embedded directly in a portal. We are planning a "widget store" that will enable researchers to choose and deploy a number of add-ons to the basic portal.

# Institutional and discipline repositories

One of the major use case deployment patterns for RRKive is to underpin an
institutional data repository / archive function, see the
[UTS data repository](/case-studies/uts-repo/) for an established example.

In this use case, data is ingested into the repository via a research data
management system which talks to the OCFL repository, _not_ the portal. There
is a clear separation of concerns: the portal's job is to provide controlled
access and search services via an index, the OCFL repository keeps version
controlled data on disc, and the Research Data Management System handles deposit
of data.

## Manual archiving

![Researcher deposits a dataset into an OCFL repository](https://www.plantuml.com/plantuml/svg/TP11Qzj048Nlyoi67rDio3NGaiGYa3PfZKr_m4WxjPUiTipi2DUO_FUij3Y9i89qqBxtlgVPkKr6QbqRm6IF9bYBcRJel79ZNY90Ul5nJqejuWdkLEMmb22Azu6Q5xXhJFHUrB5Uolbhgz95Lwp3pXl3EXTJt0Q-WDwTQN0Pf7ENloho9F5RZCkv7gBzkHHSg9FyAm3r5y4r9oPjTgm0UfuIPsSPApB2PugqvPQZuUQOZDiPKaAjyGHz4toKuDp98Sv_zEOD_jq78OUsymaT6IKsfEYGp2Xtcs1xn7NrlBe2oC2ym3sTuOhtahozW_7RDK0KOrI_tHdAFzJw1gzw7h_ZbnEl0iMlHwmuDUfh7Wq9C5h6IjGepF3qINoCZlzdvJK_K08VnRct-Ejo1z7ZgF0n9lFMcPUOiJ_BXwTFoR9RnDC8gSvR6EnODZzAB1QBmQis3x-UgitFSmGcUww7h1zkaDzRZgvhmni0)

At UTS the Research Data Management system in use is
[RedBox](https://www.redboxresearchdata.com.au/) - an
open source platform for managing data
across the research process from research data management planning (via Research
Data Management Plans (RDMPS)) to archiving and re-use of data. ReDBox has
services for provisioning and/or tracking _Research Workspaces_, which are sites
where research data collection and management. All of the data acquisition
scenarios described above would qualify as Research Workspaces, as do
file-shares on institutional storage or share-sync services such as CloudStor,
as well as survey platforms, project management and version control systems such
as Gitlab and Github.

<!--
## Fetching data from Research Workspaces

UTS researchers will be able to use the Research Data Management System to select a workspace for archiving, add metadata as appropriate, and the system will deposit the data for them.

![Coming soon: Researcher deposits a dataset by taking a snapshot of a dataset (or part thereof) in a Research Workspace](http://www.plantuml.com/plantuml/svg/RP11Rzim38Nl-XL4haC2z9h3q3H6XsxTEYI7dLc9IuN8ea7HyugY_tsI1MyUR1yC-_6zxucwJOgYVHkCSWVAyCogt8BpGbOzHsFIrSSE1Lk0DtCGuU78WGNk0jghELXbkMDn94ivVrs4--ZgQ7ZnIkQKmHWlWHQXlvFru35mxnPLLLvFV6EbkRNyBm55NS-_6uDb4JXH8XJxGcACJAU4pIH3Wuhm5IDUgAMeS7vDIkq6C84yvsihf7dm1yirTMXfdz7EOZTQXmJL-gyEjew7kFrOC7iuPCt_8h31HsynW8hFRrVQVmgtK676PFUsxt8i8_VmYRHwC3h8hLUyKEaxFMsFWahLNvjALOuqr77oDPPoF7wuCUMPB_6THJ5iu6qcFaH7lxFoNjQe1gZWogtpKwMplFu7V8X9lVRgEUROq_7-SUQibmcPFOyqq_d6SLovwjrkDywQy_sNn-RyURAOLSxDwFLbWsAxfUZwDlm1)

-->

## Publishing data

The UTS institutional data repository actually has two parts: an internal behind-the-firewall archive, with access control - to ensure that only authorized people can access data - and an external data portal for publicly accessible data. This architecture reduces the risk of data breaches by not allowing access through the firewall to sensitive or confidential data until secure tools are available to allow extra-institutional access.

Researchers can select a subset of an archived dataset to be published, or publish an entire dataset.

A "bot" "notices" that a new public dataset is available and copies it to the public repository, where it will be indexed and made available through the data portal.

![A researcher can select a subset of data and have it published on the Public Data portal](https://www.plantuml.com/plantuml/svg/bP51Rzim38Nl-XL4BjiEwR3h3aFJ606wTLkHOBTU58kDXSgYGT7BYg3_VIRa88vj3DZ9CidlYU_fDebbQUjWX1eGWZs9K0tECvRYAHgJNdniBDiQu6HMp7HSKo26ks3B5xCgXVYEs25FoztfmDH6brl7oWkQRITiuo7W6Bfqvi5reDPDhihbUU872Gv7zNygeDLv_iqOgqPWYmajbnMoCNpU4XRdCXHMB7otqHwmnYYmUqs2zG9i0jvtiQcIkOZ0qj4nBhzeypCyjllWKmKEbzvrj7_swA0CFlhI1X3sDe2pOZkD3bXcMEaENZDQGT1sGe7uxYaUlLGG2GPYsdwAxpjxoD0cvCi3VvXJBR2Xv5NEN1c-ZqcyjChP03_NcmVOvb7Yrzv9cMqt0AShDZUXE6-ww7CPpjpSt2WDnMxpxQ7OVUr7_gNpQQ4NlKsaVZLEWzcJgA9-yvWUbctJ6zsWb9NQ7DQRKGBpbyCZiTYWwlqHJjTPEVm3z0nDPlGD5hf2jqIU7uQkTsRY4kZ_HB_YilA_yUDz5EJOhyNZDnY5FyqUJgFg8EO-vLkChgt3Nm00)

NOTE: There is no monolithic "Repository Application" that mediates all interactions with the file-base OCFL store but a set of services which operate independently. This does mean that processes must be in place to ensure that there is not file-contention, with two bits of software trying to update an object at the same time.
