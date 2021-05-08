# INDEXES ☝🏻

1. [Introducion](#introduction)
2. [Example: Library Catalog](#example-library-catalog)
3. [What is an index?](#what-is-an-index)
4. [How do Indexes Decrease Write Performance?](#how-do-indexes-decrease-write-performance)

## INTRODUCTION

Indexes are well known when it comes to DBs. One of the first things you should turn to when a database is no longer performant is database indexing.

The goal of creating an index on a particular table in a database is to make it faster to search through the table and find the row or rows that we want. Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.

## EXAMPLE: LIBRARY CATALOG

A library catalog contains a list of books in a library. The catelog is organized like a database table with columns for various bits of information.

Often, there are usually two such catalogs - one by artist name and one by book title. These are like indexes for a database of books. They provide sorted data that you can easily search by relevant information.

## WHAT IS AN INDEX?

## HOW DO INDEXES DECREASE WRITE PERFORMANCE?
