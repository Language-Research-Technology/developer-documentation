---
title: Workspaces vs Repositories 
author: PT
theme:
- Copenhagen
date:
- 2023-06-12
---
# Worspaces vs Repositories

![](./research_data_cycle.png)


::: notes
There is a fundamental distinction between repositories and workspaces and the role they play in a FAIR-compliant research workflow

:::

# Examples of Workspaces

Generic workspace examples include:

- Survey tools (Survey Monkey, ReDCAP)
- Electronic Lab Notebooks
- Code environments (Jupyter notebooks, Binderhub, Github*, Matlab, R Studio)
- Research & Analytical Databases**
- "R: Drive" or similar storage
- Cloud storage such as Dropbox, Google Drive or OneDrive

*Yes, git uses "repositories" but these do _not_ function as archives -- don't assume Microsoft, the current owner of github, will preserve research or other code

**No a database is not necessarily a _repository_ (more on that below)



# Features of a repository

<table>
<thead>
<tr>
<th> ⬇️ Governance / Policy ⬇️</th>
<th> ⬇️ Technology ⬇️</th>
</tr>
</thead>
<tbody>
<tr>
<td>

-  Purpose / mission

-  Data retention policies 

-  Planning:

   -  ongoing stewardship & contingencies 

   -  persistence of IDs 

   - data exit

   - software obsolescence

-  Deposit and use and redistribution licensing/permissions framework


</td>
<td>

-  Tested data-exit pathway*

-  Interoperable metadata framework

-  APIs

-  Implementation of ID resolution & updating

-  Discovery services / catalogues / indicies

   -  Collection / archival structures

   -  Full-text & semantic indexing

   -  Facets for discovery based on explicit and implicit metadata

-  Sustainable technology neutral access-control mechanisms

*Get this right and the other things follow



</td>
</tr>
<tr>
<th>⬆️ Repo as Institution ⬆️</th>
<th>⬆️ Repo Implementation ⬆️</th>
</tr>
</tbody>
</table>

::: notes

A repository is as much an _institution_ as it is a software  _implementation_.

:::

# CARE / FAIR 

<table>
<thead>
<tr>
<th> ⬇️ Governance / Policy ⬇️</th>
<th> ⬇️ Technology ⬇️</th>
</tr>
</thead>
<tbody>
<tr>
<td>
CARE Principles
</td>

<td>
FAIR Principles
</td>

</tr>
<tr>
<th>⬆️ Repo as Institution ⬆️</th>
<th>⬆️ Repo Implementation ⬆️</th>
</tr>
</tbody>
</table>


# Differences between Repositories and Archives (and why we say _Archival Repository_)


Repository and Archive are closely related terms used by different communities -- they both have a core meaning about 'keeping' something for an appropriate time span. Some non-archivists might quip that archives are where things go never to be seen again while to non-archivists Repositories, or digital libraries may lack the rigour of proper archival practice and use unfamiliar organizing principles. 

Repositories, in the Higher Education sector are probably best known for their role in the Open Access publications movement -- while these are typically called "Institutional Repositories", it is helpful to think of them as "Institutional Publications Repositories". Many of these do contain research data, but they typically do not have access controls for non-open data, have size limits for deposits and do not have built in domain-extensibility.

In the RRKive project we aim to set aside these interesting discussions in the interest of finding common ground so we use the term _Archival Repository_.




