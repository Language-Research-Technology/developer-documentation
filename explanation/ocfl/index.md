---
title: "Standards: Oxford Common File Layout"
date: 2024-01-01
---


[Oxford Common File Layout](https://ocfl.io/) (OCFL)  is a specification for laying out digital collections on file or object storage. It is designed with long-term preservation principles in mind; does not rely on specialised software and avoids the problem of locking data collections into monolithic repositories behind APIs.

<div class="my-8">
<img src="./ocfl.png" alt="A cartoon representing an OCFL repository as a set of parallel fields containing lumps representing data payloads" />
</div>

-   An **OCFL Repository** is a system of directories laid out on a filesystem using a prescribed layout. Each repository contains one or more **OCFL Objects**. An object contains an inventory and a set of versioned content directories.
-   The metadata describing an OCFL object's inventory and versions is stored as simple JSON files which are both human- and machine-readable, and can be processed with lightweight scripts.
-   The structure inside the content directories is not specified, so any existing collection of files can be deposited into an OCFL repository and later re-exported with its structure preserved.
-   OCFL places no restrictions on the file formats of object contents.

<div class="mt-8"></div>

## OCFL provides

-   Robustness against file errors and data corruption
-   Efficient versioning and de-duplication
-   Immutable data storage

<div class="mt-8"></div>

## Links

-   [OCFL website](https://ocfl.io/)
-   [OCFL Specification v1.0](https://ocfl.io/1.0/spec/)

<div class="mt-8"></div>

## Example

Here is a simplified view of an OCFL repository containing two objects, one of which has two versions and one with three:

<pre class="bg-black text-white p-8">
-   OCFL repository
    -   Object A
        -   inventory
        -   v1
            -   inventory
            -   content
        -   v2
            -   inventory
            -   content
    -   Object B
        -   v1
            -   inventory
            -   content
        -   v2
            -   inventory
            -   content
        -   v3
            -   inventory
            -   content
</pre>
