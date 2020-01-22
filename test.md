# Introduction

Noebs is a middleware that consumes EBS services. It was built to be simple, developer friendly and customizable enough to be used
in different scenarios and adapt to variety of different logics.

# Overview

We make great use of http status codes; it is one of our design decisions. We believe that they make client codes more easy and it helps us too to make a robust API.
You only get 200 on successful transactions.
You get 400 in case of missing a field, or using wron types
You get 502 in EBS payment gateway errors (e.g., insufficient fund)

# Authentication

What is the preferred way of using the API?

# Error Codes

We use different kind of error codes:

- 400 for validations errors (e.g., missing a required field)
- 502 for EBS (payment gateway) errors (e.g., when you have an insufficient balance)
- 504 for EBS (payment gateway) timeouts. E.g., EBS server is unreachable
